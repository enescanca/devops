## 2. Case

| Machine  Name | Role          | Network Configuration                  | OS                         |
|---------------|---------------|----------------------------------------|----------------------------|
| host       | Ansible  Host | IP: 192.168.80.51    | Focal64    |
| worker         | Wordpress Server  | IP: 192.168.80.52   | Focal64    |

### 2.1. DB kullanan bir uygulamayı dockerized edip, nginx üzerinden serve edilmesi

#### Kurulum 

- Ansible'ın kullanılması için gerekli öngereksinimler; SSH keylerinin, itetilmesi, bağımlıkların kurulması,host dosyasının düzenlenmes  Vagrantfile içinde karşılanmıştır.
- Wordpress'in dockerize edilmesi için ansible öngereksinimleri kendi başına karşılamaktadır.

#### Kullanım

- Önceden hazırlanmış ve konfigüre edilmiş Vagrantfile'dan yararlanılarak `vagrant up` komutu ile iki makine ayağı kaldırılır.
- Aynı dizininde `vagrant ssh host ` ile host sunucusuna bağlanılır.
- `ansible-playbook wordpress-docker.yml -i  hosts ` komutu ile önceden düzenlenmiş hosts filedaki worker sunucusunda ansible komutları yürütülür.



#### Dosya Yapısı

```
.
├── ansible
│   ├── ansible.cfg
│   ├── defaults
│   │   └── main.yml
│   ├── hosts
│   ├── README.md
│   ├── roles
│   │   ├── docker
│   │   │   └── tasks
│   │   │       └── main.yml
│   │   ├── python
│   │   │   └── tasks
│   │   │       └── main.yml
│   │   └── wordpress-docker
│   │       ├── tasks
│   │       │   └── main.yml
│   │       └── templates
│   │           ├── docker-compose.j2
│   │           ├── static.j2
│   │           └── wordpress-nginx.j2
│   └── wordpress-docker.yml
├── provision_ansible.sh
└── Vagrantfile
```


### Roller

```
├── docker
│   └── tasks
│       └── main.yml
```


- Docker bağımlılıklarını ve gereksinimlerini karşılar.

```
├── python
│   └── tasks
│       └── main.yml
```


- Vagrantfile içinde yüklenemiş olan python paketlerini  kontrol eder, kurulu değilse kurulumun sağlar.


```
└── wordpress-docker
│   ├── tasks
│   |   └── main.yml
│   └── templates
│       ├── docker-compose.j2
│       ├── static.j2
│       └── wordpress-nginx.j2
```



- main.yml içerisinde docker-compose.yml'ın oluşturulması Wordpress/MariaDB/Nginx containerlarının deploy'u ve static page'in oluşturulması için konfigürasyon ayarları yer almaktadır.
- docker-compose.j2  : Worker'da çalıştırılacak docker-compose dosyası
- static.j2          : bootcamp=devops' header'ı geldiğinde yönlendirilecek statik sayfası
- wordpress-nginx.
j2 : Wordpress ve bootcamp=devops' header'ı geldiğinde yönlendirilecek statik sayfası için oluşturulmuş Nginx Konfigürasyon dosyası



Kaynaklar:

- https://github.com/bilalcaliskan/vagrant-ansible-lab/
- https://github.com/jamesattard/docker-ansible-wordpress
- https://stackoverflow.com/a/26223734


