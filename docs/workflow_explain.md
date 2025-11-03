# Workflow 說明文件（workflow_explain.md）

## 工作流程名稱
**Update Activity Log**

## 功能說明
此 GitHub Actions workflow 用於自動更新 `README.md` 檔案中的「最近活動紀錄」區塊。  
透過呼叫 GitHub Events API 取得使用者最新活動（Pull Request、Issue、留言、Release），  
並自動寫入 README 中的指定位置。

## 運作流程
1. **觸發事件**  
   - 每天 00:00 UTC 自動執行（schedule）  
   - 可在 Actions 頁面手動執行（workflow_dispatch）  

2. **主要步驟**  
   - **Checkout**：取得本專案原始碼。  
   - **Generate GitHub Activity**：使用 `jamesgeorge007/github-activity-readme` 取得活動並更新 README。  
   - **Commit & Push**：若有變更，Action bot 會自動送出 commit。

3. **使用 Token**  
   - 以 GitHub Secrets 中的 `TOKEN` 確保安全授權，避免公開存取權限。

4. **輸出結果**  
   - 若有新活動，會在 `README.md` 內的  
     `<!--START_SECTION:activity-->` 與 `<!--END_SECTION:activity-->` 之間插入最新活動內容。  
   - 網站首頁（`index.md`）會自動顯示更新後的 README。

## 設計理念
此流程展示 DevOps 的自動化思維：  
- **持續整合（CI）**：每次活動都能反映於文件。  
- **持續交付（CD）**：更新後自動同步至 GitHub Pages。  
- **可維護性**：透過分離 workflow 設定與文件，使專案結構清晰可擴充。
