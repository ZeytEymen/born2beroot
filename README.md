# born2beroot
##  Sanal Makina Nedir, Nasıl Çalışır, Amacı Nedir
Temel olarak, sanal makine yazılımı bilgisayarların sanallaştırma özelliğini kullanarak, fiziksel bilgisayarın kaynaklarını sanal makineler arasında paylaştırır ve her sanal makineyi fiziksel bir bilgisayar gibi davranacak şekilde izole eder.
Yeni çıkan beta sürümleri test etmek,
Bir bilgisayarda birden çok işletim sistemi ile paralel çalışmak.
gibi birçok sebeple kullanılabilir.

##  Rocky ve Debian Arasındaki Temel Farklar
|DEBIAN|ROCKY  |
|--|--|
|Daha fazla güncelleme alır kararsız bir yapıdadır|Daha az güncelleme alır ve daha kararlı bir yapıdadır |
|Bağımsız bir projedir ve kendine özgü bir topluluk tarafından geliştirilir.|Red Hat topluluğu tarafından geliştirilir ve kurumsal yapılarda tercih edilir|
|Geniş bir topluluk tarafından desteklenir ve geniş bir belgelendirme ve rehberlik kaynağına sahiptir.|Daha yeni bir proje olduğundan, topluluk desteği ve dokümantasyonunun Debian kadar geniş olmadığı söylenebilir.|
|apt adı verilen paket yöneticisini kullanır|yum adı verilen RPM tabanlı paket yöneticisini kullanır|

##  'aptitude' ve 'apt' Arasındaki Fark

|apt|aptitude|
|--|--|
|Basit ve hızlı bir paket yönetim aracı |Daha kapsamlı bir kontrol ve bağımlılık yönetimi|
|Sadece komut satırı tabanlıdır ve doğrudan grafik bir kullanıcı arayüzü sunmaz|`aptitude`'ın grafik kullanıcı arayüzü bulunur|

##  APPArmor Nedir
Ubuntu’nun 7.10 sürümünden itibaren default olarak dahil edilen önemli bir güvenlik özelliğidir. Güvenlik politikalarını uygulamak için kullanılan bir güvenlik çerçevesidir. Temel olarak, uygulamaların ve süreçlerin belirli kaynaklara (dosyalar, klasörler, ağ bağlantıları vb.) erişimini sınırlar ve izler. Bu, kötü niyetli bir yazılımın veya yetkisiz bir kullanıcının sisteme zarar vermesini önler.

####  UFW ve SSH servislerinin durumunu kontrol etme

    sudo systemctl status <ufw or ssh>
####  İşletim sistemi kontrolü

    sudo hostnamectl
---
####  'username' kullanıcısının sudo ve user42 gruplarında olduğunu kontrol et.

    sudo getent passwd <username>
    id <username>
####  Şifre politika kurallarına göz at

    sudo vim /etc/login.defs
    sudo vim /etc/pam.d/common-password //libpam-pwquality paketi

####  Kullanıcı bazlı şifre kurallarına bak ve değiştir

    sudo chage -l <username> //kuralları göster
    sudo chage -l --mindays <number> <username>
    sudo chage -l --maxdays<number> <username>
    sudo chage -l --warndays<number> <username>

####  Kullanıcı ve Grup oluşturma , ekleme

    sudo adduser <username> // Kullanıcıyı yönergeye göre oluştur
    id <username> //oluşturuldu mu ???
    sudo addgroup <groupName> //grup oluştur
    sudo adduser <username> <groupname> //gruba kullanıcı ekle

----
####  Ana Bilgisayar adı ve Değiştirme

    sudo hostnamectl //bilgisayar adı işletim sistemi vs bilgiler
    sudo hostnamectl set-hostname <newHostName> //adı değiştirdik
    sudo vim /etc/hosts //buradanda değiştiriyoruz
    //reboot edip tekrar hostnamectl ile kontrol ediyoruz
---
####  Sanal Makina ve Bölümleri

    lsblk

