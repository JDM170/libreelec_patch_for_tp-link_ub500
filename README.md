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

SHA256 linux-kernel:
```
pkg_version     5.10.164
pkg_sha256      0c7eaaa87b012c6662440f4ce2ea6e1bb961c1845cafd102eab08a57efeb8278

pkg_version     5.15.89
pkg_sha256      e7311b874e014bb6d37c051319bd6a4a4e3d05a1c32546522deabbfd2d752fe8
```

---

SHA256 linux-firmware:
```
pkg_version     20230117
pkg_sha256      909a3ee4a8ae88efee31cba7cc6b12231c6f0e0cb715d11b289007123a52e610
```
