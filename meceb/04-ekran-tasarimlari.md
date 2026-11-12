# Aşama 4 — Ekran Tasarımları

On önemli ekranın düşük sadakatli taslakları [wireframes/](wireframes/index.html) klasöründedir: bağımsız statik
HTML dosyalarıdır, tarayıcıda doğrudan açılır, üretim kodu değildir. **İçlerindeki tüm veriler, sayılar ve form
alanları örnektir**; özellikle pilot belgelerin form alanları henüz tanımlı değildir (AS-09).

Taslakların amacı görsel tasarım değil, **bilgi mimarisi ve etkileşimi** göstermektir: hangi ekranda ne var, hangi
öğe tanımdan (metadata) üretiliyor, hangi mevcut yapı taşı kullanılıyor.

## 1. Üç kullanıcı alanı

| Alan | Kitle | Yerleşim | Rota | Taslaklarda |
| --- | --- | --- | --- | --- |
| Portal | Vatandaş, firma, tesis yetkilisi | Üst menülü, sade, tek sütun ağırlıklı | `/portal/*` | 02, 03, 04, 05, 08 |
| Personel | Bakanlık personeli | Mevcut dikey Fuse kabuğu (sol menü) | `/workspace/*` | 01, 07, 09 |
| Yönetim | Tanım ve sistem yöneticisi | Aynı kabuk, "Tanımlar / Sistem" menü grupları | `/definition/*`, `/admin/*` | 06, 10 |

Tek SPA'dır; girişten sonra kullanıcı yetkisine göre uygun alana yönlendirilir. Menü mevcut `GetAuthorizedTree` ile
gelir. Portalın ayrı yerleşimi, başvuranı yönetim menüsü kalabalığından uzak tutmak içindir; Fuse'un yatay
yerleşimlerinden biri temel alınır (yeni kabuk yazılmaz).

**Portal üst çubuğundaki "işlem yapılan taraf" seçicisi** en önemli portal öğesidir: kullanıcı kendi adına mı, yetkili
olduğu bir firma/tesis adına mı işlem yaptığını burada görür ve değiştirir. Katalog, başvurular ve belgeler bu
seçime göre süzülür; seçim her istekte sunucuda doğrulanır.

## 2. Ekranlar

| # | Ekran | Taslak | Amaç | Tanımdan üretilen | Mevcut yapı taşı | Yeni bileşen |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Ana dashboard | [01](wireframes/01-dashboard.html) | Personelin işleri ve birim göstergeleri | — | `ng-apexcharts`, `FSearchBase` | Gösterge kartları |
| 2 | Belge kataloğu | [02](wireframes/02-belge-katalogu.html) | Başvurulabilecek belge türlerini bulma | Kategori ağacı, kartlar, etiketler | — | Katalog kartı, kategori süzgeci |
| 3 | Başvuru oluşturma | [03](wireframes/03-basvuru-olusturma.html) | Taraf seçimi ve uygunluk; sihirbazın ilk adımı | Adım listesi, uygunluk kontrolleri | `mat-stepper` (demo düzeyinde) | Başvuru sihirbazı (taslak kaydeden) |
| 4 | Dinamik form | [04](wireframes/04-dinamik-form.html) | Belgeye özel formun doldurulması | **Tamamı** (bölümler, alanlar, kurallar, ekler) | `mat-form-field`, tarih adaptörü | Form renderer'ı, dosya yükleme, tablo alanı |
| 5 | Başvuru detay | [05](wireframes/05-basvuru-detay.html) | Başvuranın durum takibi ve eksiklik giderme | Dışa görünen durumlar | — | Durum zaman çizelgesi, eksiklik paneli |
| 6 | İş akışı tasarımı | [06](wireframes/06-is-akisi-tasarim.html) | Adım ve geçişlerin tanımı, sürüm yayını | — (tanımın kendisi) | `form-dialog`, `@csb/diagrams` (önizleme) | Adım/geçiş düzenleyici, doğrulayıcı |
| 7 | Değerlendirme | [07](wireframes/07-degerlendirme.html) | İnceleme, eksiklik, onay/ret | Eylem düğmeleri, zorunlu açıklama/dosya | `@csb/pdfviewer` (ek önizleme) | Karar paneli, salt-okunur form görünümü |
| 8 | Belge detay | [08](wireframes/08-belge-detay.html) | Belgenin görüntülenmesi, doğrulama, yenileme | İzinli işlemler, yenileme penceresi | `@csb/pdfviewer`, `@csb/barcodegenerator` | Yaşam döngüsü çizelgesi |
| 9 | Belge yönetimi | [09](wireframes/09-belge-yonetimi.html) | Belgelerin listesi; askı, iptal, süre düzeltme | İzinli geçişler | `FSearchBase` + `@csb/grid` | Belge işlem paneli |
| 10 | Sistem yönetim paneli | [10](wireframes/10-sistem-yonetimi.html) | Belge türü tanımı ve yayını | — (tanımın kendisi) | Ürün detayındaki sekmeli kabuk kalıbı | Yayın kontrol listesi, sürüm karşılaştırma |

## 3. Tasarım kararları

**Dashboard (01).** Göstergeler kullanıcının birim ve belge türü kapsamıyla sınırlıdır; kapsam ekranda açıkça yazılır
ki rakamlar yanlış yorumlanmasın. Öncelik sırası: önce "benim işim" (bana atanan, geciken), sonra birim, sonra
belge. Başvuranın portalında dashboard yoktur; giriş sayfası "Başvurularım"dır.

