---
name: christ-sheep-gospel-action
description: 基督的羊福音的行動 — 管理及維護 G12 同工會網頁、Firebase 資料庫連動與 FormSubmit 自動發信系統。說「基督的羊」「福音的行動」「更新點餐頁面」時載入。
---

# 基督的羊福音的行動 (G12 網頁維護與連動指南)

本技能指引未來的 AI 代理人如何安全且一致地維護與更新 G12 同工會網頁（[index.html](file:///c:/Users/User/中三區G12/index.html)）、其後端的 Firebase Firestore 資料庫同步，以及 FormSubmit 電子郵件自動發送系統。

## 🎯 觸發條件

當使用者要求：
- 更新同工會點餐網頁或修改主菜選項。
- 檢查或修改與 Firebase Firestore（`mydesignProject`）的連動。
- 更新或修改電子郵件自動發送邏輯及收件人信箱。
- 優化點餐表單的互動體驗（防重複點擊、欄位重設等）。

---

## 🛠️ 維護程序與規範

### 1. Firebase Firestore 資料庫連動規範
- **專案配置**：必須連接至 `mydesignProject` (專案 ID: `mydesignproject-f22d5`)。
- **資料集合**：點餐資料必須同步至名為 **`lifebread`** 的資料庫集合。
- **雙語寫入**：文件寫入時，請確保同時寫入中英文欄位以利相容性：
  - `姓名` / `name`：登記姓名 (同時作為 document ID 以便進行覆蓋修改)
  - `套餐` / `meal`：`"舒食套餐組"`
  - `主菜` / `main`：所選主菜 (如 `和牛牛排`)
  - `created_at` / `timestamp`：時間戳記
- **監聽同步**：頁面載入時需執行 `loadOrdersFromFirebase()`。該呼叫必須放置於 `db` 實例初始化**之後**，以便即時更新看板。

### 2. FormSubmit 電子郵件發送規範
- **背景發送**：使用 `fetch` 向 `https://formsubmit.co/ajax/taiwan.kwei@gmail.com` 發送 POST 請求。
- **CC 抄送**：必須在 JSON payload 中加入 `_cc: "taiwan.kwei@ceci.com.tw,g0306@ceci.com.tw"`。
- **排版範本**：設置 `_template: "table"` 將信件內容自動排版為 HTML 表格。
- **降級備用 (Fallback)**：若 `fetch` 失敗，必須呼叫 `fallbackMailto`，透過隱藏的 anchor 點擊來啟用本機 `mailto:` 信件草稿。

### 3. UI 互動體驗與安全機制
- **防重複點擊 (Double-click Block)**：按下「送出」按鈕時，必須**立即將按鈕禁用 (`disabled = true`)** 並更變文字為 `⏳ 正在傳送...`，完成後（modal 關閉後）再延遲恢復。
- **條件式欄位重設**：
  - 開啟「立即點餐」：調用 `openOrderModal(true)` 清空姓名與主菜單選按鈕。
  - 開啟「修改餐點」：調用 `openOrderModal(false)` 載入本機 `localStorage` 已存的姓名與前次選擇。
- **即時成功回應**：點餐送出後，背景執行非同步寫入與發信的同時，**立即彈出 `alert('點餐成功，謝謝')`**，不讓網路延遲阻礙使用者體驗。

### 4. 歷史內容維持
- 導覽列第四項 tab 必須維持正字 `離塵不離城`。
- 第一片影片的預覽圖需連結至 `https://img.youtube.com/vi/RoJQjmk4CrM/maxresdefault.jpg` 以防 404。

---

## 📂 參考檔案
- [index.html](file:///c:/Users/User/中三區G12/index.html)
- [walkthrough.md](file:///C:/Users/User/.gemini/antigravity/brain/ec94d423-3a3e-473a-ac80-c0a0ca32206e/walkthrough.md)
