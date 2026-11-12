# MEÇEB — Sistem Analizi ve Mimari Tasarım

Merkezi (Çevre) Belgelendirme Yönetim Sistemi için mevcut durum analizi, hedef mimari, senaryolar, ekran taslakları
ve geliştirme planı. Bu klasördeki dokümanlar **tasarım önerisidir; kod değişikliği içermez**. Kritik mimari
kararlar onaylanmadan geliştirmeye başlanmamalıdır.

Hazırlanma tarihi: 12.11.2026 · Dayanak: bu repodaki CSB framework şablonu, `Belge_Matrisi_MEÇEP.xlsx`, süreç
diyagramları (`genel.png`, `sistem yöneticisi.png`) ve 09.11.2026 tarihli kapsam analizi dokümanı.

## Dokümanlar

| # | Doküman | İçerik |
| --- | --- | --- |
| 1 | [Mevcut durum analizi](01-mevcut-durum-analizi.md) | Framework envanteri, belge matrisi, belge türü × özellik matrisi, süreç diyagramları, ortak/farklı süreçler, kaynak çelişkileri |
| 2 | [Hedef mimari](02-hedef-mimari.md) | Genel mimari, katmanlar, modüller, veri modeli (ER), dinamik form, iş akışı, entegrasyon, yetkilendirme, belge üretimi, güvenlik, kararlar |
| 3 | [Senaryolar](03-senaryolar.md) | Pilot + E-Yeterlik, E-İzin, AATBEL, Sıfır Atık, ÇED, GBF, Firma ve Araç Lisansı |
| 4 | [Ekran tasarımları](04-ekran-tasarimlari.md) | On ekranın açıklaması · [taslaklar](wireframes/index.html) |
| 5 | [Geliştirme planı](05-gelistirme-plani.md) | Fazlar, modüller, bağımlılıklar, test ve kabul kriterleri, riskler |
| — | [Açık sorular](acik-sorular.md) | Netleştirilmesi gereken 48 soru, muhatap ve öncelikleriyle |

## Özet

**Framework.** Repo, ASP.NET Boilerplate türevi CSB 11 paketleri üzerinde .NET 9 + PostgreSQL + Angular 21 şablon
projesidir (klasik katmanlı; CQRS/MediatR yok). UÇBS SSO, rol/yetki, grid sorgulama ve denetim kaydı hazırdır.
İş akışı, dinamik form, dosya saklama, arka plan işi, bildirim ve birim bazlı veri yetkisi **yoktur**; bir kısmının
paketi yerel feed'de durmakta ancak bağlı değildir. README'ler kodla yer yer uyuşmamaktadır.

**Kaynaklar.** Excel'de 11 uygulama ve 16 belge satırı var; çoğu hücre boş, pilot belgelerin e-imza ve dağıtım
süreci "Soralım". Kapsam dokümanı tüm süreçlerin MEÇEB'e taşınmasını değil, **hibrit** bir yapıyı tarif ediyor
(bazı süreçlerde form ve inceleme alt uygulamada kalıyor); resmî sayılı ve imzalı belge **Belgenet**'te üretiliyor.

**Öneri.** Mevcut katmanlar içinde modüler monolit. Yöneticinin tanımladığı her şey (belge türü, form, iş akışı,
şablon, ücret) versiyonlu ve yayın sonrası değişmez; başvuru başladığı sürüme sabitlenir. Form için kompakt bir JSON
şeması ve sunucu tarafı doğrulama; iş akışı için BPMN motoru yerine durum/geçiş + görev tabloları; özel kurallar
adıyla seçilen kod genişletme noktalarında; entegrasyonlar port/adapter + outbox ile; her kayıt erişiminde birim ve
taraf kapsamı denetimi.

**Yol.** Önce şablonun MEÇEB projesine çevrilmesi ve altyapı eksikleri, sonra belge içeriğinden bağımsız çekirdek,
sonra pilot (Çevre Yetkilendirme Şubesi belgeleri). Pilotun başarı ölçütü: ikinci ve üçüncü belge türünün
**backend'e kod eklenmeden** yönetim ekranından tanımlanabilmesi.

## Hemen ele alınması gerekenler

1. **Git'te gizli anahtarlar.** `backend/src/CSB.ProjectName.Web.Host/appsettings.Test.json` depoda izleniyor ve
   gerçek görünen veritabanı şifresi, JWT anahtarı, şifreleme passphrase'i ve UÇBS servis bilgileri içeriyor.
   Değerler sızmış sayılıp değiştirilmeli (analiz §1.6, F-1).
2. **Yetki yükseltme açığı.** Rol ve yetki servisleri, çağıranın kendinde olmayan yetkiyi role eklemesini
   engellemiyor (F-2).
3. **Pilot için engelleyici sorular.** AS-07 … AS-14 (Çevre Yetkilendirme Şubesi) ve entegrasyon sözleşmeleri
   AS-30, AS-35, AS-36, AS-37, AS-41, AS-47.

## Onay bekleyen kritik kararlar

Ayrıntı ve alternatifler: [hedef mimari §16](02-hedef-mimari.md#16-onay-bekleyen-kritik-kararlar).

| No | Karar | Öneri |
| --- | --- | --- |
| K-1 | Mimari stil | Mevcut katmanlarda modüler monolit |
| K-2 | Form tanımı | Kendi kompakt JSON şeması + özel renderer |
| K-3 | İş akışı | Durum/geçiş + görev tabloları; görsel önizleme |
| K-4 | Başvuru verisi | `jsonb` + sorgulanan alanlar kolon |
| K-5 | İşletim modları | Yerel / hibrit / izleme |
| K-6 | Şablon biçimi | DOCX → PDF |
| K-7 | Resmî belge | Sayı, QR ve imza Belgenet'te |
| K-8 | Kiracılık | Tek kiracı |
| K-9 | Alt uygulamaya yönlendirme | Tek kullanımlık devir kodu (URL'de kimlik no ve oturum anahtarı taşınmaz) |
| K-10 | Token | Kısa ömür + yenileme + iptal |
| K-11 | Yerel parola girişi | Üretimde kapalı |
| K-12 | Hata yanıtları | Anlamlı HTTP kodları |
| K-13 | Arka plan işleri | `CSB.HangFire` |
| K-14 | Proje adı | Kesinleşen adla yeniden adlandırma |

## Sınırlar

- Framework kodu okunarak incelendi; uygulama **çalıştırılmadı** (yerelde `node_modules` kurulu değil, veritabanı
  yok). Çalışma zamanı davranışına dair çıkarımlar dokümanda "doğrulanmadı" diye işaretlidir.
- `@csb/*` paketlerinin yetenekleri tip tanımlarından ve demo sayfalarından okundu; denenmedi.
- Süreç diyagramındaki okların bir kısmı çözünürlük nedeniyle tek tek doğrulanamadı (AS-27).
- Süre ve efor tahmini verilmedi; gerekçesi geliştirme planının başındadır.
- Ekran taslaklarındaki tüm veriler ve form alanları örnektir.
