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
pkg_version     5.10.166
pkg_sha256      0051a1780e5bda0efc68dafab7c728b8283d2b028fedb439418f478be7d3e1af
```

---

SHA256 linux-firmware:
```
pkg_version     20230117
pkg_sha256      909a3ee4a8ae88efee31cba7cc6b12231c6f0e0cb715d11b289007123a52e610
```