<img src="https://i.hizliresim.com/9po1kgn.jpg">

 

 - LVM NEDİR
 LVM, fiziksel disklerden (hard diskler, SSD'ler) mantıksal hacimler oluşturarak esnek bir depolama altyapısı sağlar.
 Mantıksal hacimler, fiziksel disklerdeki bölümleme sınırlamalarını aşarak daha esnek bir depolama çözümü sunar.
 ---

####  SUDO

    dpkg -l | grep sudo //sudo yüklü mü kontrolü
    getent group sudo // sudo grubundakileri gör
    sudo cat /var/log/sudo/sudo.log // sudo ile yapılan her işlemi kontrol et
---
####  UFW
Linux tabanlı işletim sistemlerinde güvenlik duvarı (firewall) yönetimini basitleştiren bir araçtır. Temel olarak, UFW, sistemde gelen ve giden ağ trafiğini kontrol etmenizi sağlar ve böylece ağ güvenliğini sağlar.
UFW ile belirli ağ trafiği için kurallar oluşturursunuz. Bu kurallar, hangi tür trafiğin sistem üzerinden geçebileceğini veya engelleneceğini belirtir.

    dpkg -l | grep ufw //yüklü mü
    systemctl status ufw //aktif mi
    sudo ufw status //izin verilen portlar
    sudo ufw status numbered //numaralandırılmıs
    sudo ufw delete <number> //numaralı olanı sil
    sudo ufw allow <portnumber> //yeni kural ekle
---
####  SSH

  
SSH (Secure Shell) güvenli ve şifreli bir şekilde bilgisayarlar arasında iletişim sağlayan bir ağ protokolüdür. Uzaktan erişim, dosya aktarımı ve diğer ağ işlevleri için yaygın olarak kullanılır.

    dpkg -l | grep ssh //yüklü mü 
    systemctl status ssh //aktif mi
    sudo vim /etc/ssh/sshd_config //açık porta bak
    ssh <username>@localhost -p 4242 // bağlan


####  requiretty - TTY modu
TTY modunu aktif eder.Bu komut sadece sudo ön eki ile çalıştırılabilen komutlarda geçerlidir.
Herhangi bir komut çalıştırmak için açık bir terminal ister. TTY1, PTS/0 gibi.
Örneğin ;

    //kendi sunucumuz üzerinden bir dosya oluşturalım
    sudo touch /root deneme.txt //başarı ile oluşturabilmemiz gerek
    // daha sonra buna benzer bir kodu ssh ile oturum açmadan direkt komut göndererek girelim
    ssh <username>@localhost -p 4242 "sudo touch /root ttyModAktif.txt"
    // şifreyi girdikten sonra tty modu akitf ise şöyle bir hata almamız gerek "sudo: sorry, you must have a tty to run sudo"
---
####  Monitoring scripti ve açıklamaları

    #!/bin/bash
    
    # ARCH
    arch=$(uname -a)
    
    # CPU PHYSICAL
    cpuf=$(grep "physical id" /proc/cpuinfo | wc -l)
    
    # CPU VIRTUAL
    cpuv=$(grep "processor" /proc/cpuinfo | wc -l)
    
    # RAM
    ram_total=$(free --mega | awk '$1 == "Mem:" {print $2}')
    ram_use=$(free --mega | awk '$1 == "Mem:" {print $3}')
    ram_percent=$(free --mega | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}')
    
    # DISK
    disk_total=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_t += $2} END {printf ("%.1fGb\n"), disk_t/1024}')
    disk_use=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_u += $3} END {print disk_u}')
    disk_percent=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_u += $3} {disk_t+= $2} END {printf("%d"), disk_u/disk_t*100}')
    
    # CPU LOAD
    cpul=$(vmstat 1 2 | tail -1 | awk '{printf $15}')
    cpu_op=$(expr 100 - $cpul)
    cpu_fin=$(printf "%.1f" $cpu_op)
    
    # LAST BOOT
    lb=$(who -b | awk '$1 == "system" {print $3 " " $4}')
    
    # LVM USE
    lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)
    
    # TCP CONNEXIONS
    tcpc=$(ss -ta | grep ESTAB | wc -l)
    
    # USER LOG
    ulog=$(users | wc -w)
    
    # NETWORK
    ip=$(hostname -I)
    mac=$(ip link | grep "link/ether" | awk '{print $2}')
    
    # SUDO
    cmnd=$(journalctl _COMM=sudo | grep COMMAND | wc -l)
    
    wall "	Architecture: $arch
    	CPU physical: $cpuf
    	vCPU: $cpuv
    	Memory Usage: $ram_use/${ram_total}MB ($ram_percent%)
    	Disk Usage: $disk_use/${disk_total} ($disk_percent%)
    	CPU load: $cpu_fin%
    	Last boot: $lb
    	LVM use: $lvmu
    	Connections TCP: $tcpc ESTABLISHED
    	User log: $ulog
    	Network: IP $ip ($mac)
    	Sudo: $cmnd cmd"
