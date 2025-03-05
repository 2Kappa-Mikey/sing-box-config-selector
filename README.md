# sing-box-config-selector
Скрипт быстрого выбора конфига sing-box для роутера / Протестировано на Xiaomi AX3000T OPenWRT 23.05.4

В целях тестирования разных VPS серверов и\или конфигов на них имеет смысл как-то автоматизировать и упорядочить выбор вместо ручной подмены config.json в /etc/sing-box/ и перезапуска служб sing-box и network для их применения без перезагрузки роутера. 

Скрипт решает эту проблему и выводит при запуске текущий конфиг с именем текущего сервера и список доступных конфигов sing-box , не включая работающий config.json , вместе со списком серверов VPS внутри него . Если конфиг имеет несколько серверов внутри (через "type": "urltest") , то они выводятся одной строкой. Выбор 0 - ничего не меняет в конфигурации и завершает работу скрипта, любой другой выбор делает бэкап текущей конфигурации в папку /etc/sing-box/backups/ с именем config_{timestamp}.bak , заменяет текущий config.json выбранным файлом с переименованием и рестартит службы sing-box и network для применения настроек. Через несколько секунд можно проверить на, например, 2ip.ru что IP адрес изменился на IP выбранного VPS сервера.  


Выглядит это примерно так после запуска скрипта:
=============================================================================
BusyBox v1.36.1 (2024-07-15 22:14:18 UTC) built-in shell (ash)
  _______                     ________        __
 |       |.-----.-----.-----.|  |  |  |.----.|  |_
 |   -   ||  _  |  -__|     ||  |  |  ||   _||   _|
 |_______||   __|_____|__|__||________||__|  |____|
          |__| W I R E L E S S   F R E E D O M
 -----------------------------------------------------
 OpenWrt 23.05.4, r24012-d8dd03c46f
 -----------------------------------------------------
  Быстрый доступ:
 - Сменить конфиг Sing-Box: /root/switch-config
 =====================================================
 root@OpenWrt:~# /root/switch-config
Current config: config.json
Server name: config.example.com

Available configurations:
1) config_1.json (Server: config1.example.com)
2) config_10.json (Server: config10.example.com)
3) config_2.json (Server: config2.example.com)
4) config_3.json (Server: config3.example.com)
5) config_4.json (Server: config4.example.com)
6) config_5.json (Server: config5.example.com)
7) config_6.json (Server: config6.example.com)
8) config_7.json (Server: config7.example.com, config7-1.example.com, config7-2.example.com)
9) config_8.json (Server: config8.example.com)
10) config_9.json (Server: config9.example.com, config9-1.example.com)

0) Cancel and keep current config

Select configuration (0-10):
==============================================================================

Порядок установки:
1. Скопировать switch-singbox  в папку /usr/bin/
2. Сделать файл исполняемым  командой chmod +x /usr/bin/switch_singbox
3. Запускать командой /usr/bin/switch-singbox
4. или добавить alias  для запуска из любого места alias switch-config='/usr/bin/switch-singbox' 

5. Опционально можно добавить в MOTD (Message of the Day) информацию о быстром запуске и\или добавить в автозагрузку 




