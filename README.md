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
pkg_version     5.10.169
pkg_sha256      d9754f6eb55e88214c7aaa7c4831c215f88b48da1d9b40f871b055ff56ebafcf
```

---

SHA256 linux-firmware:
```
pkg_version     20230210
pkg_sha256      e636883887e660926306c9b73173765eae2c3261003a60a4351d7da2f72feebd
```
