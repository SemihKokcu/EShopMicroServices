# E-Shop Microservices

---
**Not:** Bu proje, [Mehmet Özkaya](https://github.com/aspnetrun/microservices](https://github.com/mehmetozkaya/EShopMicroservices) GitHub reposundan ilham alınarak ve eğitim amaçlı olarak geliştirilmektedir.
---

Bu proje, .NET üzerinde geliştirilmiş, mikroservis mimarisine dayalı bir e-ticaret platformu uygulamasıdır. 

## Mimari ve Tasarım Prensipleri

Bu proje, sadece çalışan bir sistem oluşturmayı değil, aynı zamanda kaliteli ve sürdürülebilir kod yazma pratiğini de hedefler. Bu doğrultuda aşağıdaki mimari yaklaşımlar ve tasarım prensipleri benimsenmiştir:

-   **Katmanlı ve Altıgen Mimari (N-Layer Hexagonal):** Proje; Core, Application, Infrastructure ve Presentation katmanlarından oluşan, DDD (Domain-Driven Design) pratikleriyle zenginleştirilmiş bir mimari üzerine kuruludur.
-   **Domain-Driven Design (DDD):** Varlıklar (Entities), Repository'ler, Domain ve Application servisleri, DTO'lar gibi DDD'nin temel yapı taşları kullanılmıştır.
-   **Temiz Mimari (Clean Architecture):** SOLID prensiplerine bağlı kalarak, bağımlılıkları tersine çeviren (Dependency Inversion), gevşek bağlı (Loosely-Coupled) ve test edilebilir bir yapı hedeflenmiştir.
-   **Tasarım Desenleri ve En İyi Pratikler:** Dependency Injection, Logging, Validation ve merkezi Exception Handling gibi modern yazılım geliştirme desenleri ve pratikleri uygulanmıştır.

## Mikroservisler

Proje aşağıdaki ana servislerden oluşmaktadır:

- **Catalog API:** Ürünleri yönetir (listeleme, ekleme, silme, güncelleme).
- **Basket API:** Kullanıcı sepetlerini yönetir. Sepete ürün ekleme, sepeti görüntüleme ve siparişe yönlendirme gibi işlemleri gerçekleştirir. Sepet verileri performans için Redis üzerinde tutulmaktadır.
- **Ordering API:** Sipariş oluşturma ve yönetme süreçlerini ele alır.
- **Discount.Grpc:** Ürünler için indirim kuponlarını yönetir ve gRPC protokolü üzerinden diğer servislerle iletişim kurar.

## Kullanılan Teknolojiler

- **Platform:** .NET 8
- **Mimari:** Mikroservis Mimarisi, CQRS (Command Query Responsibility Segregation)
- **API:** ASP.NET Core Web API, RESTful API, gRPC
- **Veritabanı:** PostgreSQL (Discount servisi için), Redis (Basket servisi için)
- **Konteynerizasyon:** Docker, Docker Compose
- **İletişim:** Senkron (REST, gRPC)
- **Shared/Building Blocks:** MediatR, FluentValidation, Mapster gibi kütüphanelerle ortak altyapı.

## Gelecek Özellikler

- **Asenkron İletişim:** Servisler arası asenkron haberleşme için **RabbitMQ** ve **MassTransit** entegrasyonu planlanmaktadır.

## Proje Nasıl Çalıştırılır?

Projeyi çalıştırmak için sisteminizde **Docker Desktop**'ın kurulu olması gerekmektedir.

1.  Projeyi klonladıktan sonra, terminal veya komut istemcisini projenin ana dizininde açın.
2.  Aşağıdaki Docker Compose komutunu çalıştırın:

    ```bash
    docker-compose up -d
    ```

3.  Bu komut, tüm servisler için gerekli olan imajları oluşturacak, konteynerleri ayağa kaldıracak ve veritabanlarını (PostgreSQL, Redis) başlatacaktır.

Servisler ayağa kalktıktan sonra, her bir servisin `Dockerfile` içinde veya `docker-compose.override.yml` dosyasında belirtilen portlar üzerinden erişilebilir olacaktır.