---

    uname -a
İşletim sistemi hakkında bilgi veren bir komuttur.

---
```
grep "physical id" /proc/cpuinfo | wc -l
```
Bu komut, `/proc/cpuinfo` dosyasındaki "physical id" satırlarını bulur ve bu satırların sayısını sayar.

---
```
    grep "processor" /proc/cpuinfo | wc -l
```

Bu komut, `/proc/cpuinfo` dosyasındaki "processor " satırlarını bulur ve bu satırların sayısını sayar.

---
```
ram_total=$(free --mega | awk '$1 == "Mem:" {print $2}')
ram_use=$(free --mega | awk '$1 == "Mem:" {print $3}')
ram_percent=$(free --mega | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}')
```
 `ram_total=$(free --mega | awk '$1 == "Mem:" {print $2}')`: Bu satır, toplam RAM miktarını MB cinsinden belirler. `free --mega` komutu, RAM kullanımı hakkında bilgiler sağlar ve `awk` komutuyla "Mem:" başlığı altındaki satırın ikinci sütununu (yani toplam RAM miktarını) alır ve `ram_total` değişkenine atar.
    
`ram_use=$(free --mega | awk '$1 == "Mem:" {print $3}')`: Bu satır, şu anda kullanılan RAM miktarını MB cinsinden belirler. Aynı şekilde, `free --mega` komutu kullanılarak RAM kullanımı hakkında bilgiler sağlanır ve `awk` komutuyla "Mem:" başlığı altındaki satırın üçüncü sütununu (yani kullanılan RAM miktarını) alır ve `ram_use` değişkenine atar.
    
`ram_percent=$(free --mega | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}')`: Bu satır, RAM kullanımının yüzde olarak belirlenmesini sağlar. Yine, `free --mega` komutu kullanılarak RAM kullanımı hakkında bilgiler sağlanır. `awk` komutuyla "Mem:" başlığı altındaki satırlardan kullanılan ve toplam RAM miktarı alınır. Ardından, kullanılan RAM miktarının toplam RAM miktarına oranı hesaplanır ve yüzde olarak ifade edilir. Sonuç, `ram_percent` değişkenine atanır. Bu, RAM kullanımının yüzde cinsinden bir değerini temsil eder.

---
```
disk_total=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_t += $2} END {printf ("%.1fGb\n"), disk_t/1024}')
disk_use=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_u += $3} END {print disk_u}')
disk_percent=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_u += $3} {disk_t+= $2} END {printf("%d"), disk_u/disk_t*100}')
```
Bu kod bloğu, disk kullanımıyla ilgili istatistikleri hesaplar.

 `disk_total=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_t += $2} END {printf ("%.1fGb\n"), disk_t/1024}')`: Bu satır, disklerin toplam kapasitesini hesaplar. İlk olarak, `df -m` komutuyla disk kullanımı bilgileri alınır. Ardından, `/dev/` dizinine sahip olan satırlar `grep "/dev/"` ile filtrelenir. Ancak, `/boot` dizini filtrelenir ve `grep -v "/boot"` ile dışlanır. Son olarak, AWK ile toplam disk kapasitesi hesaplanır ve GB cinsinden yazdırılır.

 `disk_use=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_u += $3} END {print disk_u}')`: Bu satır, disklerin şu anki kullanımını MB cinsinden hesaplar. Benzer şekilde, `df -m` komutuyla disk kullanımı bilgileri alınır, `/dev/` dizinine sahip olan satırlar `grep "/dev/"` ile filtrelenir ve `/boot` dizini filtrelenir. Ardından AWK ile toplam disk kullanımı hesaplanır ve MB cinsinden yazdırılır.

`disk_percent=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_u += $3} {disk_t+= $2} END {printf("%d"), disk_u/disk_t*100}')`: Bu satır, disk doluluğunun yüzde olarak hesaplanmasını sağlar. Yine, `df -m` komutuyla disk kullanımı bilgileri alınır, `/dev/` dizinine sahip olan satırlar `grep "/dev/"` ile filtrelenir ve `/boot` dizini filtrelenir. Son olarak, AWK ile disk kullanımı ve toplam disk kapasitesi hesaplanır, ardından disk doluluğu yüzde cinsinden yazdırılır.

