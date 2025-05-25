
# 💧 Умный Zigbee-счётчик воды для Home Assistant (ESP32-H2)

## 🔍 Что это такое?

Готовое устройство на базе **ESP32-H2**, подключённое к импульсному датчику воды. Передаёт данные в **Home Assistant** по протоколу **Zigbee** и используется для контроля количества израсходованной питьевой воды (например, из фильтра обратного осмоса).

📌 Основные цели:
- Учёт объёма выпитой/отфильтрованной воды
- Напоминание о необходимости замены фильтров
- Интеграция с Яндекс Алисой, Telegram и другими помощниками

## ⚙️ Возможности

- Поддержка Zigbee (через `esp-zigbee-sdk`)
- Подсчёт воды: 1 импульс = 1 литр (можно изменить)
- Zigbee кластеры:
  - `Metering` — объём воды
  - `OnOff` — сброс счётчика через Home Assistant
- Хранение текущего значения в энергонезависимой памяти (NVS)
- Поддержка Zigbee2MQTT и ZHA

## 📥 Скачать прошивку

Три файла для прошивки:
- `bootloader.bin` – 📎 Скачать
- `partition-table.bin` – 📎 Скачать
- `zb_water_meter.bin` – 📎 Скачать

## 🪟 Как прошить (Windows)

1. Установи [Flash Download Tool от Espressif](https://www.espressif.com/en/support/download/other-tools)
2. Подключи ESP32-H2 к компьютеру по USB
3. Запусти `flash_download_tool`, выбери чип `ESP32-H2`
4. Укажи:
   - `bootloader.bin` → **адрес 0x0**
   - `partition-table.bin` → **адрес 0x8000**
   - `zb_water_meter.bin` → **адрес 0x10000**
5. Укажи COM-порт, нажми **Start**
6. Дождись окончания и перезагрузи плату

## 🐧 Как прошить (Linux / Mac)

1. Установи `esptool`:
```bash
pip install esptool
```
2. Найди порт устройства:
```bash
ls /dev/ttyUSB*
```
3. Запусти прошивку:
```bash
esptool.py --chip esp32h2 --port /dev/ttyUSB0 --baud 460800 write_flash -z \
  0x0 bootloader.bin \
  0x8000 partition-table.bin \
  0x10000 zb_water_meter.bin
```

## 🏠 Интеграция в Home Assistant

1. Добавь устройство в Zigbee-сеть (ZHA или Zigbee2MQTT)
2. В интерфейсе появятся:
   - Сенсор объёма воды (литры)
   - Переключатель сброса счётчика
3. Настрой автоматизации:
   - Уведомления об объёме (через Telegram, Алису)
   - Напоминание о замене фильтра через заданное количество литров

---

# 💧 Smart Zigbee Water Meter for Home Assistant (ESP32-H2)

## 🔍 What is it?

This firmware turns your **ESP32-H2** board into a **Zigbee-based water flow counter**, designed to monitor **filtered water** consumption (e.g., reverse osmosis). It integrates with **Home Assistant** to help you track how much water you consume and when to change your filters.

## ⚙️ Features

- Zigbee support via `esp-zigbee-sdk`
- 1 pulse = 1 liter (can be configured)
- Zigbee clusters:
  - `Metering` – water volume (liters)
  - `OnOff` – reset the counter from HA
- Non-volatile storage of current value
- Works with Zigbee2MQTT or ZHA

## 📥 Firmware Files

Three `.bin` files required:
- `bootloader.bin` – 📎 Download
- `partition-table.bin` – 📎 Download
- `zb_water_meter.bin` – 📎 Download

## 🪟 Flashing on Windows

1. Download [Flash Download Tool from Espressif](https://www.espressif.com/en/support/download/other-tools)
2. Connect ESP32-H2 to your PC
3. Launch the tool and select `ESP32-H2`
4. Add:
   - `bootloader.bin` → **@ 0x0**
   - `partition-table.bin` → **@ 0x8000**
   - `zb_water_meter.bin` → **@ 0x10000**
5. Set COM port and press **Start**
6. Reboot the device when done

## 🐧 Flashing on Linux / Mac

1. Install `esptool`:
```bash
pip install esptool
```
2. Find device port:
```bash
ls /dev/ttyUSB*
```
3. Flash:
```bash
esptool.py --chip esp32h2 --port /dev/ttyUSB0 --baud 460800 write_flash -z \
  0x0 bootloader.bin \
  0x8000 partition-table.bin \
  0x10000 zb_water_meter.bin
```

## 🏠 Home Assistant Integration

1. Pair the device via Zigbee2MQTT or ZHA
2. You'll see:
   - Water volume sensor (liters)
   - Reset switch
3. Setup automations:
   - Alerts for water consumption
   - Filter replacement reminder
