# Açık Sorular ve Netleştirilecek Gereksinimler

Kaynaklarda boş, belirsiz, "Soralım" olarak işaretli veya birbiriyle çelişen her nokta burada tek tek listelenir.
Hiçbiri varsayımla kapatılmamıştır. "Etki" sütunu, yanıt gelmeden hangi tasarım/geliştirme kaleminin
kesinleşemeyeceğini gösterir. Hücre başvuruları `Belge_Matrisi_MEÇEP.xlsx` → "Belge Matrisi" sayfasına aittir.

Öncelik: **P** = pilot için engelleyici, **M** = mimari kararı etkiler, **S** = ilgili belge türü eklenirken gerekir.

## A. Kapsam ve yön

| No | Soru | Kaynak | Muhatap | Öncelik | Etki |
| --- | --- | --- | --- | --- | --- |
| AS-01 | Her belge türü hangi işletim modunda çalışacak (yerel / hibrit / izleme)? İstek tüm yaşam döngüsünün MEÇEB'de olmasını, kapsam dokümanı hibrit yapıyı tarif ediyor. | İstek §1–2; doküman §2, §3 | Proje yönetimi | M | Entegrasyon yükü, modül öncelikleri |
| AS-02 | Sistemin resmî adı ve kısaltması nedir (MEÇEB / MEÇEP / MCBS)? | Ç-1 | Proje yönetimi | S | Proje adlandırması (`CSB.ProjectName` → ?) |
| AS-03 | Kimlik doğrulama yalnızca UÇBS SSO mu, yoksa e-Devlet doğrulaması ayrı bir adım mı? e-Devlet UÇBS'nin içinden mi geçiyor? | Ç-2; diyagram | UÇBS ekibi | M | Kimlik modülü |
| AS-04 | Belgenin kalıcı arşivi nerede: MEÇEB mi, alt uygulama mı? "Geçici arşiv süresi" ne kadar? | Ç-9; diyagram | Proje yönetimi, alt uygulama sahipleri | M | Depolama boyutlandırması, saklama politikası |
| AS-05 | Alt uygulamalardaki mevcut geçerli belgeler MEÇEB'e aktarılacak mı (doğrulama, yenileme, süre takibi için)? | — | Proje yönetimi | M | Veri göçü işi, belge modeli |
| AS-06 | "Atık Yönetim Uygulaması" kapsamda mı? Excel'de var, dokümanın sonundaki kapsam dışı listesinde "AYD" geçiyor. | Ç-8; satır 10 | Proje yönetimi | S | B09 |

## B. Pilot — Çevre Yetkilendirme Şubesi (B05–B07)

| No | Soru | Kaynak | Muhatap | Öncelik | Etki |
| --- | --- | --- | --- | --- | --- |
| AS-07 | Başvuran e-imzası gerekli mi? | J6, J7, J8 = "Soralım" | Çevre Yetkilendirme Şubesi | P | İş akışı tanımı |
| AS-08 | Başvuru dağıtım süreci ve onay makamı nedir (merkez/taşra, şube müdürü/daire başkanı)? | K6, K7, K8 = "Soralım" | Çevre Yetkilendirme Şubesi | P | İş akışı tanımı, atama kuralı |
| AS-09 | Üç belgenin başvuru formu alanları ve istenen ekler nelerdir? Dayanak mevzuat hangisi? | I6–I8, F6–F8 boş | Çevre Yetkilendirme Şubesi | P | Form tanımları |
| AS-10 | Çıktı yalnızca "üst yazı" mı? Ayrı bir yeterlik belgesi basılıyor mu? | M6–M8 = "Üst Yazı" | Çevre Yetkilendirme Şubesi | P | Şablonlar |
| AS-11 | Ücret kalem kodları ve tutarlar; yenilemede ücret farklı mı? | H6–H8 = "Var" | Döner Sermaye, Şube | P | Ücret tanımı |
| AS-12 | Başvuru sahibi tesis mi, firma mı? "Araç takip servis sağlayıcı" bir tesis olarak mı kayıtlı? | A6 "Tesis"; D6 "Tesis-Bakanlık" | Şube, UÇBS ekibi | P | Taraf modeli |
| AS-13 | Yenileme, askıya alma ve iptal koşulları; yenileme başvurusu süre bitiminden ne kadar önce açılır? | N6–N8 (5/5/4 yıl) | Şube | P | Yaşam döngüsü kuralları |
| AS-14 | Bugün bu süreç nasıl yürüyor (kâğıt, e-posta, Belgenet)? Geçerli belgelerin listesi var mı? | Doküman: "mevcutta yazılımı bulunmayan" | Şube | P | Göç, kabul kriterleri |

