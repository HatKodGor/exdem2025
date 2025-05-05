*exdem2025*
###
# МОДУЛЬ_1

<details>
<summary> Полное решение </summary>

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
  
3. **[Создание локальных учетных записей](https://github.com/HatKodGor/exdem2025?tab=readme-ov-file#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-3)**
  
4. **[Настройте на интерфейсе HQ-RTR в сторону офиса HQ виртуальный коммутатор](https://github.com/HatKodGor/exdem2025/blob/main/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-4)**
   
5. **[Настройка безопасного удаленного доступа на серверах HQ-SRV и BR-SRV](https://github.com/HatKodGor/exdem2025/blob/main/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-5)**
  
6. **[Между офисами HQ и BR необходимо сконфигурировать IP-туннель](https://github.com/HatKodGor/exdem2025/blob/main/README.md#6-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-ip-%D1%82%D1%83%D0%BD%D0%BD%D0%B5%D0%BB%D1%8F-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-%D0%BE%D1%84%D0%B8%D1%81%D0%B0%D0%BC%D0%B8)**

7. **[Обеспечьте динамическую маршрутизацию](https://github.com/HatKodGor/exdem2025?tab=readme-ov-file#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-7)**

8. **[Настройка динамической трансляции адресов](https://github.com/HatKodGor/exdem2025?tab=readme-ov-file#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-8)**

9. **[Настройка протокола динамической конфигурации хостов](https://github.com/HatKodGor/exdem2025?tab=readme-ov-file#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-9)**

10. **[Настройка DNS для офисов HQ и BR](https://github.com/HatKodGor/exdem2025?tab=readme-ov-file#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-10)**

11. **[Настройте часовой пояс на всех устройствах, согласно месту проведения экзамена](https://github.com/HatKodGor/exdem2025?tab=readme-ov-file#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-11)**

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

(в основном ip-адреса для HQ-SRV/CLI и BR-SRV настраиваются на самом vlan)

Приводим файлы **`options`**, **`ipv4address`**, **`ipv4route`** в директории **`/etc/net/ifaces/*имя интерфейса*/`** к следующему виду (более опционально для ISP)

```yml
BOOTPROTO=static
TYPE=eth
NM_CONTROLLED=no
DISABLED=no
CONFIG_IPV4=yes
```
> **`options`**

```yml
192.168.*.*/* (пример)
```
> **'ipv4address'**

```yml
default via 192.168.*.*/* (пример)
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
(чтобы всё получилось нужно пользователю root дать доступ к sudo "nano cd /etc/sudoers" nano - по желанию) нужно расскомментировать текст, то где белый текст в левой стороне изначально стоит "#" его нужно убрать
<p align="center">
  <img  src="https://github.com/HatKodGor/exdem2025/blob/main/3.png">
<p\>

Создаем самого пользователя(мы находимся под пользователем root):
```yml
sudo useradd sshuser -u 1010
```
> опция **`-u`** позволяет указать идентификатор пользователя сразу при создании

<br/>

Задаем пароль:
```yml
sudo passwd sshuser
```

<br/>

Добавляем в группу **wheel**:
```yml
sudo usermod -aG wheel sshuser
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
(config)username net_admin
```

<br/>

Задаем пароль:
```yml
(config-user)password P@ssw0rd
```

<br/>

Присваиваем привилегии администратора:
```yml
(config-user)role admin
```


</details>

## Задание 4

### Настройте на интерфейсе HQ-RTR в сторону офиса HQ виртуальный коммутатор

- Сервер HQ-SRV должен находиться в ID VLAN 100
- Клиент HQ-CLI в ID VLAN 200
- Создайте подсеть управления с ID VLAN 999
- Основные сведения о настройке коммутатора и выбора реализации разделения на VLAN занесите в отчёт

<br/>

<details>
<summary>Решение</summary>
#### Настройка VLAN для серверов и клиентов


- **VLAN 100 для HQ-SRV:**
  - **На HQ-RTR:**
    ```yuml
    int vl.100
    ip add 192.168.0.62/26
    port ge1
    service-instance vl.100
    encapsulation dot1q 100
    rewrite pop 1
    connect ip interface vl.100
    ```
    - **На HQ-SRV:**
    ```yuml
    nmcli con add type vlan con-name ens34.100 ifname ens34.100 dev ens34 id 100 ip4 192.168.0.2/26 gw4 192.168.0.62
    ```
    
- **VLAN 200 для HQ-CLI:**
  - **На HQ-RTR:**
    ```yuml
    int vl.200
    ip add 192.168.1.78/28
    port ge1
    service-instance vl.200
    encapsulation dot1q 200
    rewrite pop 1
    connect ip interface vl.200
    ex
    wr mem
    ```
    **На HQ-CLI:**
    ``` yuml
    nmcli con add type vlan con-name ens34.200 ifname ens34.200 dev ens34 id 200 ip4 192.168.1.65/28 gw4 192.168.1.78
    ```

    

> **Отчёт:** Сведения по настройке коммутатора и выбору реализации разделения на VLAN занесите в отчёт.

</details>

<br/>

## Задание 5

### Настройка безопасного удаленного доступа на серверах HQ-SRV и BR-SRV

- Для подключения используйте порт 2024
- Разрешите подключения только пользователю sshuser
- Ограничьте количество попыток входа до двух
- Настройте баннер «Authorized access only»

<br/>

<details>
<summary>Решение</summary>
<br/>

Приводим указанные строки в файле **`/etc/openssh/sshd_config`** к следующим значениям (всё должно быть незакомментировано):
```yml
Port 2024
MaxAuthTries 2
PasswordAuthentication yes
Banner /etc/openssh/bannermotd
AllowUsers  sshuser
```
> В параметре **AllowUsers** вместо пробела используется **`Tab`**

<br/>

Создаем файл **`bannermotd`**:
```yml
----------------------
Authorized access only
----------------------
```

<br/>

Перезагружаем службу:
```yml
systemctl restart sshd
```

</details>

<br/>

## Задание 6

### Между офисами HQ и BR необходимо сконфигурировать IP-туннель

- Сведения о туннеле занесите в отчёт

- На выбор технологии GRE или IP in IP

<br/>

<details>
<summary>Решение</summary>
<br/>


Не забудьте чекнуть прописаны ли статические маршруты ip route на роутерах

- **На HQ-RTR:**
  ```yuml
  Interface tunnel.1
  Ip add 172.16.0.1/30
  Ip mtu 1400  
  ip ospf network broadcast  
  ip ospf mtu-ignore  
  Ip tunnel 172.16.4.1 172.16.5.1 mode gre  
  end  
  wr mem  
  Conf t
  Router ospf 1
  Ospf router-id  172.16.0.1
  network 172.16.0.0 0.0.0.3 area 0
  network 192.168.0.0 0.0.0.63 area 0
  network 192.168.1.78 0.0.0.15 area 0
  passive-interface default
  no passive-interface tunnel.1
  ```
- **На BR-RTR:**
  ```yuml
  Interface tunnel.1
  Ip add 172.16.0.2/30
  Ip mtu 1400
  ip ospf mtu-ignore
  ip ospf network broadcast
  Ip tunnel 172.16.5.1 172.16.4.1 mode gre
  end
  Conf t
  Router ospf 1
  Ospf router-id 172.16.0.2
  Network 172.16.0.0 0.0.0.3 area 0
  Network 192.168.2.0 0.0.0.31 area 0
  Passive-interface default
  no passive-interface tunnel.1
  end
  wr mem
  ```

</details>

<br/>

## Задание 7

### Динамическая маршрутизация

● Разрешите выбранный протокол только на интерфейсах в ip туннеле

● Маршрутизаторы должны делиться маршрутами только друг с другом

● Обеспечьте защиту выбранного протокола посредством парольной защиты

● Сведения о настройке и защите протокола занесите в отчёт

<details>
<summary>Решение</summary>
- **Цель:** Обеспечить доступ ресурсов одного офиса к другому посредством протокола link-state (например, OSPF).

- **Настройка аутентификации OSPF на EcoRouter:**

  **На HQ-RTR:**
  ```yuml
  router ospf 1
    area 0 authentication
  interface tunnel.1
    ip ospf authentication-key ecorouter
  wr mem
  ```

  **На BR-RTR:**
  ```yuml
  router ospf 1
    area 0 authentication ex
  interface tunnel.1
    ip ospf authentication-key ecorouter
  wr mem
  ```

> **Отчёт:** Занесите сведения о настройке и защите протокола в отчёт.

---
</details>

<br/>

## Задание 8

### Динамическая трансляция адресов (NAT) 

● Настройте динамическую трансляцию адресов для обоих офисов.

● Все устройства в офисах должны иметь доступ к сети Интернет

<details>
<summary>Решение</summary>
 
- **На HQ-RTR:**
  ```yuml
  conf t
  ip nat pool nat1 192.168.0.1-192.168.0.254
  ip nat source dynamic inside-to-outside pool nat1 overload interface ISP
  ip nat pool nat2 192.168.1.65-192.168.1.79
  ip nat source dynamic inside-to-outside pool nat2 overload interface ISP

 - **На BR-RTR:**
  ```yuml
  conf t
  ip nat pool nat3 192.168.2.2-192.168.2.31
  ip nat source dynamic inside-to-outside pool nat3 overload interface ISP
  ```

#### Создание подсети управления (VLAN 999)

- **На HQ-RTR:**
  ```yuml
  int vl999
  ip add 192.168.0.81/29
  port ge1
  service-instance toSW
  encapsulation untagged
  connect port te1 service-instance toSW
  end
  wr mem
  ```
  - **На HQ-RTR:**
  ```yuml
  conf t
  int ISP
  ip nat outside
  ex
  int vl999
  ip nat inside
  ```
  - **На BR-RTR:**
  ```yuml
  conf t
  int ISP
  ip nat outside
  ex
  int SRV
  ip nat inside
  ```
  

- **Настройка шлюзов на серверах:**
  - **HQ-SRV:** Шлюз – `192.168.0.1/26`
  - **BR-SRV:** Шлюз – `192.168.2.1/27`

---
</details>

<br/>

## Задание 9

### Настройка DHCP-сервера

● Настройте нужную подсеть

● Для офиса HQ в качестве сервера DHCP выступает маршрутизатор HQ-RTR.

● Клиентом является машина HQ-CLI.

● Исключите из выдачи адрес маршрутизатора

● Адрес шлюза по умолчанию – адрес маршрутизатора HQ-RTR.

● Адрес DNS-сервера для машины HQ-CLI – адрес сервера HQ-SRV.

● DNS-суффикс для офисов HQ – au-team.irpo

● Сведения о настройке протокола занесите в отчёт

<details>
 <summary>Решение</summary>
 
- **Для офиса HQ (на HQ-RTR):**
  ```yuml
  en
  conf t
  ip pool dhcpHQ 192.168.1.65-192.168.1.79
  dhcp-server 1
  pool dhcpHQ 1
  domain-name au-team.irpo
  mask 255.255.255.240  
  dns 192.168.0.2    
  gateway 192.168.1.78    
  end  
  wr mem
  ```
- **Клиентом является HQ-CLI (на hq-rtr) :**  
  ```yuml
  conf t
  interface vl.200
  dhcp-server 1
  ```
  </details>
<br/>

## Задание 10
### Настройка DNS для офисов HQ и BR.

● Основной DNS-сервер реализован на HQ-SRV.

● Сервер должен обеспечивать разрешение имён в сетевые адреса устройств и обратно в соответствии с таблицей 2

● В качестве DNS сервера пересылки используйте любой общедоступный DNS сервер

<details>
 <summary>Решение</summary>
 
- **Установка и базовая настройка:**
  ```yuml
  apt-get install -y bind 
  chattr -f +i /etc/resolv.conf
  nano /etc/bind/options.conf
  ```

  ![bind1.png](https://github.com/HatKodGor/exdem2025/blob/main/4.png)
  ![bind2.png](https://github.com/HatKodGor/exdem2025/blob/main/5.png)

  ```yuml
  nano local.conf
  ```
  ![bind3.png](https://github.com/HatKodGor/exdem2025/blob/main/6.png)

  ```yuml
  nano /etc/bind/zone/au-team.irpo.db
  ```
  ![name1.png](https://github.com/HatKodGor/exdem2025/blob/main/7.png)
  
```yuml
nano /etc/bind/zone/168.192.zone
```
![name2.png](https://github.com/HatKodGor/exdem2025/blob/main/8.png)

```yuml
  chown -R root /etc/bind/zone
  chmod 750 /etc/bind/*
  chmod 750 /etc/bind/zone/*
  systemctl restart bind
```
Если выдаёт что нужно смотреть bind.service, то ставьте вместо 750 значение 777

Проверить зоны можно командой (название домена)-checkzone -z

Для полной работоспособности на HQ-CLI нужно установить в качестве dns севрера HQ-SRV:

```bash
  nano /etc/resolv.conf
  ```
![name2.png](https://github.com/HatKodGor/exdem2025/blob/main/9.png)

</details>

<br/>

## Задание 11

### Настройте часовой пояс на всех устройствах, согласно месту проведения экзамена.

<details>

 <summary>Решение</summary> 

```yuml
  timedatectl set-timezone Europe/Moscow - alt linux
  ntp timezone +5 utc  - Ecorouter
  ```
</details>

</details>

<br/>
