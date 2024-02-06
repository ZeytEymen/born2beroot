# born2beroot
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
