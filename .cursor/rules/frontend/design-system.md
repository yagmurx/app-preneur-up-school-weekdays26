**LMS**

**Design System v1.0**

LMS Platformu icin Kapsamli UI/UX Tasarim Rehberi

Bu dokuman, LMS ogrenme yonetim sistemi platformu icin gelistirilmis kapsamli tasarim sistemini icerir. Renk paleti, tipografi, spacing sistemi, component kutuphanesi ve UI kaliplari dahil olmak uzere tum tasarim standartlarini tanimlar.

| **Versiyon**    | v1.0 - Haziran 2025                           |
| --------------- | --------------------------------------------- |
| **Platform**    | Web (Responsive, Mobile-First)                |
| **Font Ailesi** | DM Sans (Display), DM Mono (Code)             |
| **Kapsam**      | Foundations, Components, Patterns, Guidelines |

Mobil-First Yaklasim: Tum componentler once kucuk ekranlar icin tasarlanmis, buyuk ekranlara progressif olarak guclendirilmistir.

Erisilebilirlik: WCAG 2.1 AA standartlarina uyumlu, minimum 4.5:1 kontrast orani zorunludur.

Token Bazli: Tum degerler CSS degiskenlerine baglidir; tema degisikligi tek noktadan yapilabilir.

# **Icerik**

# **1\. Foundations**

Foundations, tum tasarim kararlarinin uzerine insaatildigi temel tasarim ogelerini kapsar. Bu degerleri degistirmek tum platformu etkiler.

## **1.1 Renk Paleti**

5 marka renginden olusan palet; mavi interaktif elemanlar, lacivert yapici yuzeyler, yesil basari durumlarini temsil eder. Tum renkler WCAG AA kontrast gereksinimine uymalidir.

**MARKA RENKLERI**

| **Purple**<br><br>#A70978<br><br>_Brand / Accent_ | **Pink**<br><br>#F30E8C<br><br>_CTA / Highlight_ | **Blue**<br><br>#004CD3<br><br>_Interactive / Link_ | **Navy**<br><br>#002E4C<br><br>_Text / Sidebar_ | **Green**<br><br>#02C26C<br><br>_Success / Progress_ |
| ------------------------------------------------- | ------------------------------------------------ | --------------------------------------------------- | ----------------------------------------------- | ---------------------------------------------------- |

**ACIK TON VARYANTLARI**

| **Purple Light**<br><br>#F5E8F2<br><br>_Bg / Badge fill_ | **Pink Light**<br><br>#FDE8F4<br><br>_Bg / Badge fill_ | **Blue Light**<br><br>#E0EAFF<br><br>_Bg / Hover state_ | **Navy Light**<br><br>#E0E8EF<br><br>_Table header_ | **Green Light**<br><br>#D6F7E9<br><br>_Success bg_ |
| -------------------------------------------------------- | ------------------------------------------------------ | ------------------------------------------------------- | --------------------------------------------------- | -------------------------------------------------- |

**GRI SKALASI**

| **Gray 50**<br><br>#F7F7F8<br><br>_Page bg_ | **Gray 100**<br><br>#EEEEEF<br><br>_Borders_ | **Gray 200**<br><br>#D8D8DA<br><br>_Dividers_ | **Gray 500**<br><br>#6B6B72<br><br>_Muted text_ | **Gray 700**<br><br>#3A3A40<br><br>_Body text_ |
| ------------------------------------------- | -------------------------------------------- | --------------------------------------------- | ----------------------------------------------- | ---------------------------------------------- |

### **Renk Kullanim Kurallari**