**Katalog (02).** Kapsam dokümanındaki kademeli hizmet seçimi (ana alan → alt kırılım) sol sütundaki kategori
ağacıdır. Seçili taraf adına başvurulamayan türler gizlenmez, **neden başvurulamadığı açıklanarak** soluk gösterilir
(kullanıcı aradığı belgeyi bulup neden başvuramadığını anlar). Aktif belgesi olan tür için "Başvur" yerine "Belgeyi
gör" ve yenileme tarihi gösterilir.

**Başvuru sihirbazı (03–04).** Adımlar belge türü tanımından üretilir; ödeme ve imza adımları yalnızca tanımda
varsa görünür. Uygunluk kontrolleri ilk adımdadır: kullanıcı formu doldurduktan sonra değil, **başlamadan önce**
başvuramayacağını öğrenir (diyagramdaki sırayla aynı). Taslak her adım geçişinde ve belirli aralıkla kaydedilir.

**Dinamik form (04).** Taslak, şemadaki her alan tipinin nasıl göründüğünü gösterir: salt-okunur ön dolu alanlar
(kaynağı etiketli), seçim, tarih, sayı (hata durumuyla), çoklu seçim, koşullu alan, tekrarlanabilir tablo, dosya
(tarama durumuyla), beyan. Hata mesajı alanın altında, neyin yanlış olduğunu ve nasıl düzeltileceğini söyler.

**Başvuru detay (05).** Başvuran yalnızca sade durumları görür (kapsam dokümanındaki durum tablosu); kurum içi adım
adları, personel notları ve atanan kişi gösterilmez. Eksiklik varsa sayfanın en üstünde, son tarih ve kalan gün ile
birlikte tek bir çağrı olarak durur.

**İş akışı tasarımı (06).** Hedef mimarideki karar gereği (K-3) düzenleme tablo/form iledir; üstteki diyagram
tanımdan otomatik çizilen salt-okunur önizlemedir. "Yayınla" öncesi doğrulama hataları (ulaşılamayan adım, çıkışsız
adım, rolsüz adım) listelenir. Yayındaki sürümün kaç aktif başvurusu olduğu başlıkta görünür.

**Değerlendirme (07).** Sol tarafta incelenen içerik, sağ tarafta karar. Eylem düğmeleri o adımın geçişlerinden
üretilir; seçilen eyleme göre açıklama/dosya zorunluluğu değişir. Kimlik numarası maskelidir; açma eylemi yetkiye
bağlıdır ve kayda geçer. İşlem geçmişi her zaman görünür ve değiştirilemez.

**Belge detay (08) ve belge yönetimi (09).** Yenileme düğmesi tanımdaki pencere açılınca etkinleşir; etkin değilken
nedenini söyler. Askıya alma ve iptal tek tıkla yapılmaz: gerekçe → onay → üst yazı → Belgenet. Yalnızca o belge
türü için izinli ve kullanıcının yetkili olduğu işlemler görünür.

**Belge türü tanımı (10).** Nihai hedefin ("yönetici yeni belge türü tanımlar") ekranıdır. Sekmeler tanımın
parçalarıdır; üstteki **yayın kontrol listesi** eksik parçayı gösterir. Yayınlanan sürümün değişmezliği ve açık
başvuruların eski sürümle tamamlanacağı ekranda açıkça yazılır.

## 4. Ortak arayüz kuralları

- Mevcut bileşenler kullanılır: listeler `FSearchBase`, küçük formlar `FormDialogBase`, onaylar `CoreConfirmationService`, tarih `CoreLuxonDateAdapter`, çeviri `translate` pipe'ı.
- Sunucudan gelen her metin `cellRenderer`'larda `escapeHtml` ile kaçırılır; rozetler `grid-badge.utils` ile.
- Yetkisi olmayan düğme **gösterilmez** (`*authorize`); asıl kontrol backend'dedir.
- Geri alınamaz işlemler (gönder, onayla, reddet, iptal et) açık bir onay adımı ister ve sonucu aynı ekranda bildirir.
- Her liste boş durum, yükleniyor ve hata durumuna sahiptir; hata mesajı ne olduğunu ve ne yapılacağını söyler.
- Duyarlı yerleşim: portal ekranları telefon genişliğinde tek sütuna iner (kapsam dokümanındaki mobil uyum beklentisi; ayrı mobil uygulama sorusu AS-46).
- Erişilebilirlik: klavye ile gezinme, etiketli form alanları, renge ek olarak metinle durum (rozet metni); hedef düzey AS-48.
- Dil: arayüz metinleri lokalizasyon anahtarlarıyla (`ProjectName.xml`, `ProjectName-tr.xml`); yöneticinin girdiği belge adı ve form etiketleri için çok dillilik ihtiyacı ayrıca netleştirilmeli.

## 5. Taslaklarda bulunmayan ekranlar

Kapsam gereği taslağı çizilmeyen, geliştirme planında yer alan ekranlar: form tasarım ekranı, şablon yönetimi, ücret
tarifesi, bildirim kuralları, birim yönetimi, entegrasyon izleme (çağrı kayıtları, başarısız mesajlar), raporlar,
anonim belge doğrulama sayfası, iş listesi (liste görünümü), başvurularım / belgelerim listeleri.
