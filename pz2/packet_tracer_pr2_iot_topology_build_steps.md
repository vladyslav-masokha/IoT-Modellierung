# Як створити файл `pr2_iot_solar_topology.pkt` у Cisco Packet Tracer

Цей файл потрібен тільки якщо викладач окремо просить здати `.pkt/.pka`. На цьому комп’ютері Cisco Packet Tracer не знайдено, тому валідний `.pkt` автоматично створити неможливо: формат Packet Tracer закритий і зберігається самою програмою через `File -> Save As`.

## 1. Створення топології

Відкрити Cisco Packet Tracer і додати на робочу область:

- `PC`
- `Server`
- `Switch`
- `PT-Solar Panel`
- `PT-Power Meter`
- `PT-Battery`
- `LED1`
- `LED2`
- `LED3`
- `LED4`

## 2. IoT Custom Cable

Підключити через `Connections -> IoT Custom Cable`:

| Пристрій 1 | Порт 1 | Пристрій 2 | Порт 2 |
|---|---:|---|---:|
| `PT-Solar Panel` | `D0` | `PT-Power Meter` | `D0` |
| `PT-Battery` | `D0` | `PT-Power Meter` | `D1` |
| `LED1` | `D0` | `PT-Battery` | `D1` |
| `LED2` | `D0` | `PT-Battery` | `D2` |
| `LED3` | `D0` | `PT-Battery` | `D3` |
| `LED4` | `D0` | `PT-Battery` | `D4` |

## 3. Ethernet

Підключити через `Connections -> Copper Straight-Through`:

| Пристрій | Порт пристрою | Порт комутатора |
|---|---:|---:|
| `PC` | `FastEthernet0` | `Fa0/1` |
| `Server` | `FastEthernet0` | `Fa0/2` |
| `PT-Solar Panel` | `GigabitEthernet0` | `Fa0/3` |
| `PT-Power Meter` | `FastEthernet0` | `Fa0/4` |
| `PT-Battery` | `FastEthernet0` | `Fa0/5` |

## 4. Server

Налаштувати сервер:

- IP-адреса: `1.0.0.1`
- DHCP: `On`
- IoE / Registration Server: `On`
- User: `admin`
- Password: `admin`

## 5. DHCP на IoT-пристроях

Увімкнути DHCP:

- `PT-Solar Panel -> Config -> GigabitEthernet0 -> DHCP`
- `PT-Power Meter -> Config -> FastEthernet0 -> DHCP`
- `PT-Battery -> Config -> FastEthernet0 -> DHCP`

Очікуваний приклад адрес:

- `PC`: `1.0.0.2`
- `PT-Solar Panel`: `1.0.0.3`
- `PT-Power Meter`: `1.0.0.4`
- `PT-Battery`: `1.0.0.5`

## 6. Реєстрація IoT-пристроїв

Для `PT-Solar Panel`, `PT-Power Meter`, `PT-Battery`:

1. Відкрити пристрій.
2. Перейти `Config -> Settings`.
3. У `IoE Server` вибрати `Remote Server`.
4. Ввести `Server Address: 1.0.0.1`.
5. Ввести `User Name: admin`.
6. Ввести `Password: admin`.
7. Натиснути `Connect`.

## 7. Перевірка

На ПК:

1. Відкрити `Desktop -> Web Browser`.
2. Перейти на `1.0.0.1`.
3. Увійти як `admin/admin`.
4. Переконатися, що відображаються:
   - `Connected Solar Panel`
   - `Connected Power Meter`
   - `Connected Battery`

## 8. Збереження файлу для здачі

Після перевірки вибрати:

`File -> Save As -> pr2_iot_solar_topology.pkt`

Зберегти файл у цій папці:

`C:\Users\Vladyslav Masokha\Desktop\university\Моделювання ІоТ\Практичні\pz2`
