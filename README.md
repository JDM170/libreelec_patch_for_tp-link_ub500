# Пересборка ядра для поддержки TP-Link UB500 в LibreELEC

- Устанавливаем Ubuntu или подобную систему (Если ставим на виртуалку то еще устанавливаем VBox Guest Additions)
- Устанавливаем следующие пакеты: ```sudo apt install libncurses-dev dwarves build-essential gcc bc bison flex libssl-dev libelf-dev```
- Клонируем исходники ядра: ```wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.10.146.tar.xz```
- Распаковываем: ```tar xpvf linux-5.10.146.tar.xz```
- Переходим в папку с распакованным ядром: ```cd linux-5.10.146```
- Открываем файл ```btusb.c```: ```nano drivers/bluetooth/btusb.c```
- Добавляем следующие строки после ```/* Silicon Wave based devices */```:
```
/* Tp-Link UB500 */
{ USB_DEVICE(0x2357, 0x0604), .driver_info = BTUSB_REALTEK },
```
- Проверяем файл ```hci_ldisc.c``` чтобы функция ```hci_uart_tty_read``` совпадала с ниже приведенной:
```
static ssize_t hci_uart_tty_read(struct tty_struct *tty, struct file *file,
                 unsigned char __user *buf, size_t nr,
                 void **cookie, unsigned long offset)
```
- // ```make menuconfig``` -> ```Save``` -> ```Exit```
- Узнаем имя конфигурации текущего ядра: ```ls -la /boot```
- Копируем конфигурацию текущего ядра в папку с нашим ядром: ```cp /boot/config-5.15.0-43-generic .config```
- Отключаем проверку сертификатов (не даст собрать ядро):
```
scripts/config --disable SYSTEM_TRUSTED_KEYS
scripts/config --disable SYSTEM_REVOCATION_KEYS
```
- ```make oldconfig``` -> Жмем Enter пока не появится возможность снова вводить команды
- Собираем ядро: ```make -j6```
- Собираем модули: ```make modules -j6```

---

# Сборка LibreELEC
- Устанавливаем Ubuntu 18.04 или 20.04
- Обновляем систему:
```
sudo apt update
sudo apt upgrade
sudo apt install gcc make git unzip wget xz-utils bc gperf zip g++ xfonts-utils xsltproc openjdk-11-jre-headless texinfo bison flex
```
- Клонируем репо: ```git clone https://github.com/LibreELEC/LibreELEC.tv.git --branch libreelec-10.0```
- Обновляем закидываем папку ```packages``` в директорию репозитория с заменой файлов
- Собираем: ```PROJECT=Allwinner ARCH=arm DEVICE=H3 UBOOT_SYSTEM=orangepi-pc make image -j6```
- Очистка build-директорий: ```make clean```
- Удалить все и ccache: ```make distclean```

---

- Система должна быть настроена после первого запуска, в настройках включаем Samba
- Заходим через Samba в папку ```Configfiles```
- Закидываем папку ```firmware``` в текущую директорию
- Перезапускаем систему

---

SHA256 linux-ядер:
```
pkg_version		5.10.160
pkg_sha256		30d5076acae863941045880c4c5c5109d26a54a932168fa1324237e8aeaa840b

pkg_version 	5.15.84
pkg_sha256 		318dc30cb059c2e35b59652b166b39804bb3a941f11878aae6119019a04b8217
```
