# FreeIPA

Домен: astra-net.domain.
Сервер: astra-1.astra-net.domain
Клиент-1: astra-2.astra-net.domain

### Установка статических IP

Перейти в "Панель управления" -> "Сеть" -> "Сетевые соединения", выбрать нужные интерфейс и перейти во вкладку "Настройки IP4". Задать следующие параметры:

![Настрйока статичесих адресов](https://user-images.githubusercontent.com/40645030/120633273-a1838900-c472-11eb-95e8-e2f88aa555ac.png)

в качестве первого DNS сервера должен быть указан контроллер нового домена.

Чтобы настрйоки вступили в силу, необходимо **перезагрузить машину**.

### Включение IPv6 

Для включения протокола IPv6 следует:

  1. Убедиться, что IPv6 не отключен в файле параметров загрузки /etc/default/grub.
   
  Для этого найти в файле строку параметров загрузчика GRUB_CMDLINE_LINUX и убедиться, что там не указан параметр "ipv6.disable=1", если такой параметр указан - убрать его.

  2. Убедиться, что IPv6 не отключен в файле параметров сетевых служб /etc/sysctl.conf, и в файлах /etc/sysctl.d/* (в частности, в файле /etc/sysctl.d/999-astra.conf).
    
  Т.е., убедиться, что в файле отсутствуют строки вида
  
  ```
  net.ipv6.conf.all.disable_ipv6 = 1
  net.ipv6.conf.default.disable_ipv6 = 1
  net.ipv6.conf.lo.disable_ipv6 = 1
  ```
  
  и, если таковые строки имеются, удалить их или закомментировать.

  3. Если изменения были внесены в файл /etc/default/grub, то следует обновить загрузчик:
    
  ```
  $ sudo update-grub
  ```
  
  И перезагрузить машину.

### Установка привилегий

### Установка пакетов

```
$ sudo apt install astra-freeipa-server 
```
