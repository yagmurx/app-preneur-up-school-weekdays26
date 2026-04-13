# **TEKNİK ÜRÜN GEREKSİNİM DÖKÜMANI (TECH PRD)**

**Proje Adı:** Mini Readers Club

**Aşama:** Faz 1 \- MVP (Minimum Uygulanabilir Ürün)

**Platform:** Sadece iOS (Native)

**Hazırlayan:** Yağmur YILDIZ PARILTI

**Durum:** Onaylandı

## **1\. Ürün Vizyonu ve İş Hedefleri (Özet)**

Mini Readers Club, modern ebeveynlerin çocuklarının okuma alışkanlıklarını takip etmelerini ve bu başarıları sosyal medyada estetik bir şekilde paylaşmalarını sağlayan premium bir iOS uygulamasıdır.

* **Kuzey Yıldızı Metriği:** Sisteme başarıyla eklenen toplam kitap sayısı.  
* **Viralite Metriği:** Kullanıcı başına Instagram'da paylaşılan sertifika/rozet sayısı.

## **2\. Teknoloji Yığını (Tech Stack) & Mimari**

MVP aşamasında hız, "premium" his ve esneklik (vendor lock-in'den kaçınma) dengesini sağlamak için aşağıdaki mimari kullanılacaktır:

* **Mobil İstemci (Frontend):** iOS Native (Swift). Yüksek performanslı UI ve akıcı animasyonlar hedeflenmektedir.  
* **Backend (API Katmanı):** FastAPI (Python). Tüm iş mantığı (business logic) ve yönlendirmeler burada koşacaktır.  
* **Sunucu & Dağıtım:** Render (FastAPI uygulamasını host etmek için).  
* **Veritabanı:** Supabase (Sadece PostgreSQL veritabanı özelliği kullanılacaktır).  
* **Dosya Depolama (Storage):** Supabase Storage (Uygulama içi oluşturulan başarı rozetleri ve kullanıcı görselleri için).  
* **Test Ortamı:** Apple TestFlight.

## **3\. VERİTABANI ŞEMASI (SUPABASE / POSTGRESQL)**

FastAPI üzerinden Supabase'e yazılacak ilişkisel veri modeli (ERD) aşağıdaki gibidir.

| **Tablo Adı** | **Sütun (Column)** | **Veri Tipi** | **Özellikler / Kısıtlamalar** | **Açıklama** |
| --- | --- | --- | --- |---|

| **users** | id | UUID | Primary Key, Auto-gen | Kullanıcının eşsiz kimliği |

| | apple\_sub\_id | VARCHAR | Unique, Not Null | Apple Sign-in'den dönen benzersiz ID |

| | email | VARCHAR | Unique | Apple'dan dönen gizlenmiş/açık email |

| | created\_at | TIMESTAMPTZ | Default: NOW() | Kayıt tarihi |

| **children** | id | UUID | Primary Key, Auto-gen | Çocuğun eşsiz kimliği |

| | parent\_id | UUID | Foreign Key \-\> users(id) | Hangi ebeveyne ait olduğu |

| | name | VARCHAR(50) | Not Null | Çocuğun adı |

| | birth\_date | DATE | Not Null | Yaş hesabı ve kürasyon için |

| | avatar\_color | VARCHAR(7) | Default: '\#E5E7EB' | UI'da çocuğu ayırt etmek için hex kod |

| **books** | id | UUID | Primary Key, Auto-gen | Kitabın sistemdeki ID'si |

| | isbn | VARCHAR(20) | Unique, Index | Barkod no (Hızlı arama için indeksli) |

| | title | VARCHAR(200) | Not Null | Kitap adı (Google API'den çekilen) |

| | author | VARCHAR(100) | Nullable | Yazar adı |

| | cover\_url | TEXT | Nullable | Kapak görseli (Google API url'i) |

| **reading\_logs** | id | UUID | Primary Key, Auto-gen | Okuma kaydı ID'si |

| | child\_id | UUID | Foreign Key \-\> children(id) | Kitabı okuyan çocuk |

| | book\_id | UUID | Foreign Key \-\> books(id) | Okunan kitap |

| | logged\_at | TIMESTAMPTZ | Default: NOW() | Ne zaman eklendiği |

| **milestones** | id | UUID | Primary Key, Auto-gen | Kazanılan rozet kaydı |

| | child\_id | UUID | Foreign Key \-\> children(id) | Rozeti kazanan çocuk |

| | threshold | INT | Not Null (Örn: 10, 25, 50\) | Hangi barajın aşıldığı |

| | unlocked\_at | TIMESTAMPTZ | Default: NOW() | Rozetin açılma zamanı |

## **4\. API UÇ NOKTALARI (FASTAPI \- REST/JSON)**

Swift uygulamasının haberleşeceği temel uç noktalar:

* **POST /api/v1/auth/apple**  
  * **Payload:** { "identity\_token": "string", "authorization\_code": "string" }  
  * **İşlem:** Apple token'ı doğrulanır, kullanıcı Supabase'de yoksa yaratılır, varsa getirilir. Geriye sisteme özel JWT (Access Token) dönülür.  
* **GET /api/v1/children**  
  * **İşlem:** İstek atan ebeveynin (JWT üzerinden tespit edilir) kayıtlı çocuklarını ve her çocuğun toplam okuduğu kitap sayısını (COUNT(reading\_logs)) liste olarak döner.  
* **POST /api/v1/children**  
  * **Payload:** { "name": "Can", "birth\_date": "2022-05-10" }  
* **POST /api/v1/books/scan**  
  * **Payload:** { "isbn": "9789750719387", "child\_id": "uuid" }  
  * **İşlem (Core Logic):**  
    1. DB'de isbn var mı bakılır. Yoksa Google Books API'ye gidilip kapak/isim bilgisi çekilir ve books tablosuna yazılır.  
    2. reading\_logs tablosuna ekleme yapılır.  
    3. Çocuğun toplam kitap sayısı hesaplanır. Eğer sayı tam 10, 25 veya 50 ise JSON yanıtına "milestone\_unlocked": 10 eklenir.  
* **GET /api/v1/curation/lists**  
  * **İşlem:** Statik kürasyon (0-2 yaş vb.) listelerini getirir.

## **5\. EKRANLAR (SCREENS) VE KULLANICI AKIŞI (UI/UX)**

Arayüz tasarımı, gereksiz siyah konturlardan arındırılmış, modern Apple stili "glassmorphism" (buzlu cam) efektlerine ve Notion benzeri minimalist, tipografi odaklı bir yapıya sahip olacaktır.

1. **Splash & Login Screen:**  
   * Temiz, beyaz/kırık beyaz arka plan. Ortada sadece uygulamanın logosu.  
   * Alt kısımda tek bir buton: " Sign in with Apple".  
2. **Onboarding \- Child Setup Screen:**  
   * Minimalist bir form. Çocuğun adı için geniş, kenarları yuvarlatılmış (border-radius: 12\) bir TextField.  
   * Doğum tarihi seçimi için standart iOS DatePicker (sadece ay/yıl yeterli olabilir).  
3. **Dashboard (Ana Ekran):**  
   * **Üst Bar:** Çocuğun adı ve avatarı. Yanında dropdown oku (birden fazla çocuk varsa geçiş için).  
   * **Kahraman Alanı (Hero):** 10, 25 veya 50 hedefine giden yatay, estetik bir Progress Bar. (Örn: "10. Kitaba son 3 kitap\!").  
   * **Son Okunanlar:** Yatayda kaydırılabilir (Horizontal Scroll), Apple-style gölgelendirmeli (soft shadow) kitap kapakları.  
   * **Floating Action Button (FAB):** Ortada büyük, dikkat çekici, üzerinde kamera/barkod ikonu olan "Kitap Ekle" butonu.  
4. **Scanner Screen (Kamera):**  
   * Tam ekran canlı kamera görüntüsü. Ortada sadece barkodu hizalamak için köşeli, ince çizgili bir vizör (viewfinder) alanı.  
   * Okuma gerçekleştiği an "Haptic Feedback" (telefonun hafif titreşmesi) ve başarılı okuma sesi.  
5. **Milestone Modal (Kritik Ekran \- Instagrammable):**  
   * Barkod okutulup baraj aşıldığında ekranın altından (Bottom Sheet) fırlayan kutlama ekranı.  
   * Ekranda Lottie tabanlı bir konfeti animasyonu ve ortada şık, cam efektli (glassmorphic) bir "Başarı Sertifikası / Rozet" görseli.  
   * Altında kocaman bir "Instagram Hikayelerinde Paylaş" butonu.

## **6\. USER STORIES & ACCEPTANCE CRITERIA (BACKLOG)**

### **EPIC 1: Kimlik Doğrulama ve Çocuk Profili**

**US 1.1 \- Apple ile Giriş**

* **Hikaye:** Bir ebeveyn olarak, şifre yaratmakla uğraşmamak için Apple Kimliğimle uygulamaya giriş yapabilmek istiyorum.  
* **Kabul Kriterleri (Acceptance Criteria):**  
  * **Given (Varsayalım ki):** Kullanıcı uygulamayı ilk kez açmıştır.  
  * **When (Eğer):** "Sign in with Apple" butonuna basarsa ve FaceID/TouchID onayını verirse;  
  * **Then (O zaman):** FastAPI tarafında token doğrulanmalı, Supabase'de users tablosunda kayıt yoksa oluşturulmalıdır.  
  * **And (Ve):** Kullanıcıya cihazda saklanacak bir JWT verilmeli ve kullanıcı "Çocuk Ekleme" (Eğer daha önce çocuk eklemediyse) ekranına yönlendirilmelidir.  
  * **Hata Durumu:** İnternet yoksa "Bağlantı hatası, lütfen tekrar deneyin" şeklinde native bir iOS uyarısı (UIAlertController) çıkmalıdır.

**US 1.2 \- İlk Çocuğu Ekleme**

* **Hikaye:** Sisteme giriş yaptıktan sonra, okuma verilerini takip edebilmek için çocuğumun adını ve yaşını eklemek istiyorum.  
* **Kabul Kriterleri:**  
  * **Given:** Kullanıcı giriş yapmış ama children tablosunda kaydı yoktur.  
  * **When:** İsim (min 2 karakter) ve Doğum Tarihi girip "Kaydet"e bastığında;  
  * **Then:** Bilgiler /api/v1/children endpoint'ine POST edilmeli.  
  * **And:** İşlem başarılıysa Dashboard (Ana Ekran) açılmalı ve üst kısımda çocuğun ismi görünmelidir.  
  * **Hata Durumu:** İsim alanı boş bırakılırsa "İsim alanı boş bırakılamaz" şeklinde inline bir kırmızı hata metni belirmelidir.

### **EPIC 2: Barkod Motoru**

**US 2.1 \- Barkod Tarama ve Kitap Ekleme**

* **Hikaye:** Kameramı kullanarak bir kitabın barkodunu saniyeler içinde okutmak ve kütüphaneye eklemek istiyorum.  
* **Kabul Kriterleri:**  
  * **Given:** Kullanıcı Dashboard'daki "+" butonuna basmıştır.  
  * **When:** Kamera açılır, kullanıcı kitabı vizöre ortalar ve AVFoundation barkodu (ISBN-10 veya ISBN-13) başarıyla yakalar;  
  * **Then:** Sistem otomatik olarak (butona basmaya gerek kalmadan) okunan kodu almalı, titreşim (haptic) ile bildirim vermeli.  
  * **And:** Ekranda "Kitap bulunuyor..." (activity indicator) görünmeli, /books/scan API'si çağrılmalı.  
  * **And:** API başarılı dönerse kitap kapak görseli ekranda görünmeli ve okuma kaydedilmelidir.  
  * **Fallback (B planı):** Eğer Google Books'ta kitap bulunamazsa, kullanıcı "Manuel Ekleme" formuna yönlendirilmelidir (Sadece Kitap Adı ve Yazar sorulur).

### **EPIC 3: Oyunlaştırma ve Paylaşım**

**US 3.1 \- Milestone Tetikleme ve Instagram Paylaşımı**

* **Hikaye:** Çocuğum 10\. kitabını bitirdiğinde şık bir sertifika görmek ve bunu Instagram Hikayemde paylaşmak istiyorum.  
* **Kabul Kriterleri:**  
  * **Given:** Çocuğun halihazırda 9 kitabı okunmuştur ve kullanıcı yeni bir barkod okutmuştur.  
  * **When:** /books/scan API'si "milestone\_unlocked": 10 yanıtını döndüğünde;  
  * **Then:** Barkod okuma ekranı kapanmalı ve doğrudan Milestone Modal (Lottie animasyonlu sertifika) ekranı açılmalıdır.  
  * **And:** Kullanıcı "Paylaş" butonuna bastığında, Swift kodu ilgili UIView'i bir UI Image olarak render etmeli (arkaplanda screenshot almalı).  
  * **And:** UIActivityViewController açılmalı ve cihazda yüklüyse "Instagram Stories" seçeneği gösterilmelidir.

## **7\. Kapsam Dışı (Out of Scope \- Faz 1 İçin)**

* Gelişmiş analitik, okuma süreleri, ısı haritaları.  
* İkinci ebeveyn (Anne-Baba) hesap eşleştirmesi veya aile içi ortak kütüphane.  
* Herhangi bir ödeme sistemi (In-App Purchase), Premium üyelik.  
* İkinci el kitap takas altyapısı.