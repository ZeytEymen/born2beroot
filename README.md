# born2beroot
born2beroot - Ecole 42 project

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
