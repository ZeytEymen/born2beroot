born2beroot - Ecole 42 project
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

####  requiretty - TTY modu
TTY modunu aktif eder.Bu komut sadece sudo ön eki ile çalıştırılabilen komutlarda geçerlidir.
Herhangi bir komut çalıştırmak için açık bir terminal ister. TTY1, PTS/0 gibi.
Örneğin ;

    //kendi sunucumuz üzerinden bir dosya oluşturalım
    sudo touch /root deneme.txt //başarı ile oluşturabilmemiz gerek
    // daha sonra buna benzer bir kodu ssh ile oturum açmadan direkt komut göndererek girelim
    ssh <username>@localhost -p 4242 "sudo touch /root ttyModAktif.txt"
    // şifreyi girdikten sonra tty modu akitf ise şöyle bir hata almamız gerek "sudo: sorry, you must have a tty to run sudo"

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

