# Сборка LibreELEC
- Устанавливаем Ubuntu 18.04 или 20.04
- Обновляем систему:
```
sudo apt update
sudo apt upgrade
sudo apt install gcc make git unzip wget xz-utils bc gperf zip g++ xfonts-utils xsltproc openjdk-11-jre-headless texinfo bison flex
```
- Клонируем репо: ```git clone https://github.com/LibreELEC/LibreELEC.tv.git --branch libreelec-10.0```
- Закидываем папку ```packages``` в директорию репозитория с заменой файлов
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
pkg_version		5.10.163
pkg_sha256		96e226e2d388abc0600434e0f4f365a8829ef901f4d8e761e7ffe2799dc09b20

pkg_version 	5.15.88
pkg_sha256 		417539fdd96a3af97ef9ad2b51ca13967cb922f53970563b60290b935a81a181
```