---
```
cpul=$(vmstat 1 2 | tail -1 | awk '{printf $15}')
cpu_op=$(expr 100 - $cpul)
cpu_fin=$(printf "%.1f" $cpu_op)
```
`cpul=$(vmstat 1 2 | tail -1 | awk '{printf $15}')`: Bu satır, CPU kullanımını belirler. İlk olarak, `vmstat 1 2` komutuyla CPU kullanım istatistikleri alınır. `tail -1` komutu, son satırı alır çünkü bu satırın istenilen istatistikler içerdiği kabul edilir. Son olarak, AWK ile CPU kullanımı değeri belirlenir ve değişkene atanır.
    
 `cpu_op=$(expr 100 - $cpul)`: Bu satır, CPU kullanımının yüzde cinsinden doluluk oranını hesaplar. `expr` komutu, basit matematiksel işlemler yapmak için kullanılır. Burada, 100'den CPU kullanımı değeri çıkarılarak boş CPU yüzdesi hesaplanır ve bu değer `cpu_op` değişkenine atanır.
    
`cpu_fin=$(printf "%.1f" $cpu_op)`: Bu satır, CPU kullanımının virgülden sonra bir basamağa yuvarlanmasını sağlar. `printf "%.1f"` ifadesi, bir sayıyı virgülden sonra bir basamak olacak şekilde formatlar. Bu şekilde, CPU kullanımı yüzdesi daha okunaklı bir şekilde yazdırılır ve `cpu_fin` değişkenine atanır.

---
```
lb=$(who -b | awk '$1 == "system" {print $3 " " $4}')
```

`lb=$(who -b | awk '$1 == "system" {print $3 " " $4}')`: Bu satır, sistemin başlangıç zamanını belirler. `who -b` komutu, sistemin son yeniden başlatılma zamanını gösterir. `awk '$1 == "system" {print $3 " " $4}'` ifadesi, `who -b` komutunun çıktısını işler ve "system" kullanıcısına ait olan satırı bulur. Sonrasında bu satırdaki üçüncü ve dördüncü sütunları, yani başlangıç tarihini ve saati alır. Bu bilgiler, `lb` değişkenine atanır.

---
```
lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)
```
`lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)`: Bu satır, LVM'nin kullanılıp kullanılmadığını belirler. İlk olarak, `lsblk` komutu ile blok cihazları listelenir ve `grep "lvm"` ile LVM'ye ait olan satırlar filtrelenir. Daha sonra, `wc -l` ile bu satırların sayısı hesaplanır. `-gt 0` koşulu, bu sayının 0'dan büyük olup olmadığını kontrol eder. Eğer LVM'ye ait bir blok cihazı bulunursa, yani `lsblk` çıktısında LVM'ye ait bir satır varsa, `echo yes` çalıştırılır; aksi takdirde `echo no` çalıştırılır. Sonuç, `lvmu` değişkenine atanır. Bu sayede `lvmu` değişkeni "yes" veya "no" olarak atanır, LVM'nin kullanılıp kullanılmadığına dair bilgi verir.

```
tcpc=$(ss -ta | grep ESTAB | wc -l)
```
`tcpc=$(ss -ta | grep ESTAB | wc -l)`: Bu satır, TCP bağlantılarının sayısını hesaplar. İlk olarak, `ss -ta` komutu, TCP bağlantılarının detaylarını listeler. Ardından, `grep ESTAB` ile bu listeyi ESTABLISHED durumundaki TCP bağlantılarını filtreler. Son olarak, `wc -l` komutu ile bu filtrelenmiş satırların sayısı hesaplanır ve `tcpc` değişkenine atanır. Bu, sistemdeki mevcut TCP bağlantılarının sayısını temsil eder.

---

```
ulog=$(users | wc -w)
```
`ulog=$(users | wc -w)`: Bu satır, `users` komutuyla mevcut oturum açmış kullanıcıların listesini alır. Ardından, `wc -w` komutuyla bu kullanıcı listesinin kelime sayısını hesaplar. Her bir kullanıcı bir kelime olarak kabul edilir. Sonuç, `ulog` değişkenine atanır ve bu değişken, şu anda oturum açmış olan kullanıcıların sayısını temsil eder.

