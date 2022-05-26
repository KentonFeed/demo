# demo
11
https://github.com/KentonFeed/dsystem 
Домен ALD
1. Linux Debian 10.x 64-bit, 2GB, диск 20GB, smolensk 1.6. 
        ald, useradmin, Все ПО, служба ALD, сервер ALD. 

Драйвера:
cd Загрузки/vmware-tools-distrib/
ls
sudo ./vmware-install.pl

Панель управления: сетевые соединения- 192.168.33.130/24

sudo nano /etc/hosts
Вторая строка:
192.168.33.130 ald.demo.lab ald
192.168.33.131 dlp.demo.lab dlp
192.168.33.132 cl.demo.lab cl

Панель управления: доменная политика- создание ALD сервера (везде пароли)- исп свои Настройки сети - создать сервер 

2. sudo mkdir -p /disk1 
sudo mkdir -p /disk2
sudo cp -a /media/cdrom0/* /disk1 (smolensk 1.6)
sudo cp -a /media/cdrom0/* /disk2
 (devel-smolensk 1.6)
sudo nano /etc/apt/sources.list
 deb file:///disk1/ smolensk main non-free contrib
 deb file:///disk2/ smolensk main non-free contrib 
sudo mount /mnt/20190222se16.iso /media/cdrom
sudo apt-cdrom -m add
sudo umount /media/cdrom
sudo apt update
Установить версию из пакета
sudo apt dist-upgrade
sudo apt -f install

5. Firefox- в адресной строке адрес DLP-дополнительно-исключение-исключение 
Логин officer
Пароль xxXX1234
Подключить диск Lic_IWTM (IWTM - Lic_IWTM)
Еще-лицензии- Загрузить -cdrom0-на лицензию и сохранить
Ещё-LDAPсинхронизация - + - имя сервера demo.lab - тип Astra Linux - LDAPсервер 192.168.33.130 - LDAPзапрос dc=demo, dc=lab, в логине demo\admin Сохранить

Панель управления: дом политика-пользователи-синий + - admin - пароль изменить 
Привелегии домена - отметить первые 2 пункта и добавить все компы

4. sudo systemctl status ntp
sudo systemctl enable ntp
sudo systemctl start ntp
sudo apt install fly-admin-ntp
sudo nano /etc/ntp.conf 
Удалить 4 строки pool
Добавить server 127.127.1.0
fudge 127.127.1.0 stratum 10
#restrict удалить # и должно быть 192.168.33.0 вместо 123
ntpq -p


6. systemctl status ssh (active (running))
sudo sysytemctl enable ssh
Пароль xxXX1234
systemctl restart sshd
ssh admin@dlp
Пароль xxXX1234
yes
Активен режим Единого…
sudo nano /etc/ssh/sshd_config
Удаляем # в строке #Port 22 
systemctl restart sshd
sudo netstat -tulpan | grep ssh

7. sudo nano /etc/hosts.allow
sshd: 192.168.33.131, 192.168.33.132
sudo nano /etc/hosts.deny
sshd: ALL

8. Панель упр: сеть- домен политика- пользователи-создать user1-3
Пароль на все xxXX@1234
(1) 
(2)
(3)

9. Пуск - офис - текст Libre - любой текст - сохранить на Раб.столе - файл - цифровые подписи - цифр.подписи - управ.сертифик - создать пару ключей:
имя - Alina
Срок действия - 1 год
Размер ключа - 2048
Алгоритм - GOST R 34.10-2012
 
ctrl p - печатать в файл - печатать в файл - на раб.столе сохранить - по сохр. свойства 

Создать повторный файл с таким же текстом 


———————————————-

DLP
1. 8GB, диск 150GB, smolensk 1.6. 
dlp, useradmin, Средства удаленного доступа SSH, служба ALD, клиент ALD

Драйвера:
cd Загрузки/vmware-tools-distrib/
ls
sudo ./vmware-install.pl

sudo nano /etc/hosts
192.168.33.130 ald.demo.lab ald
192.168.33.131 dlp.demo.lab dlp
192.168.33.132 cl.demo.lab cl

Панель управления: сетевые соединения- 192.168.33.131/24
шлюз 192.168.33.130
DNS 192.168.33.130

настройка ALD: ald.demo.lab, пароль, IP-адрес 192.168.33.130-подключиться

2. sudo mkdir -p /disk1 
sudo mkdir -p /disk2
sudo cp -a /media/cdrom0/* /disk1 (smolensk 1.6)
sudo cp -a /media/cdrom0/* /disk2
 (devel-smolensk 1.6)
sudo nano /etc/apt/sources.list
 deb file:///disk1/ smolensk main non-free contrib
 deb file:///disk2/ smolensk main non-free contrib
sudo mount /mnt/20190222se16.iso /media/cdrom
sudo apt-cdrom -m add
sudo umount /media/cdrom
sudo apt update
sudo apt dist-upgrade
sudo apt -f install
sudo mount /mnt/repository-dev-update.iso /media/cdrom
sudo apt-cdrom -m add
sudo umount /media/cdrom
sudo apt update
sudo apt dist-upgrade
sudo apt -f install

3. sudo cat /etc/astra_update_version
sudo mkdir -p /disk3
sudo mkdir -p /disk4
sudo cp -a /media/cdrom0/* /disk3 (repository)
sudo cp -a /media/cdrom0/* /disk4 (20190222se16)
sudo nano /etc/apt/sources.list
deb file:///disk3/ smolensk main non-free contrib
 deb file:///disk4/ smolensk main non-free contrib
sudo mkdir -p /distr
(astra)
sudo cp -a /media/cdrom0/* /distr 
sudo apt-get update
cd /distr
ls
sudo bash iwtm-installer-6.11.5.1156-astra-smolensk1.6-signed.run
Все по умолчанию (не выбирать SELECT)


4. sudo nano /etc/ntp.conf 
server ald.demo.lab iburst вместо 4х строк pool 
sudo systemctl status ntp
sudo systemctl enable ntp
sudo systemctl start ntp
sudo service ntp restart 
ntpq -p

6. systemctl status ssh (active (running))
sudo sysytemctl enable ssh
Пароль xxXX1234
systemctl restart sshd
ssh admin@ald 
Пароль xxXX1234
yes
Активен режим Единого…
sudo nano /etc/ssh/sshd_config
Удаляем # в строке #Port 22 
systemctl restart sshd
sudo netstat -tulpan | grep ssh

7. sudo nano /etc/hosts.allow
sshd: 192.168.33.130, 192.168.33.132
sudo nano /etc/hosts.deny
sshd: ALL

8. sudo mkdir -p /ssl1
cd /ssl1
sudo openssl genrsa -out rootCA.key 2048 (генерация тайного ключа)
mc (ключ)

sudo openssl req -x509 -new -key rootCA.key -days 365 -out rootCA.crt (корневой сертификат)
ru
khv
khv
httbpt
httpbt
192.168.33.130
demo@lab.com
mc (сертификат и ключ)

sudo openssl genrsa -out dlp.demo.lab.key 2048 (создание подписанного сертификата)

sudo openssl req -new -key dlp.demo.lab.key -out dlp.demo.lab.csr (запрос на сертификат)
mc
ru
khv
khv
demo
demo
192.168.33.131
demo@lab.com
xxXX1234
httbpt

sudo openssl x509 -req -in dlp.demo.lab.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out dlp.demo.lab.crt -days 365(подписываем сертификат)

sudo openssl pkcs12 -export -in rootCA.crt -inkey rootCA.key -out cert.p12

sudo apt install fly-admin-samba
sudo nano /etc/samba/smb.conf
[share]
comment - For all doc’s
# Доступно всем 
guest ok = yes
force user = nobody
force group = nogroup
path = /sry/share
read only = no

sudo systemctl restart smbd
sudo mkdir -p /srv/share/
sudo chown nobody:nogroup /srv/share
sudo chmod 777 /srv/share/
smbtree

Панель управ: сеть - Samba - share - доступ - в 1 строке должен быть nobody - доступ только выбр пользователям (enabled to selected) - выделить - +Добавить - появится на 2 строке - сохранить

ВМ: параметры - жесткий диск - добавить - создать 
sudo apt install lvm2
sudo su
echo “1” > /sys/class/block/sda/device/rescan
echo “- - -“ > /sys/class/scsi_host/host0/scan
echo “- - -“ > /sys/class/scsi_host/host1/scan
echo “- - -“ > /sys/class/scsi_host/host2/scan
fdisk -l /dev/sdb 
pvcreate /dev/sdb
pvscan
pvdisplay
vgcreate vol_grp1 /dev/sdb
lvcreate -L 5G -n logical_vol1 vol_grp1
lvdisplay
apt install cryptsetup
cryptsetup -y -v luksFormat /dev/vol_grp1/logical_vol1
YES
Пароль
cryptsetup luksOpen /dev/vol_grp1/logical_vol1 backup2
ls -l /dev/mapper/backup2
cryptsetup -v status backup2
pv -tpreb /dev/zero | dd of=/dev/mapper/backup2 bs=128M
mkfs.ext4 /dev/mapper/backup2 
mkdir /backup2 
mount /dev/mapper/backup2 /backup2 
ls -l /backup2 
cd /backup2 
ls
Пуск - офис - текст Libre - любой текст - сохранить на Раб.столе - файл - цифровые подписи - цифр.подписи - управ.сертифик - создать пару ключей:
имя - Alina
Срок действия - 1 год
Размер ключа - 2048
Алгоритм - GOST R 34.10-2012
cp -a /home/useradmin/Desktops/Desktop1/backup2.odt /backup2 
ls

Создать текстовый файл script.txt 
Открываем его и пишет 
#!/bin/bash
echo “hello world”
date
Сохранить 
sudo su
chmod ugo+x script.txt
./script.txt
cp -a /home/useradmin/Desktop/script.sh /etc/network/if-up.d
cp -a /home/useradmin/Desktop/script.sh /etc/X11/Xsession.d

?
cat dlp.demo.lab.crt
cat > /etc/nginx/cert.cert 


———————————————-

CLIENT
1. 2GB, диск 20GB, smolensk 1.6. 
client, useradmin, Средства удаленного доступа SSH, служба ALD, клиент ALD

Драйвера:
cd Загрузки/vmware-tools-distrib/
ls
sudo ./vmware-install.pl

sudo nano /etc/hosts
192.168.33.130 ald.demo.lab ald
192.168.33.131 dlp.demo.lab dlp
192.168.33.132 cl.demo.lab cl

Панель управления: сетевые соединения- 192.168.33.132/24
шлюз 192.168.33.130
DNS 192.168.33.130

настройка ALD: ald.demo.lab, пароль, IP-адрес 192.168.33.130-подключиться

2. sudo mkdir -p /disk1 
sudo mkdir -p /disk2
sudo cp -a /media/cdrom0/* /disk1 (smolensk 1.6)
sudo cp -a /media/cdrom0/* /disk2
 (devel-smolensk 1.6)
sudo nano /etc/apt/sources.list
 deb file:///disk1/ smolensk main non-free contrib
 deb file:///disk2/ smolensk main non-free contrib
sudo mount /mnt/20190222se16.iso /media/cdrom
sudo apt-cdrom -m add
sudo umount /media/cdrom
sudo apt update
sudo apt dist-upgrade
sudo apt -f install
sudo mount /mnt/repository-update-dev.iso /media/cdrom
sudo apt-cdrom -m add
sudo umount /media/cdrom
sudo apt update
sudo apt dist-upgrade
sudo apt -f install

В source ничего не удалять

3. sudo mkdir -p /distr
(astra)
sudo cp -a /media/cdrom0/* /distr
cd /distr
sudo tar -xvzf iwdm.6.11.5.468-signed.tar.gz
sudo ./install.sh
sudo ./install.sh dmserver:15101

4. sudo nano /etc/ntp.conf 
server ald.demo.lab iburst вместо 4х строк pool 
sudo systemctl status ntp
sudo systemctl enable ntp
sudo systemctl start ntp
sudo service ntp restart 
ntpq -p

6. systemctl status ssh (active (running))
sudo sysytemctl enable ssh
Пароль xxXX1234
systemctl restart sshd
ssh admin@ald 
Пароль xxXX1234
yes
Активен режим Единого…
sudo nano /etc/ssh/sshd_config
Удаляем # в строке #Port 22 
systemctl restart sshd
sudo netstat -tulpan | grep ssh

7. sudo nano /etc/hosts.allow
sshd: 192.168.33.130, 192.168.33.131
sudo nano /etc/hosts.deny
sshd: ALL


??????????

ssh useradmin@ald:5555 ????

————————————————-

IWDM SERVER
Window Server 2019, BIOS, 2GB, 60GB, образ microsoft 2019 (в папке ОС)
Microsoft Standart( возможности раб стола), выборочная

Установить драйвера - мой комп - этот комп - кликнуть по vmware и установить

ВМ - параметры - параметры - общие папки - всегда включено- добавить диск D 

Мой комп - сеть - кликнуть на желтую строку(включить сетевое обнаружение-да)
IWTM - Postrges- IWTM 6_11 - setup и crawler (на раб.стол)

Параметры (внизу панели комп с желтым знаком) -настройка параметров адаптера - Ethernet0 - свойства - IPv4 - 192.168.33.135

Пуск - Стандартные - Блокнот от им админа 
Блокнот - открыть - диск С - Windows - System32 - drivers - etc - Все файлы - hosts - пишем 192.168.33.131 dlp.demo.lab - сохранить

Мой комп - свойства - изменить параметры - изменить - dmserver workgroup 

Postgres - все по умолчанию-убираем Stack builder 

Setup - все по умолчанию - PostgreSQL - СерверБД: localhost
ИмяБД: db
Имя: postgres
Пароль: xxXX1234
Все по умолчанию 
Имя: officer
Пароль: xxXX1234
Адрес : 192.168.33.131
Токен в браузере ALD -плагины - токены

В Client написать sudo nano /etc/hosts
Добавить 192.168.33.135 dmserver

Консоль управления: имя:localhost , логин:officer, пароль. Инструменты: Настройки - общие(4 строки по 10) - применить и сохранить

ВМ - параметры - добавить - сетевой адаптер - готово - VMnet8(NAT)

От препода - ChromeSetup
Проводник - сеть - сет.папка - IWTM - WinCSCP

WinSCP - хост:192.168.33.131, имя:useradmin

________
(Если комп не появился в консоли упр)
Средства админа -службы: обнаружение SSDP(автоматически); публикация ресурсов обнаружения функции(автомат); узел универсальных PNP-устройств(автомат)
________


