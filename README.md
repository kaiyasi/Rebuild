# 校園匿名平台重建計畫書

## **1. 專案概述**
本專案為**匿名校園討論平台**，提供匿名發文、管理員審核、刪文請求、標籤分類、社群平台整合（Discord / IG）等功能，並確保內容安全與使用者隱私。

- **前端**：Vue 3 + Vite + Tailwind CSS + Pinia
- **後端**：Laravel 12 + MySQL / PostgreSQL
- **媒體存儲**：Discord API（圖片/影片上傳）
- **第三方服務**：
  - Google OAuth（管理員登入）
  - Instagram API（美宣發佈）
  - AI NLP（推薦標籤 + 過濾違規內容）

---

## **2. 角色與職責**
| 角色 | 職責 |
|------|--------------------------------------------------|
| **匿名使用者** | 無需登入，可發文、瀏覽文章、提交刪文請求 |
| **版主** | 最高權限，管理所有功能、網站設計、權限分配 |
| **美宣** | 負責貼文排版設計、網站美觀調整、IG 貼文管理 |
| **審文** | 負責文章審核、決定標籤、管理刪文請求 |
| **開發者** | 系統維護與功能開發（需版主許可才能查看機密資訊） |

---

## **3. 主要功能**
### **3.1 前台（匿名使用者）**
1. **首頁 (`/`)**
   - 版規確認通知
   - 手機版：僅顯示發文
   - 電腦版：貼文輪播 + 公告
2. **發文 (`/post`)**
   - Markdown 編輯器
   - 圖片/影片上傳（儲存到 Discord）
   - AI 過濾 + 人工審核
3. **文章頁 (`/post/:id`)**
   - 顯示完整內容
   - 點讚 / 回應
   - 提交刪文請求
4. **刪文申請 (`/report`)**
   - 提交文章編號 + 刪文理由
   - Email & Discord 通知管理員
5. **標籤系統**
   - AI 自動推薦標籤
   - 審文人員選擇或調整標籤
6. **其他資訊頁**
   - `/about` - 關於我們
   - `/rules` - 版規
   - `/platform` - 社群連結

### **3.2 後台（管理員）**
1. **管理儀表板 (`/admin/dashboard`)**
   - 待審核文章
   - 刪文請求
   - 違規 AI 偵測通知
2. **文章管理 (`/admin/posts`)**
   - 查看 / 編輯 / 刪除文章
   - 標籤管理
3. **刪文管理 (`/admin/reports`)**
   - 審核刪文請求
   - 確認刪除後發送 Email
4. **標籤管理 (`/admin/tags`)**
   - 調整 AI 自動標籤
   - 新增 / 刪除標籤
5. **貼文設計 (`/admin/post-design`)**
   - 美宣調整貼文排版
   - 設定 IG 發佈格式
6. **網站設計 (`/admin/design`)**
   - 美宣調整網站佈局
   - 調整顏色、字體、背景
   - 即時預覽
7. **權限管理 (`/admin/permissions`)**
   - 版主管理其他管理員
   - 記錄 Email / Discord ID
8. **黑名單管理 (`/admin/blacklist`)**
   - 封鎖違規 IP
   - Gmail 覆核解封
9. **Discord 設定 (`/admin/discord`)**
   - 綁定 Discord 頻道
   - 設置自動通知

---

## **4. API 設計**
| API | 方法 | 描述 |
|-------------|------|----------------|
| `/api/posts` | GET | 取得所有文章 |
| `/api/post/:id` | GET | 取得單篇文章 |
| `/api/post` | POST | 發表新文章（含 AI 過濾） |
| `/api/report` | POST | 提交刪文請求 |
| `/api/admin/reports` | GET | 取得所有刪文請求 |
| `/api/admin/approve/:id` | POST | 通過文章 |
| `/api/admin/delete/:id` | DELETE | 刪除文章 |
| `/api/admin/blacklist` | POST | 封鎖違規 IP |
| `/api/admin/design` | PUT | 調整網站配色、字體 |
| `/api/admin/post-design/:id` | PUT | 調整貼文版面 |

---

## **5. 開發流程**
### **5.1 階段 1：前後端基礎架構**
:white_check_mark: 設置 Vue 3 + Tailwind + Pinia  
:white_check_mark: 設置 Laravel 12 + MySQL  
:white_check_mark: API 設計（文章、標籤、刪文管理）  

### **5.2 階段 2：核心功能開發**
:small_blue_diamond: 前端 UI
   - 首頁 / 發文 / 文章瀏覽
   - 管理後台
   - 標籤篩選
:small_blue_diamond: 後端 API
   - 發文管理
   - AI 內容過濾
   - 標籤推薦
   - 刪文請求

### **5.3 階段 3：擴展功能**
:small_blue_diamond: Google OAuth（管理員登入）  
:small_blue_diamond: Discord Bot（媒體存儲）  
:small_blue_diamond: Instagram API（美宣發文）  
:small_blue_diamond: 網站設計調整  
:small_blue_diamond: AI 自動分類 / 過濾  

---

## **6. JSON / 資料庫切換機制**
- **開發模式 (`DEV_MODE=true`)** → 使用 JSON
- **正式模式 (`DEV_MODE=false`)** → 使用 MySQL / PostgreSQL

### **切換方法**
```env
DEV_MODE=true
DB_CONNECTION=mysql
DB_DATABASE=campus_anonymous
```

---

## **7. 目標**
- 確保代碼模組化
- 提升系統安全性
- 優化 UX / UI
- 強化管理員審核流程
- 社群平台整合

:rocket: **確認後，即可開始開發！**
