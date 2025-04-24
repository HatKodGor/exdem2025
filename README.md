*exdem2025*
###
# МОДУЛЬ_1

<br/>

<details>
<summary>Установка/предустановка необходимых пакетов</summary>

 1.Нужно поставить галочку в "Система управления NetworkManager" в категории "Система управления сетевыми интерфейсами" для работы с утилитой "nmcli"
 <p align="center">
  <img width="1080" height="720" src="https://github.com/HatKodGor/exdem2025/blob/main/2.png"
<p\>
<p align="center"><strong>NM</strong></p>

2. В ALT Linux Server/JeOS(если необходимо и будет возможность устанавливать пакеты)
  -  apt-get update - обновление репозиториев пакетов
  -  apt-get install nano - текстовый редактор
  -  apt-get install NetworkManager-tui NetworkManager-cli - работа с сетевыми интерфейсами

<br/>


</details>

<br/>

### Содержание

1. **[Произведите базовую настройку устройств](https://github.com/HatKodGor/exdem2025/blob/main/README.md#%D0%BF%D1%80%D0%BE%D0%B8%D0%B7%D0%B2%D0%B5%D0%B4%D0%B8%D1%82%D0%B5-%D0%B1%D0%B0%D0%B7%D0%BE%D0%B2%D1%83%D1%8E-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D1%83-%D1%83%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%81%D1%82%D0%B2)**

2. **[Настройка ISP](https://github.com/HatKodGor/exdem2025?tab=readme-ov-file#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-2)**
  
3. **[Создание локальных учетных записей]**
  
4. **[Настройте на интерфейсе HQ-RTR в сторону офиса HQ виртуальный коммутатор]**
   
5. **[Настройка безопасного удаленного доступа на серверах HQ-SRV и BR-SRV]**
  
6. **[Между офисами HQ и BR необходимо сконфигурировать IP-туннель]**

7. **[Обеспечьте динамическую маршрутизацию]**

8. **[Настройка динамической трансляции адресов]**

9. **[Настройка протокола динамической конфигурации хостов]**

10. **[Настройка DNS для офисов HQ и BR]**

11. **[Настройте часовой пояс на всех устройствах, согласно месту проведения экзамена]**

<br/>

<p align="center">
  <img width="450" height="600" src="https://github.com/user-attachments/assets/8ee209f5-6fed-4f03-bbe3-e202155957b3"
<p\>
<p align="center"><strong>Топология</strong></p>

<br/>

## Задание 1

### Произведите базовую настройку устройств

- Настройте имена устройств согласно топологии. Используйте полное доменное имя

- На всех устройствах необходимо сконфигурировать IPv4

- IP-адрес должен быть из приватного диапазона, в случае, если сеть локальная, согласно RFC1918

- Локальная сеть в сторону HQ-SRV(VLAN100) должна вмещать не более 64 адресов

- Локальная сеть в сторону HQ-CLI(VLAN200) должна вмещать не более 16 адресов

- Локальная сеть в сторону BR-SRV должна вмещать не более 32 адресов

- Локальная сеть для управления(VLAN999) должна вмещать не более 8 адресов

- Сведения об адресах занесите в отчёт, в качестве примера используйте Таблицу 3

<br/>

<details>
<summary>Решение</summary>
<br/>

**Полное доменное имя можно посмотреть в таблице для [Задания 10](https://github.com/damh66/demo2025/tree/main/module1#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-10)**

<br/>

#### Настройка имен устройств на ALT Linux
```yml
hostnamectl set-hostname <FQDN>; exec bash
```
> FQDN (Fully Qualified Domain Name) - полное доменное имя
> 
> `exec bash` - обновление оболочки

<br/>

#### Настройка имен устройств на EcoRouter

Переходим в режим конфигурации и прописываем следующее:
```yml
hostname <name>
```
> `<name>` - желаемое имя устройства

<br/>

<table align="center">
  <tr>
    <td align="center">Сеть</td>
    <td align="center">Адрес подсети</td>
    <td align="center">Пул-адресов</td>
  </tr>
  <tr>
    <td align="center">SRV-Net (VLAN 100)</td>
    <td align="center">192.168.0.0/26</td>
    <td align="center">192.168.0.1 - 192.168.0.62</td>
  </tr>
  <tr>
    <td align="center">CLI-Net (VLAN 200)</td>
    <td align="center">192.168.1.0/28</td>
    <td align="center">192.168.1.65 - 192.168.1.78</td>
  </tr>
  <tr>
    <td align="center">BR-Net</td>
    <td align="center">192.168.2.0/27</td>
    <td align="center">192.168.2.1 - 192.168.2.30</td>
  </tr>
  <tr>
    <td align="center">MGMT (VLAN 999)</td>
    <td align="center">192.168.99.0/29</td>
    <td align="center">192.168.99.1 - 192.168.99.6</td>
  </tr>
  <tr>
    <td align="center">ISP-HQ</td>
    <td align="center">172.16.4.0/28</td>
    <td align="center">172.16.4.1 - 172.16.4.14</td>
  </tr>
  <tr>
    <td align="center">ISP-BR</td>
    <td align="center">172.16.5.0/28</td>
    <td align="center">172.16.5.1 - 172.16.5.14</td>
  </tr>
</table>
<p align="center"><strong>Таблица подсетей</strong></p>

<br/>

- **Пример таблицы адресации:**

  | Имя Устройства | IPv4                    | Интерфейс      | NIC     | Шлюз        |
  |----------------|-------------------------|----------------|---------|-------------|
  | ISP            | NAT (inet)              | ens33          | Internet|             |
  |                | 172.16.4.14/28          | ens34          | ISP_HQ  |             |
  |                | 172.16.5.14/28          | ens35          | ISP_BR  |             |
  |________________|_________________________|________________|_________|_____________|
  | HQ-RTR         | 172.16.4.1/28           | toISP(ge0)     | ISP_HQ  | 172.16.4.14 |
  |                | 192.168.0.81/29         | vl999          |         |             |
  |                | 192.168.0.62/26         | vl100(ge1)     |         |             |
  |                | 192.168.1.78/28         | vl200(ge1)     | HQ_NET  |             |
  |                | 172.16.0.1/30           | GRE            | TUN     |             |
  |________________|_________________________|________________|_________|_____________|
  | HQ-SRV         | 192.168.0.2/26          | ens34.100@ens34| SRV_NET | 192.168.0.62|
  |________________|_________________________|________________|_________|_____________|
  | HQ-CLI         | 192.168.1.65/28 (DHCP)  | ens34.200@ens34| CLI_NET | 192.168.1.78|
  |________________|_________________________|________________|_________|_____________|
  | BR-RTR         | 172.16.5.1/28           | toISP(ge0)     | ISP_BR  | 172.16.5.14 |
  |                | 192.168.2.1/27          | toBRS_RV(ge1)  | BR_NET  |             |
  |                | 172.16.0.2/30           | GRE            | TUN     |             |
  |________________|_________________________|________________|_________|_____________|
  | BR-SRV         | 192.168.2.2/27          | ens34          | BR_NET  | 192.168.2.1 |

> Адресация для **ISP** взята из следующего задания

<br/>

#### Наcтройка IP-адресации на **HQ-SRV**, **BR-SRV**, **HQ-CLI** (настройка IP-адресации на **ISP** проводится в [следующем задании](https://github.com/damh66/demo2025/tree/main/module1#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-2))

Приводим файлы **`options`**, **`ipv4address`**, **`ipv4route`** в директории **`/etc/net/ifaces/*имя интерфейса*/`** к следующему виду (в примере **HQ-SRV**):
```yml
BOOTPROTO=static
TYPE=eth
NM_CONTROLLED=no
DISABLED=no
CONFIG_IPV4=yes
```
> **`options`**

```yml
192.168.*.*/*
```
> **'ipv4address'**

```yml
default via 192.168.*.*/*
```
> **'ipv4route'**


<br/>

#### Настройка IP-адресации на EcoRouter

Настраиваем интерфейс на **HQ-RTR**, который смотрит в сторону **ISP**:

- Создаем логический интерфейс:
```yml
interface toISP
  ip address 172.16.4.2/28
```

- Настраиваем физический порт:
```yml
port ge0
  service-instance ge0/toISP
    encapsulation untagged
```

- Объединеняем порт с интерфейсом:
```yml
interface toISP
  connect port ge0 service-instance ge0/toISP
```

<br/>

Настраиваем интерфейсы на **HQ-RTR**, которые смотрят в сторону **HQ-SRV** и **HQ-CLI** (с разделением на VLAN):

- Создаем два интерфейса:
```yml
interface vl.100
  description "to hq-srv"
  ip address 192.168.0.62/26
!
interface vl.200
  description "to hq-cli"
  ip address 192.168.1.78/28
```

- Настраиваем порт:
```yml
port ge1
  service-instance vl.100
    encapsulation dot1q 100
    rewrite pop 1
  service-instance vl.200
    encapsulation dot1q 200
    rewrite pop 1
```

- Объединяем порт с интерфейсами:
```yml
interface vl.100
  connect port ge1 service-instance vl.100
!
interface vl.200
  connect port ge1 service-instance vl.200
```

<br/>

#### Адресация на BR-RTR (без разделения на VLAN) настраивается аналогично примеру выше в сторону ISP

<br/>

#### Добавление маршрута по умолчанию в EcoRouter (HQ-RTR; BR-RTR)

Прописываем следующее:
```yml
ip route 0.0.0.0/0 172.16.4.14 - HQ-RTR
ip route 0.0.0.0/0 172.16.5.14 - BR-RTR
```

</details>

<br/>


## Задание 2

### Настройка ISP

- Настройте адресацию на интерфейсах:

  - Интерфейс, подключенный к магистральному провайдеру, получает адрес по DHCP

  - Настройте маршруты по умолчанию там, где это необходимо

  - Интерфейс, к которому подключен HQ-RTR, подключен к сети 172.16.4.0/28

  - Интерфейс, к которому подключен BR-RTR, подключен к сети 172.16.5.0/28

  - На ISP настройте динамическую сетевую трансляцию в сторону HQ-RTR и BR-RTR для доступа к сети Интернет

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка интерфейса, который получает IP-адрес по DHCP
При первом входе в систему должно быть уже предустановлено, на всякий:
<details>
Файл **`options`** (в директории интерфейса"cd /etc/net/ifaces") приводим к следующему виду:
 
```yml
BOOTPROTO=dhcp
TYPE=eth
DISABLED=no
CONFIG_IPV4=yes
```
> **`BOOTPROTO=dhcp`** - заменили статический способ настройки адреса на динамическое получение

</details>

<br/>

#### Настройка маршрута по умолчанию

Прописываем шлюз по умолчанию:
```yml
default via *адрес шлюза*
```
>**ipv4route**

<br/>

#### Настройка интерфейсов, смотрящих в сторону HQ-RTR и BR-RTR происходит аналогично настройке в [Задании 1](https://github.com/HatKodGor/exdem2025?tab=readme-ov-file#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-1)
>**'options' - HQ-RTR/BR-RTR**
<details>
 
 ```yml
 BOOTPROTO=static
 TYPE=eth
 NM_CONTROLLED=no
 DISABLED=no
 CONFIG_IPV4=yes
 ```
</details>

<br/>

>**'ipv4address'**
<details>

 ```yml
172.16.4.14/28 - HQ-RTR
172.16.5.14/28 - BR-RTR
```
</details>

<br/>

#### Включение маршрутизации

В файле **`/etc/net/sysctl.conf`** изменяем строку:
```yml
net.ipv4.ip_forward = 1
```

<br/>

Изменения в файле **`sysctl.conf`** применяем следующей командой:
```yml
sysctl -p /etc/sysctl.conf
```

</details>

<br/>

## Задание 3

### Создание локальных учетных записей

- Создайте пользователя sshuser на серверах HQ-SRV и BR-SRV

  - Пароль пользователя sshuser с паролем P@ssw0rd

  - Идентификатор пользователя 1010

  - Пользователь sshuser должен иметь возможность запускать sudo без дополнительной аутентификации.

- Создайте пользователя net_admin на маршрутизаторах HQ-RTR и BR-RTR

  - Пароль пользователя net_admin с паролем P@$$word

  - При настройке на EcoRouter пользователь net_admin должен обладать максимальными привилегиями

  - При настройке ОС на базе Linux, запускать sudo без дополнительной аутентификации

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Создание пользователя `sshuser` на серверах
(чтобы всё получилось нужно пользователю root дать доступ к sudo "nano cd /etc/sudoers" nano - по желанию)
<p align="center">
  <img  src="https://github.com/HatKodGor/exdem2025/blob/main/3.png">
<p\>

Создаем самого пользователя:
```yml
useradd sshuser -u 1010
```
> опция **`-u`** позволяет указать идентификатор пользователя сразу при создании

<br/>

Задаем пароль:
```yml
passwd sshuser
```

<br/>

Добавляем в группу **wheel**:
```yml
usermod -aG wheel sshuser
```

<br/>

Добавляем строку в **`/etc/sudoers`**:
```yml
sshuser ALL=(ALL) NOPASSWD:ALL
```
> Позволяет запускать **sudo** без аутентификации 

<br/>

#### Создание пользователя `net_admin` на Ecorouter

Создаем самого пользователя:
```yml
username net_admin
```

<br/>

Задаем пароль:
```yml
password P@ssw0rd
```

<br/>

Присваиваем привилегии администратора:
```yml
role admin
```


</details>

<br/>