## C. Excel'de boş bırakılan hücreler

| No | Soru | Hücre | Muhatap | Öncelik |
| --- | --- | --- | --- | --- |
| AS-15 | Firma Araç Lisanslandırma: ödeme, e-imza, dağıtım süreci ve belge süresi nedir? | H10, J10, K10, N10 | Atık Yönetimi | S |
| AS-16 | İthalat-İhracat "İzin" ve "Belge" satırları iki ayrı belge türü mü? "Belge" tam olarak nedir? | C11, C12 | İthalat-İhracat | S |
| AS-17 | İthalat-İhracat: e-imza ve dağıtım süreci; "süre sonu manuel değiştiriliyor" kuralı kim tarafından, hangi koşulda uygulanıyor? | J11–K12, N11–N12 | İthalat-İhracat | S |
| AS-18 | AAT Belgesi: e-imza ve dağıtım süreci; "AAT Kimlik Belgesi" çıktısının içeriği | J16, K16 | Atıksu | S |
| AS-19 | ÇED Olumlu: ödeme, e-imza, dağıtım süreci. 18. satırda yalnızca "Süresiz" var — ikinci bir belge mi kastediliyor? | H17, J17, K17, N18 | ÇED | S |
| AS-20 | "Talep Edilen Belge", "Entegrasyonlar", "Veri Giriş Formu" sütunları 16 satırın 14'ünde boş. Her belge için doldurulabilir mi? | F, G, I sütunları | Tüm birimler | S |
| AS-21 | "Uygulama Servis" sütunundaki "Başvuru durum ve süreç kontrolü" hangi servisleri kastediyor (mevcut mu, yazılacak mı)? | L11, L14, L17 | Alt uygulama ekipleri | S |
| AS-22 | "E-İmza/Vatandaş" sütunu neyi ölçüyor: başvuranın e-imzası mı, belgenin e-imzalı olması mı? | J sütunu başlığı | Analiz ekibi | M |
| AS-23 | "Alt Uygulama Durumu = Var/Yok" tam olarak ne demek: çalışan bir yazılım var mı, yoksa belge altında alt kırılım var mı? ("Kaynak Hücreler" sayfasında ayrıca "Belge Alt Kırılım" sütunu var.) | E sütunu | Analiz ekibi | M |
| AS-24 | E-İzin "Şahıs" grubunda; kapsam dokümanı tesis diyor. Belge sahibi kim? | A3 (Ç-4) | E-İzin | S |
| AS-25 | AATBEL "Çıktı yok – olumlu/olumsuz durumu" ama süre "1 yıl". Belge üretilmiyorsa süren şey nedir? | M4, N4 | AATBEL | S |
| AS-26 | GBF iki satırda "Yeni analiz yapılacak" notlu; analiz ne zaman, MEÇEB'e dahil mi? | C13, C19 | GBF | S |

## D. Diyagramlar ve kapsam dokümanı

| No | Soru | Kaynak | Muhatap | Öncelik |
| --- | --- | --- | --- | --- |
| AS-27 | `genel.png` içindeki okların bir kısmı çözünürlük nedeniyle tek tek doğrulanamadı; düzenlenebilir kaynak dosya (draw.io/Figma) paylaşılabilir mi? | Diyagram | Analiz ekibi | S |
| AS-28 | Yardım merkezi ve "Bana Sor" sohbet robotu MEÇEB kapsamında mı? Hangi fazda? | `sistem yöneticisi.png` | Proje yönetimi | S |
| AS-29 | KVKK maskeleme kurallarının arayüzden yönetimi bekleniyor mu, yoksa sabit kurallar yeterli mi? | `sistem yöneticisi.png` | BT güvenlik, KVKK birimi | M |
| AS-30 | UÇBS hangi servisleri sağlıyor: kullanıcı tipi, yetkili olunan firma/tesis listesi, vekâlet doğrulama, İK birim ağacı, tesis adres/NACE, tesisin aktif izinleri? Sözleşmeleri nedir? | Doküman WBS; kod incelemesi | UÇBS ekibi | **P** |
| AS-31 | YÖK ve SGK/KHK sorguları hangi belge türlerinde zorunlu? Sorguyu MEÇEB mi yapar, alt uygulama API'si mi? Hukuki dayanak ve veri paylaşım protokolü var mı? | Ç-7; doküman §3.1 | Hukuk, ilgili birimler | M |
| AS-32 | Sıfır Atık: MEÇEB'de toplanacak "ilave ek belgeler" nelerdir? (Dokümanda "İLAVE EK BELGELER NELER?" notu var.) İptal sonrası gösterilecek uyarı metni nedir? ("Uyarı metni?" notu) | Doküman §3.1 | Sıfır Atık | S |
| AS-33 | Eksiklik bildirimi kaç tur? Her turun süresi ne? Süre aşımında otomatik iptal tüm belge türlerinde mi? | Doküman durum tablosu ("1. tur", "2. tur") | Tüm birimler | M |
| AS-34 | Sistem tek kurum (tek kiracı) olarak mı çalışacak? Framework'te çoklu kiracılık açık. | Kod incelemesi (F-9) | Proje yönetimi, framework ekibi | M |

