# NDEF2HEX 轉換器

專為 Proxmark3 使用者設計的 NDEF to HEX 轉換工具

線上使用: [https://agong.tech/ndef2hex](https://agong.tech/ndef2hex)

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![HTML](https://img.shields.io/badge/HTML-5-orange.svg)
![CSS](https://img.shields.io/badge/CSS-3-blue.svg)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6-yellow.svg)

## 簡介

NDEF2HEX 是一個簡單易用的靜態網頁工具,可以將網址 (URL) 轉換成 NDEF 格式的 HEX 碼,專門用於 Proxmark3 寫入 NFC 卡片。

## 功能特色

- **雙協定支援**: 支援 HTTP 和 HTTPS 兩種協定
- **即時轉換**: 輸入網址即可快速轉換為 HEX 格式
- **一鍵複製**: 輕鬆複製 HEX 碼或完整的 PM3 指令
- **即時預覽**: 顯示完整的 URL 預覽
- **操作提示**: 提供詳細的使用說明和注意事項
- **現代化介面**: 美觀的藍色漸層設計
- **響應式設計**: 支援各種螢幕尺寸

## 使用方法

### 線上使用
1. 訪問 [https://agong.tech/ndef2hex](https://agong.tech/ndef2hex) 或直接在瀏覽器中開啟 `ndef-to-hex.html`
2. 選擇通訊協定 (HTTP 或 HTTPS)
3. 輸入您的網址 (例如: `google.com`)
4. 點擊「轉換為 HEX」按鈕
5. 複製生成的指令並在 Proxmark3 中執行

### 範例

**輸入:**
- 協定: HTTPS
- 網址: `google.com`

**輸出:**
```
HEX: 030FD1010B5504676F6F676C652E636F6DFE
PM3 指令: hf mf ndefwrite -d 030FD1010B5504676F6F676C652E636F6DFE
```

## Proxmark3 使用說明

### 對於 NTAG 系列卡片 (NTAG213/215/216)
直接寫入即可:
```bash
hf mf ndefwrite -d [生成的HEX碼]
```

### 對於 Mifare Classic 卡片
需要先格式化:
```bash
# 1. 格式化卡片
hf mf ndefformat

# 2. 寫入 NDEF 資料
hf mf ndefwrite -d [生成的HEX碼]
```

## 技術細節

### NDEF URI Record 格式
- **TLV Type**: `03` (NDEF Message)
- **TNF**: `0xD1` (Well-known type, MB=1, ME=1, SR=1)
- **Type**: `U` (0x55, URI Record)
- **URI Identifier**: 
  - `0x03` = `http://`
  - `0x04` = `https://`
- **TLV Terminator**: `FE`

### 瀏覽器相容性
- Chrome / Edge (推薦)
- Firefox
- Safari
- Opera

## 專案結構

```
NDEF2HEX/
├── ndef-to-hex.html    # 主要網頁檔案
└── README.md           # 說明文件
```

## 適用場景

- NFC 名片
- 智慧海報
- 產品標籤
- 導覽系統
- 行銷活動
- 個人網站分享

## 注意事項

1. **卡片容量限制**: 確保您的網址長度不超過卡片容量
   - NTAG213: 144 bytes
   - NTAG215: 504 bytes
   - NTAG216: 888 bytes

2. **網址格式**: 請輸入不含協定前綴的網址 (例如: `google.com` 而非 `https://google.com`)

3. **卡片格式化**: 非 NTAG 卡片需要先執行 `hf mf ndefformat` 格式化

## 貢獻

歡迎提交 Issue 或 Pull Request!

## 授權

本專案採用 MIT 授權條款 - 詳見 [LICENSE](LICENSE) 檔案

## 作者

**Agong**
- GitHub: [@Agong88](https://github.com/Agong88)
- Website: [agong.tech](https://agong.tech)

## 致謝

- 感謝 Proxmark3 社群的支援
- NFC Forum 的 NDEF 規範文件

## 版本歷史

### v1.0.0 (2025-10-26)
- 初始版本發布
- 藍色主題設計
- HTTP/HTTPS 協定支援
- 一鍵複製功能
- 格式化提醒

---

如果這個專案對您有幫助,請給它一顆星星!
