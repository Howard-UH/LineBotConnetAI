# 透過 Make 與 AI 打造 LINE 自動回覆客服機器人

本指南將帶你一步步使用 Make 和 OpenRouter 上的免費 AI 模型，打造一個能夠自動回覆訊息的 LINE 客服機器人。即使你沒有程式背景，也能輕鬆完成。

## 核心工具

* **Make**：一個強大的自動化工具，用於串接不同的應用服務。
* **OpenRouter**：一個聚合了多種 AI 模型的服務，方便你選擇和使用。
* **LINE 開發者帳號**：用於建立 LINE 官方帳號與設定 Messaging API。

---

## 建立步驟

### 1. 註冊並設定 Make 帳號
- 選擇登入方式（例如：Google 帳號）。
- 填寫基本資料與問卷。
- 建立一個新的「場景」（Scenario），這將是我們機器人的工作流程。

### 2. 建立 Make 的 Webhook 模組
- 在 Make 場景中，新增一個 **Webhook** 模組。
- 這個模組的功用是接收來自 LINE 的訊息。
- 設定 Webhook 名稱，並取得 Webhook 網址。這個網址稍後會貼到 LINE 的設定中。

### 3. 設定 LINE 開發者帳號與官方帳號
- 前往 [LINE 開發者頁面](https://developers.line.biz/) 並登入。
- **建立 Provider**：這是你的應用程式開發者名稱。
- **建立 Messaging API Channel**：這會同時建立一個專屬的 LINE 官方帳號。
- 進行簡訊認證以啟用帳號。
- 在 LINE 官方帳號的管理後台，設定基本資料。
- **開啟聊天功能與 Webhook 功能**：
    - 在 LINE 官方帳號後台，關閉「自動回應訊息」，開啟「Webhook」。
    - 在 Messaging API 的設定頁面，將 Make 產生的 **Webhook 網址** 貼上。
    - 啟用 `Use Webhook` 功能，這樣當有人傳送訊息時，LINE 才會將訊息轉發給 Make。

### 4. 串接 OpenRouter 的 AI 模型
- 前往 [OpenRouter 網站](https://openrouter.ai/) 並註冊登入。
- **建立 API Key** 並複製，這將是 Make 連接 AI 模型的金鑰。
- 在 Make 場景中，新增一個 **OpenRouter** 模組。
- 在設定中，貼上你的 API Key。
- 選擇一個免費的 AI 模型（例如：Google 的模型）。
- 設定訊息來源為 LINE Webhook 收到的文字內容。

### 5. 設定 LINE 回覆模組
- 在 Make 場景中，新增一個 **LINE** 模組，並選擇 `Send a Reply Message`。
- **建立 LINE 連接**：
    - 需要填入 **Channel Access Token**，此金鑰可從 LINE 開發者後台取得。
- 設定 **Reply Token**：將這個值設定為 Webhook 收到的 `Reply Token`，這樣 LINE 才知道要回覆哪一個使用者。
- 設定回覆訊息內容為 OpenRouter AI 模型產生的文字。

### 6. 測試與啟用
- 在 Make 中，點擊 `Run once` 進行單次測試。
- 用你的 LINE 帳號向官方帳號傳送訊息，確認 AI 是否能正確回覆。
- 測試成功後，將 Make 的執行頻率設定為 `Immediately` 並啟用，讓機器人可以永久運行。

### 7. 進階設定：客製化 AI 回覆風格與知識庫

- **客製化回覆風格**：在 OpenRouter 模組中，於訊息內容後方加入指令，例如要求 AI 回覆「友善、活潑，或加入表情符號」，以打造獨特的助理風格。
- **專屬知識庫**：限定 AI 只能回覆特定網頁或 Google 文件中的資訊，建立一個專屬的客服知識庫，讓回覆更精準。

### 備註
- Make 的免費方案有每月 1000 次的操作限制。
- 每次使用者傳送訊息，會觸發 Webhook、OpenRouter 和 LINE 回覆這三個模組，因此大約可處理 **300 多則訊息**。
- 影片強調，透過這種方式，即使不懂程式，也能輕鬆建立一個能理解問題、自動回覆的 LINE AI 助理，可應用於客服、行銷資訊提供等場景。
