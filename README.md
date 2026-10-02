# 陳思羽 Ssu-Yu Chen

臺大經濟系畢業，現為臺大資工系林守德教授實驗室專題研究生，研究台股新聞的文字特徵與量化評估。
關注機器學習特徵的樣本外驗證，以及 LLM 在金融文本上的應用與可信度。

**開發方式**：下列專案由我與 Claude（AI coding assistant）協作完成。我負責定義問題與功能範圍、
設計資料與系統分工、訂定驗證標準；多數實作程式碼由 Claude 產生，再由我審查、測試與修正。

## Selected projects

### [food-log — 飲食帳本](https://github.com/ssuyu0829/food-log)
Telegram 打一句話記飲食，Gemini 估熱量與營養素，PWA 看趨勢。Supabase（Postgres＋Deno Edge Functions）。

**我做的關鍵決定：**
- 手搖飲不存算好的熱量，改存配方：原本的表裡，同一杯的熱量與糖量隱含的鮮奶量差 20%，改成從同一個參數推出兩者
- 用體重校準記錄準度，但**刻意不算「AI 高估幾 %」**：體重只能識別「攝取 − 消耗」，高估與漏記會互相抵銷；樣本不足時只報趨勢
- LLM 輸出用 JSON schema 限制格式，數值當成未驗證輸入做範圍檢查

### [multiply-dojo — 九九特訓場](https://github.com/ssuyu0829/multiply-dojo)
給家教學生每天用的乘法練習 PWA。

**我做的關鍵決定：**
- 直式填空題出題前窮舉驗證唯一解
- 答錯自動分成「進位／對位／九九本身」，老師端看得出錯在哪一步
- 自適應出題：錯誤率 × 反應時間 EMA × 複習間隔加權；答錯也會拉低速度分數，避免「快但錯」被當成熟練

### [meeting-assistant — 開會小助手](https://github.com/ssuyu0829/meeting-assistant)
填可用時段 → 熱力圖看交集 → 組長拍板自動寄信 → 出席與會議紀錄，收在同一個會議底下。
專案保留了兩個由測試固定下來的安全修正：靜態檔路徑遍歷與 availability 端點越權存取。

### [cat-favor — 貓罐頭紀錄](https://github.com/ssuyu0829/cat-favor)
拍成分標籤 → Gemini 辨識 → 規則庫推乾物比／碳水／磷 → 五隻貓各自評分。所有推算值都明確標示為估算。

### [coffee-map — 咖啡廳地圖](https://github.com/ssuyu0829/coffee-map)
行政區篩選、標籤與 Google Maps 評論摘要。Python／Flask。