- Birincil eylemler (kayit, satin alma, ilerleme) icin mavi (#004CD3) kullanin.
- Marka vurgulari ve ozel aksan noktalari icin mor (#A70978) kullanin.
- Tamamlanma, basari ve ilerleme gostergelerinde yesil (#02C26C) kullanin.
- Sidebar, navbar ve karanlik yuzeyler icin lacivert (#002E4C) kullanin.
- Metin icin en az 4.5:1 kontrast orani saglayin.
- Acik ton varyantlari yalnizca arka plan ve badge dolgusu icin kullanilmalidir.

## **1.2 Tipografi**

DM Sans; yuvarlak, modern ve okunabilir bir sans-serif font ailesidir. DM Mono ise teknik degerler, token isimleri ve kod gostertimi icin kullanilir.

**YAZI TIPI SISTEMI**

| **Stil**         | **Boyut / Agirlik** | **Renk** | **Ornek**                                |
| ---------------- | ------------------- | -------- | ---------------------------------------- |
| **Display / H1** | 40px 700 -1px       |          | Invest In Your Education                 |
| **Heading / H2** | 28px 700 -0.5px     |          | My Learning Dashboard                    |
| **Heading / H3** | 22px 700 -0.3px     |          | Course Progress Overview                 |
| **Subheading**   | 18px 600            |          | UX Design Fundamentals                   |
| **Body Large**   | 16px 400 1.6lh      |          | Lorem ipsum dummy text of printing...    |
| **Body Small**   | 14px 400 1.6lh      |          | 13.000+ Ogrenci -- Son guncelleme: 3 gun |
| **Label / OL**   | 11px 600 CAPS 1.5ls |          | IT & SOFTWARE -- MEDIA TRAINING          |
| **Code / Mono**  | 13px 400 DM Mono    |          | #004CD3 --color-primary                  |

## **1.3 Spacing Sistemi**

4px tabanlı bir spacing skalasi kullanilir. Tum margin, padding ve gap degerleri bu sistemin katları olmalidir. Bu yaklasim gorsel ritim ve tutarlilik saglar.

| **Token**      | **Deger** | **Kullanim**                                |
| -------------- | --------- | ------------------------------------------- |
| \--spacing-xs  | 4px       | Ikon ici araliklar, kompakt badge padding   |
| \--spacing-sm  | 8px       | Ikon-metin arasligi, liste ogesi ic boslugu |
| \--spacing-md  | 12px      | Card ic boslugu, form grup arasligi         |
| \--spacing-lg  | 16px      | Section boslugu, nav item padding           |
| \--spacing-xl  | 24px      | Card padding, modal ic alan                 |
| \--spacing-2xl | 32px      | Buyuk bolum arasligi, panel padding         |
| \--spacing-3xl | 48px      | Sayfa bolum arasligi                        |
| \--spacing-4xl | 64px      | Hero / sayfa ust boslugu                    |

### **Border Radius**

| **Token**      | **Deger** | **Kullanim**                 |
| -------------- | --------- | ---------------------------- |
| \--radius-sm   | 4px       | Kucuk badge, tag, ikon buton |
| \--radius-md   | 8px       | Input, select, kucuk kart    |
| \--radius-lg   | 12px      | Liste ogesi, orta boy kart   |
| \--radius-xl   | 16px      | Ana kart, panel, dropdown    |
| \--radius-2xl  | 24px      | Modal, sidebar, buyuk panel  |
| \--radius-full | 999px     | Tum butonlar, badge ve pill  |

### **Golge (Shadow) Sistemi**

| **Token**    | **Deger**                  | **Kullanim**           |
| ------------ | -------------------------- | ---------------------- |
| \--shadow-sm | 0 1px 4px rgba(navy,0.08)  | Kart, dropdown zemin   |
| \--shadow-md | 0 4px 16px rgba(navy,0.10) | Hover kart, sticky nav |
| \--shadow-lg | 0 8px 32px rgba(navy,0.13) | Modal, tooltip         |

# **2\. Components**

Tum componentler atom duzeyinden baslayarak olusturulmustur. Her component; kullanim kurallari, durum tanimlari ve eriselebilirlik gereksinimleri ile birlikte belgelenmistir.

## **2.1 Butonlar**

Butonlar bes varyant, iki boyut ve ikon destegi icerir. Tum butonlar minimum 44x44px dokunma hedef alanina sahip olmalidir (mobil-first gereksinimi).

| **Varyant**   | **Arka Plan** | **Yazi Rengi** | **Kullanim Durumu**                |
| ------------- | ------------- | -------------- | ---------------------------------- |
| **Primary**   | #004CD3       | #FFFFFF        | Ana eylem: Kayit, Satin Al, Baslat |
| **Purple**    | #A70978       | #FFFFFF        | Marka aksani: Sertifika, Premium   |
| **Green**     | #02C26C       | #FFFFFF        | Tamamlama, basari: Gonderildi      |
| **Secondary** | #FFFFFF       | #004CD3        | Ikincil: Onizle, Detay, Iptal      |
| **Ghost**     | #F4F6FB       | #3A3A40        | Ucuncu: Daha Fazla, Kapat          |
| **Icon**      | #F7F7F8       | #3A3A40        | Ikon-only: Arama, Bildirim, Ayar   |

Disabled durumu: opacity: 0.45, cursor: not-allowed, pointer-events: none

Hover durumu: background %15 koyulasir, translateY(-1px), shadow artar

Focus durumu: 3px outline, renk = buton renginin %20 alpha degeri

Loading durumu: spinner ikonu eklenir, metin gizlenir, boyutlar sabit kalir

## **2.2 Badge ve Etiketler**

Badge'ler kategori, durum ve ozellik gostertimi icin kullanilir. Iki tip vardir: filled (dolu) ve outlined (cerceveli).

| **Varyant** | **Arka Plan** | **Yazi Rengi** | **Kullanim**              |
| ----------- | ------------- | -------------- | ------------------------- |
| **Purple**  | #F5E8F2       | #A70978        | IT & Software kategorisi  |
| **Pink**    | #FDE8F4       | #A70978        | Media Training kategorisi |
| **Blue**    | #E0EAFF       | #004CD3        | Devam Ediyor, interaktif  |
| **Green**   | #D6F7E9       | #017A43        | Tamamlandi, Basarili      |
| **Navy**    | #E0E8EF       | #002E4C        | Yeni, Onerilir            |

## **2.3 Form Elemanlari**

Form elemanlari label, input, hint ve durum mesajlarindan olusur. Her input minimum 48px yuksekliginde olmali ve touch-friendly olmalidir.

| **Varsayilan**   | Gri cerceve (#D8D8DA), beyaz arka plan, gri placeholder |
| ---------------- | ------------------------------------------------------- |
| **Focus**        | Mavi cerceve (#004CD3), 3px mavi outline golgesi        |
| **Hata (Error)** | Kirmizi cerceve (#E24B4A), hata mesaji altta kirmizi    |
| **Basari (OK)**  | Yesil cerceve (#02C26C), onay ikon ve mesaj             |
| **Disabled**     | Gri arka plan (#F7F7F8), opacity: 0.6, kilitli ikon     |

Input yuksekligi: min 48px (mobil), 44px (desktop)

Label: 13px, 600 weight, lacivert (#002E4C)

Placeholder: gri (#B0B0B4)

Hint metni: 12px, normal weight, altta, duruma gore renkli

Icon padding: sol icon icin padding-left: 44px uygulanir

## **2.4 Kurs Kartlari**

Kurs kartlari uc renk aksani ile gelir; mavi (IT), mor (Media), yesil (Business). Her kart ust sinirda 3px renkli accent bar icerir.

| **Kart Yapisi**   | Header tag \| Baslik \| Aciklama \| Progress bar \| Footer (ogrenci sayisi + avatar) |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Padding**       | 20px yatay, 20px dikey (--spacing-xl)                                                |
| **Border radius** | 16px (--radius-xl)                                                                   |
| **Golge**         | Varsayilan: shadow-sm \| Hover: shadow-md + translateY(-2px)                         |
| **Progress bar**  | 4px yukseklik, renk = kart aksani, arka plan gray-100                                |
| **Avatar stack**  | Kucuk avatarlar -10px margin-left ile ust uste gelir                                 |
| **Rating**        | Sari yildiz ikonu + puan degeri, ust sag kosede badge                                |

## **2.5 Avatar Sistemi**

Dort boyut: XL (profil sayfasi), L (kart baslik), M (liste), S (yiginlama). Renk varyantlari marka paletiyle eslesmektedir.

| **Boyut** | **Olcek** | **Font** | **Kullanim**                   |
| --------- | --------- | -------- | ------------------------------ |
| **XL**    | 56px      | 18px     | Profil sayfasi, hesap ayarlari |
| **L**     | 44px      | 15px     | Kart basligi, yorum yazari     |
| **M**     | 36px      | 13px     | Liste ogesi, bildirimler       |
| **S**     | 28px      | 11px     | Avatar yiginlama, mini profil  |

## **2.6 Uyari ve Bildirimler**

Dort semantik durum: bilgi (mavi), basari (yesil), uyari (sari), hata (kirmizi). Sol kenarda kalin 4px border ile guclendirilmis renk kodlamasi.

| **Tip**    | **Arka Plan** | **Cerceve** | **Ornek Metin**                    |
| ---------- | ------------- | ----------- | ---------------------------------- |
| **Bilgi**  |               |             | Kurs materyalleri guncellendi.     |
| **Basari** |               |             | Kursu basariyla tamamladiniz!      |
| **Uyari**  |               |             | Aboneliginiz 3 gun icinde bitiyor. |
| **Hata**   |               |             | Odeme islemi gerceklestirilemedi.  |

# **3\. UI Kaliplari (Patterns)**

Kaliplar, birden fazla component'in bir araya gelerek olusturduğu tekrar eden duzen ve etkilesim yapilaridir. Butun sayfalarda tutarli uygulanmalidir.

## **3.1 Navigasyon Yapisi**

Platform iki seviyeli navigasyon kullanir: ust bar (global) ve sol sidebar (bolum ici). Mobil'de sidebar alt tab bara donusur.

| **Ust Bar**         | Logo \| Global nav linkleri \| Bildirim \| Profil avatari. Yukseklik: 60px. Arkaplan: lacivert (#002E4C). |
| ------------------- | --------------------------------------------------------------------------------------------------------- |
| **Sol Sidebar**     | Logo \| Ikon navigasyon \| Profil. Genislik: 60px (collapsed) / 220px (expanded). Dark lacivert.          |
| **Aktif Durum**     | Ikon: yesil renk (#02C26C) + arka plan glow. Sidebar'da sol 4px yesil bant.                               |
| **Mobil (<768px)**  | Sidebar gizlenir. Alt tab bar 5 ikon gosterir. Hamburger menu tam ekran paneli acar.                      |
| **Tab Navigasyonu** | Kurs detay ve dashboard ici sekmeler. Pill style, aktif sekme beyaz kart + golge.                         |

## **3.2 Kurs Listeleme ve Filtreleme**

Kurslar kart grid'inde listelenir. Filtre taglari (chip) ile kategoriye gore sugulanir. Aktif filtre maviye doner.

| **Grid Yapisi**     | Desktop: 3 sutun. Tablet (768-1024px): 2 sutun. Mobil (<768px): 1 sutun. |
| ------------------- | ------------------------------------------------------------------------ |
| **Filtre Siralama** | Aktif filtre ilk sirada, sonra alfabe sirasi                             |
| **Bos Durum**       | Uygun kurs bulunamazsa: illustrasyon + "Farkli filtre deneyin" mesaji    |
| **Yukleme Durumu**  | Kart iskelet animasyonu (shimmer effect), 3 adet                         |

## **3.3 Kurs Detay Sayfasi**

Video oynatici + ders listesi + materyal bolumu. Sol panel video/icerik, sag panel kurs mufredati. Mobil'de tek sutun, mudredat alttan acilir.

| **Ust Alan**     | Kurs basligi, kategori badge, ogretmen avatar, rating, ogrenci sayisi                 |
| ---------------- | ------------------------------------------------------------------------------------- |
| **Video Player** | Ozel player, 16:9 oran, alt bar: oynat/duraklat, ilerleme, ses, tam ekran             |
| **Ders Listesi** | Tamamlanan dersler: yesil check. Aktif ders: mavi vurgu. Kilitli dersler: gri + kilit |
| **Materyaller**  | Dosya tipi ikonu, dosya adi, boyut bilgisi, indirme butonu                            |
| **Ilerleme Bar** | Ust kismda sabit, tamamlanma yuzdesi ve ders sayaci                                   |

## **3.4 Dashboard / Ana Sayfa**

Kullanicinin tum ogrenme aktivitesinin ozeti. Stat kartlari, devam eden kurslar ve yakin etkinlikler icerir.

| **Stat Kartlari**      | 4 adet: Toplam Kurs, Tamamlanan, Ogrenme Suresi, Sertifikalar. 2x2 grid. |
| ---------------------- | ------------------------------------------------------------------------ |
| **Devam Eden Kurslar** | Son 3 kurs, progress bar ile. "Tum kurslar" linki.                       |
| **Aktivite Grafigi**   | Son 7 gun ogrenme suresi, cizgi grafik, yesil renk                       |
| **Yakin Etkinlikler**  | Canli ders ve son teslim tarihleri, takvim ikonu ile                     |

## **3.5 Modal ve Overlay Kaliplari**

| **Kayit Modal** | Kurs baslik + kategori badge + aciklama + Kayit / Iptal butonlari             |
| --------------- | ----------------------------------------------------------------------------- |
| **Onay Modal**  | Uyari ikon + soru metni + Onay (kirmizi/mavi) / Vazgec butonlari              |
| **Form Modal**  | Tam form icerigi, scroll destekli, sabit alt buton bar                        |
| **Overlay**     | Background: rgba(0,46,76,0.45). Esc ile kapanir. Arka plana tiklamak kapatir. |
| **Animasyon**   | Acilis: scale(0.95) + opacity 0 -> 1, 200ms ease-out. Kapanis: 150ms ease-in. |

# **4\. Design Token Referansi**

Tum CSS degiskenleri asagida listelenm istir. Bu tokenlar kullanilarak theme degisikligi merkezi bir noktadan yonetilebilir.

## **4.1 Renk Tokenlari**

| **Token**               | **Deger** | **Kullanim**                             |
| ----------------------- | --------- | ---------------------------------------- |
| \--color-primary        | #004CD3   | Ana buton, link, aktif durum, focus ring |
| \--color-brand          | #A70978   | Marka vurgusu, aksan noktalar            |
| \--color-accent         | #F30E8C   | CTA, ozel promosyon, highlight           |
| \--color-surface        | #002E4C   | Sidebar, navbar, dark yuzeyler           |
| \--color-success        | #02C26C   | Tamamlanma, basari, ilerleme             |
| \--color-primary-light  | #E0EAFF   | Buton hover bg, bilgi kutusu             |
| \--color-brand-light    | #F5E8F2   | Badge fill, tag bg                       |
| \--color-success-light  | #D6F7E9   | Basari mesaj bg                          |
| \--color-text-primary   | #141418   | Ana basliklar                            |
| \--color-text-secondary | #3A3A40   | Govde metni                              |
| \--color-text-muted     | #6B6B72   | Yardimci metin, placeholder              |
| \--color-border         | #D8D8DA   | Kart, input siniri                       |
| \--color-bg-page        | #F4F6FB   | Sayfa arka plani                         |
| \--color-bg-card        | #FFFFFF   | Kart ve panel arka plani                 |

## **4.2 Tipografi Tokenlari**

| **Token**       | **Deger**             | **Kullanim**               |
| --------------- | --------------------- | -------------------------- |
| \--font-display | 'DM Sans', sans-serif | Tum metin icerigi          |
| \--font-mono    | 'DM Mono', monospace  | Kod, token, teknik deger   |
| \--text-display | 40px / 700 / -1px     | H1, hero basligi           |
| \--text-heading | 28px / 700 / -0.5px   | H2, bolum basligi          |
| \--text-subhead | 22px / 700 / -0.3px   | H3, kart basligi           |
| \--text-body-lg | 16px / 400 / 1.6      | Ana govde metni            |
| \--text-body    | 14px / 400 / 1.6      | Ikincil metin, meta        |
| \--text-label   | 11px / 600 / 1.5ls    | Overline, kategori etiketi |

## **4.3 Etkilesim Tokenlari**

| **Token**          | **Deger**        | **Kullanim**                    |
| ------------------ | ---------------- | ------------------------------- |
| \--transition-fast | 150ms ease-in    | Kapanis, focus kaybetme         |
| \--transition-base | 200ms ease-out   | Acilis, hover, aktif durum      |
| \--transition-slow | 300ms ease       | Sayfa gecisi, modal             |
| \--focus-ring      | 0 0 0 3px alpha  | Klavye navigasyon focus halkasi |
| \--hover-lift      | translateY(-2px) | Kart hover efekti               |

# **5\. Eriselebilirlik ve Responsive**

## **5.1 Eriselebilirlik Kurallari**

- Kontrast orani: Normal metin icin minimum 4.5:1, buyuk metin icin 3:1 (WCAG 2.1 AA).
- Klavye navigasyonu: Tum interaktif elementler Tab ile ulasilabilir olmalidir.
- Focus gostergesi: Mavi focus ring (3px, %20 alpha), hicbir zaman gizlenmemeli.
- Ekran okuyucu: Anlamli alt metinler, aria-label, aria-describedby kullanilmalidir.
- Animasyonlar: prefers-reduced-motion medya sorgusu dikkate alinmalidir.
- Renk bagimliliktan kacin: Durumu rengin yaninda sekil veya metin ile de belirtin.
- Minimum dokunma alani: 44x44px (Apple), 48x48px (Google Material) standartlari.
- Hata mesajlari: Yalnizca renk ile degil, aciklayici metinle de desteklenmeli.

## **5.2 Responsive Breakpoint'ler**

| **Token**      | **Deger**   | **Kullanim**                               |
| -------------- | ----------- | ------------------------------------------ |
| xs (Telefon)   | < 480px     | Tek sutun, bottom nav, buyuk dokunma alani |
| sm (Telefon-L) | 480-767px   | Tek sutun, genisletilmis padding           |
| md (Tablet)    | 768-1023px  | 2 sutun grid, sidebar collapse             |
| lg (Desktop)   | 1024-1279px | 3 sutun grid, sidebar acik                 |
| xl (Genis)     | \>= 1280px  | 3+ sutun, max-width: 1400px                |

## **5.3 Mobil-First Yaklasim**

Tasarim once en kucuk ekran icin yaplir, sonra buyuk ekranlara genisletilir. Bu yaklasim performansi arttirir ve kullanici deneyimini onceliklendirir.

CSS: Once base stiller yaz, sonra @media (min-width: ...) ile genislet.

Grid: grid-template-columns: 1fr; baslat, md+ icin repeat(2, 1fr), lg+ icin repeat(3, 1fr) ekle.

Resimler: width: 100%; max-width: 100%; overflow: hidden;

Font boyutu: Mobil 14-16px, desktop 16-18px (clamp() kullanilabilir).

Sidebar: Mobilde gizli (off-canvas), tablet ve ustunde gorunur.

# **6\. Uygulama Rehberi**

## **6.1 CSS Degisken Kurulumu**

Asagidaki token tanimlari projenizin kok :root blogunun icerigini olusturmalidir. Tum komponent stilleri bu degerlere referans vermeli; hicbir zaman direkt hex kodu kullanilmamalidir.

:root {

\--color-primary: #004CD3;

\--color-brand: #A70978;

\--color-accent: #F30E8C;

\--color-surface: #002E4C;

\--color-success: #02C26C;

\--color-text-primary: #141418;

\--color-text-muted: #6B6B72;

\--color-bg-page: #F4F6FB;

\--color-bg-card: #FFFFFF;

\--font-display: "DM Sans", sans-serif;

\--font-mono: "DM Mono", monospace;

\--radius-card: 16px;

\--radius-btn: 999px;

\--shadow-md: 0 4px 16px rgba(0,46,76,0.10);

}

## **6.2 Component Hiyerarsisi**

Komponentler uc katmanda organize edilmistir: Atomlar (temel elementler), Molekuller (birlesik elementler) ve Organizmalar (sayfa bolmeleri).

| **Atomlar**      | Button, Badge, Avatar, Input, Tag, Progress, Alert - Temel yapı tasları |
| ---------------- | ----------------------------------------------------------------------- |
| **Molekuller**   | Card, Form Group, Search Bar, Tab Bar - Atomlardan olusan bilesimler    |
| **Organizmalar** | Sidebar Nav, Course Grid, Dashboard, Modal - Tam sayfa bolmeleri        |
| **Sayfalar**     | Dashboard, Course Detail, Profile, Settings - Tam sayfa sablonlar       |

## **6.3 Yapilanma Kontrol Listesi**

Her yeni component veya sayfa tasariminda asagidaki kontrol listesini kullanin:

- Renk tokenlari kullaniliyor mu? (hicbir direkt hex kodu olmamali)
- Mobil goruntumu test edildi mi? (320px minimum)
- Klavye navigasyonu calisıyor mu?
- Focus durumlari gorunur mu?
- Bos durum tasarimi mevcut mu? (no-content state)
- Yukleme durumu tasarimi mevcut mu? (loading/skeleton)
- Hata durumu tasarimi mevcut mu?
- Renk kontrast orani kontrol edildi mi? (min 4.5:1)
- Touch hedef alanlari yeterli mi? (min 44px)
- Animasyonlar prefers-reduced-motion'a duyarli mi?

**LMS Design System v1.0**

Haziran 2025 - Dahili Kullanim Icin