---
```
ip=$(hostname -I)
mac=$(ip link | grep "link/ether" | awk '{print $2}')
```
 `ip=$(hostname -I)`: Bu satır, `hostname -I` komutuyla sistemdeki tüm ağ arabirimlerinin IP adreslerini alır. Birden fazla IP adresi varsa, bu IP adresleri bir boşlukla ayrılarak `ip` değişkenine atanır.
    
 `mac=$(ip link | grep "link/ether" | awk '{print $2}')`: Bu satır, `ip link` komutuyla sistemdeki ağ arabirimlerinin detaylarını alır. `grep "link/ether"` komutuyla sadece MAC adreslerini içeren satırları filtreler. Ardından, AWK kullanılarak bu satırlardan sadece MAC adresleri (ikinci sütun) çıkarılır ve `mac` değişkenine atanır. Bu, sistemdeki birincil ağ arabiriminin MAC adresini temsil eder.
 
---
```
cmnd=$(journalctl _COMM=sudo | grep COMMAND | wc -l)
```
`cmnd=$(journalctl _COMM=sudo | grep COMMAND | wc -l)`: Bu satır, `journalctl` komutuyla sistem günlüklerini inceleyerek `sudo` komutuyla yapılan işlemleri arar. `_COMM=sudo` ifadesi, sadece `sudo` komutuyla ilgili kayıtları filtreler. Ardından, `grep COMMAND` komutu ile `sudo` komutunun başarılı çalıştırılması durumundaki kayıtları bulur. Son olarak, `wc -l` komutu ile bulunan bu kayıtların sayısı hesaplanır ve `cmnd` değişkenine atanır. Bu, `sudo` komutuyla yapılan başarılı işlemlerin sayısını temsil eder.

---
 WALL nedir
"Wall" kısaltması "write all"dan gelir ve "duvara yaz" anlamına gelir. Bu komut, bir sistem yöneticisinin veya yetkili bir kullanıcının, sistemdeki tüm kullanıcılara bir mesaj göndermesini sağlar. Bu mesaj, terminalde çalışan her kullanıcıya ulaşır ve sistemdeki tüm kullanıcılara eşzamanlı olarak iletilir.

## Tüm  Kodlar ve Anlamları

    su -
    sudo -s
Root ortamına geçmek için.

---
    lsblk
Disk yapısını incelemek için

---

    reboot
Sisteme reset atar

---

    hostnamectl
Host adı sürüm bilgisi vs öğrenme

    hostnamectl set-hostname <newHostName>
Yeni Host adı vermek için bu kod yazılır fakat;

    vim etc/hosts
dosyasına erişmeli ve değişikliği burayada uygulamayız, değişiklerin kaydedilmesi için sisteme reset atmak gerekir...

##  Kullanıcı ve Grup

    sudo adduser <username>
Yeni bir kullanıcı oluştur

---
    sudo getent passwd <username>
    id <username>
Kullanıcıya ait bilgiler (kullanıcı oluşturulduğuna dair bilgi)

---

    sudo passwd
Root şifresi değiştir

    passwd
Aktif kullanıcı şifresi değiştir

    passwd <username>
Belirtilen kullanıcı şifresini değiştirmek

---

    sudo deluser <username>
Kullanıcıyı siler

    sudo deluser --remove-home <username>
Kullacıyı ana dizini ile birlikte kaldırır

    sudo deluser --remove-all-files <username>
Kullanıcıya ait tüm dosyalar temizlenir.

---

    sudo addgroup <group>
   Grup oluştur.

    sudo adduser <username> <group>
    sudo usermod -aG <group> <username>
Gruba kullanıcı ekleme

---

    adduser <username> <group>
    usermod -aG <group> <username> 
Kullanıcıyı istenilen bir gruba ekler

---
    getent group <group>
 Gruptaki kullanıcıları görüntüleme
 
---

    sudo chage -l <username>
   Kullanıcıya dayatılan şifre politikalarını öğren.

---

    groups
    groups <username>
Dahil olunan grupları öğren, sadece groups yazılırsa aktif kullanıcıya dair bilgiler.

##  SSH
    dpkg -l | grep ssh
Kurulum kontrolü

    ssh <username>@127.0.0.1 -p 4242
SSH ile sanal makinaya bağlan

    sudo systemctl status ssh
    sudo service ssh status
SSH servisi aktif durumu öğren

    sudo systemctl restart ssh
    sudo service ssh restart
SSH servisine reset at

    sudo grep Port /etc/ssh/sshd_config
Port ayarlarını kontrol et

    sudo vim /etc/ssh/sshd_config
SSH ayarlarına eriş

    logout
    exit
SSH ile bağlandı isen sonlandır

    who
SSH ile bağlandığın zaman sanal makinadan terminale kimler hangi şekilde bağlı görebiliriz.
