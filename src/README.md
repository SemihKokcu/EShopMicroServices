# E-Shop Microservices

Bu proje, .NET üzerinde geliştirilmiş, mikroservis mimarisine dayalı bir e-ticaret platformu uygulamasıdır. Proje, modern yazılım geliştirme prensipleri ve teknolojileri kullanılarak tasarlanmıştır.

## Proje Hakkında

Bu platform, temel e-ticaret işlevlerini (ürün katalogu, sepet yönetimi, sipariş ve indirimler) ayrı servislere bölerek yönetir. Her servis, kendi sorumluluk alanına odaklanmış olup, bağımsız olarak geliştirilebilir, dağıtılabilir ve ölçeklendirilebilir.

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

## Proje Nasıl Çalıştırılır?

Projeyi çalıştırmak için sisteminizde **Docker Desktop**'ın kurulu olması gerekmektedir.

1.  Projeyi klonladıktan sonra, terminal veya komut istemcisini projenin ana dizininde açın.
2.  Aşağıdaki Docker Compose komutunu çalıştırın:

    ```bash
    docker-compose up -d
    ```

3.  Bu komut, tüm servisler için gerekli olan imajları oluşturacak, konteynerleri ayağa kaldıracak ve veritabanlarını (PostgreSQL, Redis) başlatacaktır.

Servisler ayağa kalktıktan sonra `launchSettings.json` dosyasında belirtilen portlar üzerinden erişilebilir olacaktır.