## E. Entegrasyonlar

| No | Soru | Muhatap | Öncelik |
| --- | --- | --- | --- |
| AS-35 | **Belgenet**: taslak evrak gönderme, imza akışı başlatma, sayı/barkod/QR ve imzalı PDF alma servisleri mevcut mu? Senkron mu, geri çağrı mı? Şablon Belgenet'te mi tutulur, MEÇEB'de mi? | Belgenet ekibi | **P** |
| AS-36 | Hiyerarşik onay hem MEÇEB'de hem Belgenet'te mi yürüyecek? (Doküman "Belgenet ve MEÇEB üzerinden… denetler" diyor.) Çift onay istenmiyorsa hangisi esas? | Belgenet ekibi, birimler | **P** |
| AS-37 | **Döner sermaye**: referans no üretimi, ödeme sayfasına yönlendirme, sonuç bildirimi (geri çağrı/sorgu), iade/iptal servisleri; sanal POS'u kim işletiyor? | Döner Sermaye İşletmesi | **P** |
| AS-38 | Başvuranın e-imza/mobil imzası için kurumun kullandığı altyapı hangisi? (Repoda yerel imza aracına bağlanan bir bileşen var; lisansı ve kullanılabilirliği teyit edilmeli.) | BT, framework ekibi | M |
| AS-39 | Belge doğrulama: QR kodu Belgenet'in doğrulama sayfasına mı, MEÇEB'in doğrulama sayfasına mı gidecek? | Belgenet ekibi | M |
| AS-40 | SMS ve e-posta için kurumsal servis hangisi? | BT | S |
| AS-41 | Dosya saklama: S3 uyumlu kurumsal nesne deposu var mı? Antivirüs taraması için kurumsal servis (ICAP/ClamAV vb.) var mı? | BT altyapı | **P** |
| AS-42 | Alt uygulamalarla çift yönlü entegrasyonda (Sıfır Atık, İthalat, E-İzin, ÇED) servisleri kim yazacak, takvimi nedir? | Alt uygulama ekipleri | S |

## F. Kurumsal ve işletimsel

| No | Soru | Muhatap | Öncelik |
| --- | --- | --- | --- |
| AS-43 | Beklenen hacim: yıllık başvuru sayısı, eş zamanlı kullanıcı, ek dosya boyut/adet sınırları | Birimler, BT | M |
| AS-44 | Başvuru, belge ve kişisel veri saklama süreleri; silme/anonimleştirme kuralları | Hukuk, KVKK birimi | M |
| AS-45 | Yedekleme ve felaket kurtarma hedefleri (RPO/RTO); kurumsal log toplama (SIEM) altyapısı | BT altyapı, BT güvenlik | M |
| AS-46 | Mobil uyumluluk beklentisi duyarlı web arayüzü müdür, yoksa ayrı mobil uygulama mı? | Proje yönetimi | S |
| AS-47 | Framework ekibi `CSB.HangFire` / `CSB.BlobStoring` / `CSB.MailKit` paketlerini destekliyor mu; S3 sağlayıcısı ekleyebilir mi? | Framework ekibi | **P** |
| AS-48 | Erişilebilirlik ve kurumsal arayüz standartları (kurumsal kimlik, WCAG düzeyi) | Kurumsal iletişim, BT | S |
