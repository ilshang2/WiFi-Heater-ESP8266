```
HWater 控制系統

專案描述

HWater 控制系統是一個基於 ESP8266 的智慧水溫控制解決方案。透過 ESPHome 平台，該系統能夠自動調整目標水溫，根據環境溫度進行智慧化控制，同時提供手動控制和定時模式功能，確保水溫始終保持在理想範圍內。

功能特點

- 自動目標水溫調整：根據環境溫度自動調整目標水溫，節能又高效。
- 手動控制：允許使用者手動啟動或停止加熱器，並設定加熱持續時間。
- 定時模式：設定特定的啟動和停止時間，自動控制加熱器運行。
- 即時監控：實時顯示當前水溫、環境溫度、濕度、加熱器狀態及剩餘加熱時間。
- 遠端管理：透過內建的 Web Server，使用者可在網頁界面上進行配置和監控。

硬體需求

- ESP8266 模組（如 ESP-01，1MB Flash）
- DHT11 溫濕度感測器
- 水溫感測器（連接至 ADC 引腳 A0）
- 繼電器模組（控制加熱器，連接至 GPIO14）
- 電源供應（根據 ESP8266 和繼電器模組的需求）
- 連接線材和面包板（或其他電路板）

軟體需求

- ESPHome（版本 2024.11.1）
- Arduino IDE 或 PlatformIO（可選，用於進一步自訂）
- GitHub 帳戶（選用，用於版本控制與分享）

安裝指南

1. 硬體連接

按照下表將各元件連接至 ESP8266：

| 元件                | ESP8266 引腳 |
|---------------------|--------------|
| DHT11 溫濕度感測器  | GPIO4        |
| 水溫感測器（ADC）    | A0           |
| 繼電器模組          | GPIO14       |
| 電源供應            | VCC & GND    |

2. 安裝 ESPHome

確保您已安裝 ESPHome。如果尚未安裝，可以參考 ESPHome 官方文檔進行安裝。

3. 配置 ESPHome

將提供的 `hwater.yaml` 配置文件保存至 ESPHome 配置目錄下。

4. 編譯並上傳

使用 ESPHome Dashboard 或命令行工具編譯並上傳配置至 ESP8266。

```bash
esphome run hwater.yaml
```

5. 設定 Wi-Fi

首次啟動時，ESP8266 會啟動 AP 模式。連接至 `HWater Fallback Hotspot` 並通過瀏覽器訪問 `192.168.4.1` 進行 Wi-Fi 設定。

使用說明

1. Web 界面

配置完成後，透過設備連接的 Wi-Fi 網絡，使用瀏覽器訪問 ESP8266 的 IP 地址（通常在路由器中查詢）即可進入 Web 界面，進行以下操作：

- 查看狀態：檢視當前水溫、環境溫度、濕度、加熱器狀態及剩餘加熱時間。
- 設定目標溫度：調整目標水溫，系統會自動根據環境溫度進行調整。
- 手動控制：啟動或停止加熱器，並設定手動加熱持續時間。
- 定時設定：設定加熱器的啟動和停止時間，系統將根據設定自動控制。

2. 手動加熱

啟動手動加熱觸發開關，系統將啟動加熱器並在設定的時間後自動關閉。

3. 定時模式

設定定時開始和結束時間，系統將在指定的時間段內自動啟動或停止加熱器。

目錄結構

```
hwater/
├── hwater.yaml          # ESPHome 配置文件
├── www/                 # （已刪除）自定義的 Web 文件
│   ├── index.html
│   ├── styles.css
│   └── script.js
└── README.md            # 本文件
```

常見問題

1. 編譯錯誤

確保 `hwater.yaml` 配置文件中的註釋使用 `//` 而非 `#`，以符合 C++ 的語法規則。

2. 感測器讀數不準確

- 檢查感測器連接是否正確。
- 確保感測器工作在合適的電壓範圍內。
- 定期校準感測器以維持讀數準確性。

3. 加熱器無法啟動

- 確認繼電器模組與加熱器連接正確。
- 檢查 GPIO14 是否正確配置並能夠控制繼電器。
- 確認加熱器本身無故障。

貢獻

歡迎任何形式的貢獻！請提交問題報告或拉取請求，以改善此專案。

授權

本專案採用 MIT 授權。

聯繫方式

如有任何問題或建議，請在 GitHub Issues 中提出，或通過電子郵件聯繫我。

---

感謝您使用 HWater 控制系統！希望這個專案能夠幫助您實現智慧水溫管理。如果您覺得這個專案對您有幫助，請考慮在 GitHub 上給予 Star 支持。😊
```
