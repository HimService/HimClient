# HimClient

[繁體中文](README.md) | [English](README_EN.md)

<blockquote style="color: red;">
  <p><strong>警告！</strong><br>
  我們無法保證HimClient的進階安全性和穩定性，建議僅以測試與體驗之目的使用。</p>
</blockquote>


你可以前往此地查看最新版本的README
https://himservice-docs.himserver.com/#HimClient/intro
## 簡介

HimClient 專案為一個基於Pterodactyl面板的伺服器儀表板專案，旨在為 Pterodactyl 面板延伸出一個供使用者的用戶介面。此專案允許使用者使用 Discord 帳戶登入系統並創建面板帳戶，使使用者可透過 Discord 登入並管理其 Pterodactyl 伺服器資源。儀表板提供多項功能，包括伺服器狀態監控、資源管理、商店系統、用戶方案管理及管理員後台功能，旨在簡化伺服器託管服務的管理與使用流程。

本專案採用前後端架構，後端負責資料處理與邏輯，前端則專注於使用者介面體驗。資料儲存採用 SQLite 資料庫，配置資訊則透過 JSON 檔案進行管理，以確保系統的靈活性。

## 專案架構

本專案主要由以下組件構成：

- **後端 API (Node.js/Express)**:
    - 使用 `server.js` 實現，基於 Express 框架搭建 RESTful API 服務。
    - 負責處理所有來自前端的請求，包括使用者身份驗證、資料庫操作、與 Pterodactyl API 互動等。
    - API 端點涵蓋：你可以[在此](https://himservice-docs.himserver.com/#HimClient/api)查看HimClient的API文檔
    - 資料庫操作使用 SQLite，透過 `sqlite3` 進行互動。
    - 使用 `node-fetch` 與 Pterodactyl API 進行資料交換。
    - 任務排程使用 `node-cron`，例如定期檢查並刪除過期伺服器。

- **前端儀表板 (HTML/CSS/JavaScript)**:
    - 位於 `public` 目錄，採用 HTML、CSS 及 JavaScript 開發。
    - 使用 `index.html` 作為入口，透過 JavaScript 實現路由與頁面渲染。
    - 儲存使用者登入狀態及基本資訊。
    - 頁面結構模組化，包含側邊欄 (`sidebar.js`)、首頁 (`home.js`)、登入頁面 (`login.js`)、儀表板 (`dashboard.js`)、伺服器管理頁面 (`servers.js`)、設定頁面 (`settings.js`)、商店頁面 (`shop.js`)、方案頁面 (`plans.js`)、掛機賺點頁面 (`earn.js`)、禮品卡頁面 (`giftcards.js`)、客服單頁面 (`support.js`)、條款頁面 (`terms.js`)、管理員頁面 (`admin.js`)、404 頁面 (`notfound.js`) 及回調頁面 (`callback.js`) 等。
    - 使用 CSS (`public/css`) 檔案定義頁面樣式，提升使用者介面美觀性與操作體驗。

- **配置檔案 (config.json)**:
    - 儲存系統的各項配置資訊，包括：
        - 伺服器基本設定 (主機地址、端口)。
        - Pterodactyl 面板 API 金鑰與 URL。
        - Discord 應用程式憑證 (client ID, client secret, redirect URI)。
        - 使用者方案配置。
        - 續約系統設定。
        - 商店物品配置。
        - 頁面文字內容及其他靜態資源設定。
    - 專案啟動時載入，並在後端前端中使用。

- **資料庫 (database.db)**:
    - 使用 SQLite 資料庫檔案儲存使用者資料、伺服器資訊及禮品卡資料。
    - 資料表結構包括 `users` (使用者表), `servers` (伺服器表), 及 `giftcards` (禮品卡表)。

- **其他檔案**:
    - `README.md`: 專案說明文件。
    - `API.md`: API 文件，詳細描述所有後端 API 端點。
    - `egg.json`, `server.json`, `shop.json`, `terms.json`: 儲存伺服器核心、伺服器位置、商店物品及使用條款等 JSON 資料。

## 安裝

以下步驟將指導您完成 HimClient 專案的安裝與設定：

### 條件

在開始安裝之前，請確保您的系統已安裝以下軟體：

1. **Node.js**: 建議使用 Node.js 16.0 或更高版本。您可以從 [Node.js 官網](https://nodejs.org/) 下載並安裝。
2. **npm (Node Package Manager)**: npm 通常會隨 Node.js 一起安裝。請確保 npm 版本為 7.0 或更高版本。

### 安裝步驟

1. **下載專案**:

   您可以直接下載 ZIP 壓縮檔的方式取得專案。

   **下載 ZIP 壓縮檔**:

   您可以從專案倉庫頁面下載 ZIP 壓縮檔，解壓縮至您的目錄。

2. **安裝 Node.js 依賴**:

   在專案根目錄下，執行以下命令以安裝專案所需的 Node.js 模組：

   ```bash
   npm install
   ```

   此命令將根據 `package.json` 檔案中的定義，自動安裝依賴。

3. **設定 `config.json` 檔案**:

   你可以[在此](https://himservice-docs.himserver.com/#HimClient/set-config)查看`config.json`、`server.json`等配置檔例檔

   **重要**:

   - 請務必將 `secret` 替換為您自訂的強密碼，用於 API 請求的身份驗證。
   - 在 [Discord Developer Portal](https://discord.com/developers/applications) 建立 Discord 應用程式，並取得 `client_id` 及 `client_secret`，並設定正確的 `redirect_uri`。
   - 填寫您的 Pterodactyl 面板 URL 及 API 金鑰。Application API 金鑰需在 Pterodactyl 後台管理員介面生成，Client API 金鑰可在使用者設定中生成。

4. **初始化資料庫**:

   專案首次啟動時，將自動建立 SQLite 資料庫檔案 `database.db` 及必要的資料表結構。您無需手動建立資料庫。

5. **啟動伺服器**:

   在專案根目錄下，執行以下命令以啟動伺服器：

   ```bash
   npm start
   ```

   或

   ```bash
   node server.js
   ```

   伺服器成功啟動後，您將在終端機看到系統上線的訊息，並顯示伺服器運行的地址與端口。

6. **存取儀表板**:

   開啟瀏覽器，訪問伺服器所運行的網址 (預設為 `http://localhost:8080`)，即可開始使用 HimClient 儀表板。

完成以上步驟後，您已成功安裝並設定 HimClient 專案。如有任何問題，請參考專案文件或尋求技術支援。

## 已知問題

## 開發與貢獻

### 報告問題

如果發現 bug 或有功能建議，請在 GitHub 創建 Issue，提供詳細描述和重現步驟。

## 許可證

請閱讀 `LICENSE` 文件。
