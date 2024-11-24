# WiFi-Heater-ESP8266

## 專案概述
WiFi-Heater-ESP8266 是一個基於 ESP8266 WiFi 模組的智能熱水器控制系統，旨在通過物聯網技術提升熱水器的便捷性和能源效率。此專案允許用戶通過 WiFi 遠端控制水溫並監測熱水器的運行狀況，實現智能化家居體驗。

## 系統架構
此專案的系統架構主要由 ESP8266 WiFi 模組、熱水器控制電路及相關感應器組成。ESP8266 負責將熱水器連接至本地 WiFi 網絡，用戶可以透過手機或電腦發送指令以控制熱水器的開關、調整水溫等功能。

- **ESP8266 模組**：用於連接到 WiFi，處理所有網絡請求及控制指令。
- **溫度感應器**：負責測量水溫，並將數據反饋給 ESP8266，以便進行控制。
- **控制電路**：通過繼電器或其他開關裝置實現熱水器的開關控制。
- **用戶界面**：用戶可以透過 Web 應用程式或專屬手機應用來控制熱水器並查看目前的水溫狀態。

## 使用方法
### 硬體設置
1. **準備硬體**：
   - 一台 ESP8266 開發板（如 NodeMCU）
   - 溫度感應器（如 DS18B20）
   - 繼電器模組，用於控制熱水器的電源開關
   - 熱水器
2. **連接 ESP8266**：
   - 將溫度感應器連接到 ESP8266，讀取水溫數據。
   - 將繼電器連接到 ESP8266，並將熱水器的電源通過繼電器控制。

### 軟體設置
1. **開發環境**：
   - 使用 Arduino IDE 或 PlatformIO 來編寫 ESP8266 的控制程式碼。
   - 安裝 ESP8266 開發板擴展包，配置相關的驅動。
2. **程式碼上傳**：
   - 編寫程式碼以處理 WiFi 連接、HTTP 請求，並實現控制邏輯。
   - 以下是 `hwater.yaml` 的程式碼內容，供您參考：

```yaml
esphome:
  name: hwater
  friendly_name: HWater

esp8266:
  board: esp01_1m

logger:

api:
  encryption:
    key: "7uoAmbYwHvWNQA3xCXsXaJWoQiAf3OJQb+6reWqCU8o="

ota:
  platform: esphome
  password: "ef6e1fd2688b16bda2ac563f214e8f16"

wifi:
  ssid: "ShangHome"
  password: "61389038"
  ap:
    ssid: "Hwater Fallback Hotspot"
    password: "61389038"
  manual_ip:
    static_ip: "192.168.31.84"
    gateway: "192.168.31.1"
    subnet: "255.255.255.0"
    dns1: "192.168.31.1"

web_server:
  port: 80

globals:
  - id: heater_timer_remaining
    type: int
    restore_value: False
    initial_value: '0'

switch:
  - platform: gpio
    pin: GPIO2
    name: "Water Heater Switch"
    id: heater
    restore_mode: RESTORE_DEFAULT_OFF
  - platform: template
    name: "04_Enable Timer Mode"
    id: timer_mode
    optimistic: True
    turn_on_action:
      - lambda: |
          ESP_LOGD("main", "Timer Mode set to: ON");
          auto now = id(sntp_time).now();
          if (now.is_valid()) {
            int start_hour = 7;
            int end_hour = 23;
            float current_temp = id(dht11_temperature).state;
            float target_temp = id(target_temperature).state;
            bool in_timer_range = (now.hour >= start_hour && now.hour < end_hour);
            if (in_timer_range && current_temp < target_temp) {
              id(heater).turn_on();
              ESP_LOGD("main", "Timer mode activated immediately: Heater ON, current temp: %f, target temp: %f", current_temp, target_temp);
            }
          }
    turn_off_action:
      - lambda: |
          id(timer_mode).publish_state(false);
          ESP_LOGD("main", "Timer Mode set to: OFF");
          id(heater).turn_off();

# 更多程式碼...（省略部分內容）
```

3. **WiFi 設定**：
   - 配置 WiFi 名稱和密碼，將 ESP8266 連接到本地網絡。

### 操作系統
1. **連接到熱水器控制面板**：
   - 開啟手機或電腦上的瀏覽器，輸入 ESP8266 的 IP 地址。
   - 進入控制介面，查看水溫、開啟或關閉熱水器，設定目標溫度。
2. **遠端控制與自動化**：
   - 可選擇設定每日排程，例如早上自動開啟熱水器並加熱到預設溫度。

## 範例圖片與圖表
下面是一些系統設置的範例圖片，幫助您了解如何進行硬體連接和軟體配置：

![image](https://github.com/user-attachments/assets/4db3814d-b06a-4ab1-8606-4b7d558d3727)

## 版本歷史
- **v1.0**: 初始版本，實現 WiFi 連接與基本熱水器開關功能。
- **v1.1**: 增加溫度感應與自動調節功能。

## 許可證
此專案基於 MIT 許可證開源，您可以自由使用、修改和分發，但需要保留原作者的版權聲明。

