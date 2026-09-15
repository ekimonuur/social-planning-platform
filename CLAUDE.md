# Social Planning Platform — Proje Bağlamı

## Onur Hakkında
- 5 yıllık pure PHP developer, framework kullanmamış; Node.js'te de deneyimi var
- Laravel öğreniyor (sıfırdan) — CV'sinde Laravel'i güçlendirmek istiyor
- Hedef: profesyonel Backend Engineer seviyesi
- **Öncelik sırası: 1) öğrenmek, 2) ürünü tamamlamak.** Bu yüzden Laravel'in basit
  kavramları bile ilk kullanıldığında kısaca açıklanmalı (routing, middleware,
  Eloquent ilişkileri, form request vb. — "biliyordur" varsayılmasın).
- Çalışma tarzı: her teknik kararın "neden"ini anlamak istiyor
  - Neden bu teknoloji?
  - Alternatifi ne?
  - Büyük şirketler bunu nasıl çözüyor?
  - Daha ölçeklenebilir çözüm nasıl olur?
  - Performans ve güvenlik açısından dikkat edilmesi gerekenler?
- Bu proje aynı zamanda mülakatlarda anlatılabilecek bir case study olacak —
  önemli konularda "bu mülakatta nasıl sorulabilir?" notu eklenebilir.

## Proje Fikri
Arkadaş gruplarının ortak plan yapmasını sağlayan platform.
WhatsApp/Instagram DM'lerinde kaybolan fikirleri saklar, oylama yaptırır, etkinlik
oluşturur, katılım takibi yapar, hatırlatır ve geçmiş etkinlikleri (anı/fotoğraf)
arşivler.

Uzun vadeli döngü: **fikir → tartışma → karar → plan → etkinlik → anı**.
Sadece bir "event calendar" veya "to-do list" değil.

## Teknoloji Seçim Prensibi
> Bir teknoloji sırf öğrenilmek isteniyor diye projeye eklenmez. Her teknoloji
> seçimi gerçek bir problem üzerinden yapılır. Öğrenilmek istenen ama bu projenin
> doğal ihtiyacı olmayan teknolojiler (RabbitMQ, Kafka, Kubernetes, DynamoDB,
> Next.js SPA vb.) ayrı küçük "learning lab"lerde denenir, ana ürüne zorla
> sokulmaz.

Mimari yaklaşım: **modular monolith**. Laravel uygulaması içinde Auth/Users/
Groups/Events/Polls/Notifications gibi domain sınırları korunur; mikroservise
"daha profesyonel" diye erken geçilmez. Gereksiz Service/Repository/interface
katmanları eklenmez — kod "simple enough to understand, structured enough to
scale" olmalı.

## Teknik Mimari

### Aşama 1 (Şu An)
- Laravel + Livewire + Tailwind + **PostgreSQL** + Redis + Docker
- Redis/Queue/Realtime (Laravel Reverb) yalnızca gerçek bir ihtiyaç doğduğunda
  devreye alınır (sırf öğrenmek için erken eklenmez)

### Aşama 2
- REST API çıkar → React Native (Expo, TypeScript) mobil uygulama
- Next.js web SPA ana ürüne dahil değil; ayrı bir öğrenme lab'ı olarak ele alınabilir

### Aşama 3
- Spring Boot ile bağımsız servisler
- Python ile AI servisleri

### AWS & Deploy
- Geliştirme boyunca local Docker kullanılır.
- AWS (RDS, S3, CloudFront, ECS/Fargate, CloudWatch) yalnızca **Sprint 10
  (Docker & Deploy)** aşamasında, minimal ve süreli bir "production'a çıkarma"
  egzersizi olarak devreye alınır, sonra kapatılır — sürekli açık kaynak maliyeti
  riskinden kaçınılır.

## Geliştirme Metodu
- Küçük dikey feature'lar halinde ilerlenir (bkz. Sprint Planı), "big bang" yok.
- Yeni bir feature'da mümkünse sıra: (A) domain problemini anlat → (B) tasarımı
  anlat (entity/ilişki/data/authorization) → (C) gerekiyorsa alternatifleri
  karşılaştır → (D) küçük kararları Onur'a sor (örn. "etkinliğin sahibi kim
  olmalı?") → (E) birlikte implement et → (F) sonunda kısa "ne öğrendik" özeti.
- Kod review'da öncelik: security, N+1/query verimliliği, authorization,
  validation, Laravel convention'ları — ama gereksiz uzun rapor üretilmez.
- Debugging'de doğrudan çözüm verilmez; önce hata kaynağı birlikte bulunur
  (hipotez → test → çözüm → neden açıklaması), Onur açıkça hızlı çözüm istemedikçe.
- Kod değişikliğinden önce mevcut dosyalar/pattern'ler incelenir; gereksiz dosya
  oluşturulmaz, mevcut kod gereksiz yere değiştirilmez.

## İlk MVP Kapsamı
- **Auth:** register, login, logout, profil
- **Groups:** oluşturma, katılma, davet, üyeler
- **Events:** oluşturma, görüntüleme, düzenleme, silme, tarih/saat/konum/açıklama
- **Participation:** katılıyorum / kararsızım / gelemiyorum
- **Polls:** oylama oluşturma, oy verme, sonuç görme
- **Dashboard:** yaklaşan etkinlikler, aktif oylamalar, gruplar

MVP sonrası değerlendirilecekler (şimdi kapsam dışı): yorumlar, etkinlik chat'i,
wishlist, takvim entegrasyonu, push/email notification, fotoğraf galerisi,
arkadaşlık sistemi, grup rolleri, recurring events, masraf paylaşımı, AI önerileri.

## Sprint Planı
- [x] Proje kurulumu
- [ ] Sprint 1: Authentication
- [ ] Sprint 2: Grup sistemi
- [ ] Sprint 3: Etkinlikler
- [ ] Sprint 4: Oylamalar
- [ ] Sprint 5: Wishlist
- [ ] Sprint 6: Bildirimler
- [ ] Sprint 7: Queue ve Redis
- [ ] Sprint 8: API
- [ ] Sprint 9: Testler
- [ ] Sprint 10: Docker & Deploy (+ AWS deployment egzersizi)
- [ ] Sprint 11: Mobil uygulama
- [ ] Sprint 12: Java mikroservisleri

## Güncel Durum
**Tarih:** 2026-09-15
**Sprint:** Kurulum aşaması
**Son yapılan:** Proje kapsamı ve teknoloji kararları netleştirildi (PostgreSQL,
Livewire→API→React Native sırası, AWS'in deploy aşamasına ertelenmesi)
**Sıradaki adım:** Laravel kurulumu

## Alınan Kararlar
- `docs/decisions/` altında numaralı dosyalar olarak tutulacak

## Oturum Geçmişi
- `docs/sessions/` altında tarih bazlı dosyalar olarak tutulacak
- [2026-08-04](docs/sessions/2026-08-04.md) — İlk oturum, proje planı ve yapı kuruldu
