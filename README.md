# sing-box-config-selector
Скрипт быстрого выбора конфига sing-box для роутера / Протестировано на Xiaomi AX3000T OPenWRT 23.05.4

В целях тестирования разных VPS серверов и\или конфигов sing-box на роутере имеет смысл как-то автоматизировать и упорядочить выбор конфигурации вместо ручной подмены config.json в /etc/sing-box/ и перезапуска служб sing-box и network для их применения без перезагрузки роутера. 
В /etc/sing-box/ должен лежать текущий действующий конфиг config.json  Рядом в /etc/sing-box/ положить новые конфиги  с именем , например config_1.json , config_2.json и т.д. с новыми параметрами и прочими настройками. 

Скрипт решает эту проблему и выводит при запуске текущий конфиг с именем текущего сервера и список доступных конфигов sing-box , не включая работающий config.json , вместе со списком серверов VPS внутри него . Если конфиг имеет несколько серверов внутри (через "type": "urltest") , то они выводятся одной строкой. Выбор 0 - ничего не меняет в конфигурации и завершает работу скрипта, любой другой выбор делает бэкап текущей конфигурации в папку /etc/sing-box/backups/ с именем config_{timestamp}.bak , заменяет текущий config.json выбранным файлом с переименованием в config.json и рестартит службы sing-box и network для применения настроек. Через несколько секунд можно проверить на, например, 2ip.ru что IP адрес изменился на IP выбранного VPS сервера.  


Выглядит это примерно так после запуска скрипта:
=============================================================================
![image](https://github.com/user-attachments/assets/00e7c7d9-c1f4-43a3-a78e-a1eca46d5b2c)
![image](https://github.com/user-attachments/assets/8c0e6a78-6763-4b47-a405-164746013ba0)
![image](https://github.com/user-attachments/assets/decff2a6-491d-4698-a3a9-743f105ec37b)



==============================================================================

Порядок установки: 
1. Скопировать switch-singbox  в папку /usr/bin/
2. Сделать файл исполняемым  командой
   ```sh
   chmod +x /usr/bin/switch_singbox
   ```   
3. Запускать командой
   ```sh
   /usr/bin/switch-singbox
   ```
5. или добавить alias  для запуска из любого места командой
   ```sh
   alias switch-config='/usr/bin/switch-singbox'
   ```

6. Опционально можно добавить в MOTD (Message of the Day) информацию о быстром запуске и\или добавить в автозагрузку
7. Место на роутере не резиновое, потому следует периодически чистить /etc/sing-box/backups/ от старых бэкапов. Возможно в будущем перепишу скрипт чтобы сохранялась только последняя рабочая конфигурация.


Вы восхитительны! 

