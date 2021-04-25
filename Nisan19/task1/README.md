#Trendyol System Bootcamp Mezuniyet Projesi 1

##1. Case
|      | Box | Hostname |  IP |
| :--- | :---: | :---: | :---: |
| **Libvirt** | centos/7 | task-1 |192.168.80.50 |

####1.1 Sanal makinada bir Centos kurup, güncellemelerinin yapılması

Kurulum esnasında  "Wheel" grubunda ki noname kullanıcısı ile aşağıdaki komut çalıştırılır.

```bash
# sudo yum -y update
```

#### 1.2 Kişisel bir user yaratılması
Kullanıcı oluşturulur ve şifre atanır.

```bash
# sudo adduser enes.canca
# sudo passwd enes.canca
```
>  Kullanıcının sudo ile komut çalıştırabilmesi için wheel grubuna eklenmesi gereklidir.

```bash
# sudo usermod -aG wheel enes.canca
```
Sonraki işlemleri gerçekleştirmek için enes.canca kullanıcısına geçilir.

```bash
# su - enes.canca
```

####1.3. Sunucuya 2. disk olarak 10 GB disk eklenmesi ve "bootcamp" olarak mount edilmesi


```bash
#HOST ❯ ls /var/lib/libvirt/images|grep task
task_1.qcow2
```
>KVM-Libvirt ile sanallaştırmayı tercih ettiğim için qcow2 formatı ile disk ekliyorum.

```bash
#HOST ❯ #sudo qemu-img create -f qcow2 /var/lib/libvirt/images/task_1-2.qcow2 10G
```
Oluşturulan disk sanal makinaya bağlanır.
```bash
#HOST ❯ sudo virsh attach-disk task_1 /var/lib/libvirt/images/task_1-2.qcow2 vdb --driver qemu --subdriver qcow2 --live --persistent
```
```bash
[enes.canca@task-1 ~]$ sudo fdisk -l | grep '^Disk /dev/vd[a-z]'
Disk /dev/vda: 21.5 GB, 21474836480 bytes, 41943040 sectors
Disk /dev/vdb: 10.7 GB, 10737418240 bytes, 20971520 sectors
```
XFS dosya sistemi oluşturur. /bootcamp' e mount edilir.

```bash
sudo mkfs.xfs /dev/vdb
sudo mkdir -p /bootcamp
echo "/dev/vdb /bootcamp xfs defaults 0 0" | sudo tee -a /etc/fstab
sudo mount -a
```
Çıktıda görüldüğü üzere 10 GB'lık diskimiz /bootcamp altına mount edilmiştir.
```bash
[enes.canca@task-1 ~]$ df -hT
Filesystem              Type      Size  Used Avail Use% Mounted on
devtmpfs                devtmpfs  484M     0  484M   0% /dev
tmpfs                   tmpfs     496M     0  496M   0% /dev/shm
tmpfs                   tmpfs     496M  6.9M  489M   2% /run
tmpfs                   tmpfs     496M     0  496M   0% /sys/fs/cgroup
/dev/mapper/centos-root xfs        17G  1.6G   16G   9% /
/dev/vda1               xfs      1014M  168M  847M  17% /boot
tmpfs                   tmpfs     100M     0  100M   0% /run/user/0
/dev/vdb                xfs        10G   33M   10G   1% /bootcamp
```
#### 1.4. /opt/bootcamp/ altında bootcamp.txt diye bir file yaratılıp, file'ın içerisine "merhaba trendyol" yazılması

/opt/bootcamp dizini oluşturulur ve "merhaba trendyol" text'i eklenir.
```bash
sudo mkdir /opt/bootcamp
echo "merhaba trendyol" | sudo tee -a /opt/bootcamp/bootcamp.txt
```
#### 1.5. Kişisel kullanıcının home dizininde tek bir komut kullanarak bootcamp.txt file'ını bulup, bootcamp
diskine taşınması
```bash
sudo find / -name bootcamp.txt -exec mv {} /bootcamp/ \;
```
