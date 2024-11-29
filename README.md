Wifi-SmartWaterHeater-ESP8266
專案概述
此專案旨在透過 ESP8266 控制家用熱水器，結合無線網路、自動化控制及數據監控，讓使用者能夠遠程監控和管理熱水器的運行狀態。本專案的特色包括定時模式、自動溫度調節和手動控制加熱器等多種模式，方便用戶根據不同需求進行調整。

功能
支援手動控制加熱器的開關
支援自動目標水溫調整
提供定時加熱模式，根據預設時間自動啟動/停止加熱
通過 Web 伺服器監控加熱器狀態
使用 DHT11 感測器來監控環境溫濕度和水溫
支援通過 OTA 進行無線韌體更新
支援顯示當前加熱時間和剩餘加熱時間
硬體需求
ESP8266 (NodeMCU v2)
DHT11 感測器 (用於測量溫度和濕度)
相關繼電器模組 (控制熱水器)
軟體需求
ESPHome
YAML 配置檔案 (包含此專案的所有自定義設定)
無線網路環境，用於控制和監控設備
安裝與設定
克隆專案：

bash
複製程式碼
git clone https://github.com/yourusername/Wifi-SmartWaterHeater-ESP8266.git
cd Wifi-SmartWaterHeater-ESP8266
修改配置檔案： 打開 hwater.yaml 配置檔案，根據你的環境修改以下參數：

wifi.ssid：輸入你的 WiFi 名稱
wifi.password：輸入你的 WiFi 密碼
ota.password：輸入自定義的 OTA 更新密碼
編譯與燒錄： 使用 ESPHome 編譯並將配置燒錄至 ESP8266：

bash
複製程式碼
esphome run hwater.yaml
設備連接與監控： 上傳完成後，ESP8266 會連接到你指定的 WiFi，你可以透過 Web 伺服器訪問設備，監控熱水器狀態。

目錄結構
bash
複製程式碼
Wifi-SmartWaterHeater-ESP8266/
├── hwater.yaml           # 主配置檔案
├── LICENSE               # 開源授權
├── README.md             # 專案介紹文件 (即此文件)
└── assets/               # 包含圖片與其他資源
使用說明
手動模式：通過啟動 Manual Heater Trigger 來手動開啟或關閉加熱器。
自動調整模式：開啟 Auto Target Temperature Adjustment，系統將根據環境溫度自動調整目標水溫。
定時模式：啟用 Enable Timer Mode 並設定開始和結束時間，熱水器將自動在特定時間段內啟動。
注意事項
請務必確認加熱器的接線安全。
當自動加熱或手動加熱模式啟動時，請監控水溫，避免過熱。
貢獻
歡迎任何貢獻！如果你有建議或改進想法，請透過 GitHub Issue 提出，或直接發送 Pull Request。

授權
此專案以 MIT License 授權，歡迎自由使用、修改及分發。
