
#### 1. Case

Task 1 dizininin altında yer almaktadır.

- 1.1 Sanal makinada bir Centos kurup, güncellemelerinin yapılması
- 1.2 Kişisel bir user yaratılması (ad.soyad şeklinde) Not: aşağıdaki işlemler bu kullanıcı ile yapılacak
- 1.3. Sunucuya 2. disk olarak 10 GB disk eklenmesi ve "bootcamp" olarak mount edilmesi
- 1.4. /opt/bootcamp/ altında bootcamp.txt diye bir file yaratılıp, file'ın içerisine "merhaba trendyol"
- yazılması
- 1.5. Kişisel kullanıcının home dizininde tek bir komut kullanarak bootcamp.txt file'ını bulup, bootcamp
- diskine taşınması


#### 2. Case

Task 2 dizininin altında yer almaktadır.

2.1. DB kullanan bir uygulamayı dockerized edip, nginx üzerinden serve edilmesi

- DB kullanan bir uygulamanın ansible ile dockerize edilmesi
- Docker kurulumu ve container ayaga kaldırma islemlerinin ansible ile yapılması

2.2 İlk adımda dockerize edilen uygulamanın Nginx üzerinden serve edilmesi ve gelen request içerisinde
bootcamp=devops header'ı varsa "Hoşgeldin Devops" statik sayfasına yönlenebilmesi

- Nginx kurulumu ve konfigürasyonu ansible ile yapılması
- “Hosgeldin DevOps" adlı bir statik sayfa oluşturularak, gelen request içerisinde bootcamp=devops header'ı varsa bu sayfaya yönlendirilmesi
