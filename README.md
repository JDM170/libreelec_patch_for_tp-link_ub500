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
```sudo apt update
sudo apt upgrade
sudo apt install gcc make git unzip wget xz-utils bc gperf zip g++ xfonts-utils xsltproc openjdk-11-jre-headless texinfo bison flex```
- Клонируем репо:
```git clone https://github.com/LibreELEC/LibreELEC.tv.git --branch libreelec-10.0```
- Обновляем ```packages -> linux -> package.mk```:
```pkg_version	5.10.159
pkg_sha256	1ba9bf57b6bf36d76447d5044b80b746cb5fd61d981c811603dc763b7789cea7

pkg_version 	5.15.83
pkg_sha256	40590843c04c85789105157f69efbd71a4efe87ae2568e40d1b7258c3f747ff3
```
- Собираем: ```PROJECT=Allwinner ARCH=arm DEVICE=H3 UBOOT_SYSTEM=orangepi-pc make image -j6```
- Очистка build-директорий: ```make clean```
- Удалить все и ccache: ```make distclean```
