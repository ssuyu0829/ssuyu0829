# 陳思羽 Ssu-Yu Chen

臺大經濟系畢業。2026 年 4 月至 9 月在臺大資工系林守德教授實驗室做專題，
負責台股新聞資料管線與文字特徵的建置與評估。
目前做台股量化研究：資料管線、回測與樣本外評估。
LLM 產生的金融文本特徵是否可信（前瞻偏誤、分心效應），是接下來想做的題目。

---

## 研究

2026 年 4 月至 9 月在臺大資工系林守德教授實驗室做專題，主題是台股預測的資料與評估，兩條線都已收案：

- **新聞文字特徵**：建置 266 檔台股、2021–2026 年的新聞資料管線，以中文 FinBERT 與 Qwen2.5-7B 產生情緒特徵，在實驗室既有市場特徵之上做對照實驗；用安慰劑對照與事先設定的判讀門檻整理結果，新聞特徵沒有帶來穩定改善。
- **回測與策略評估**：對實驗室策略做消融掃描與新舊回測引擎逐格對帳，把「這個數字能不能信」寫成可重跑的檢核：季度報酬連乘須還原全期報酬、IC 須高於打亂標籤的雜訊地板、股池須為當時組得出來的名單、回測不得在上市前成交。

目前以 FinLab 資料做自己的策略測試，同時補資料結構、演算法、線性代數與機率。
接下來想做的題目：LLM 情緒分數的預測力有多少來自文字、多少來自模型記憶（以模型公開日切分、遮蔽公司識別資訊重評）；2026-07 起的資料只收集不分析，作為保留集。

---

## 專案

2026 年 3–10 月與 Claude 協作做出的五個系統。多數實作程式碼由 Claude 產生；問題定義、資料與系統設計、驗證標準與測試由我負責並審查。
寫得快之後，瓶頸變成 AI 很會產生看起來合理、其實錯的東西，所以每個專案底下的「關鍵判斷」是我在 AI 之外真正做的事：
定義問題的範圍、決定什麼證據才算做對、抓出看似合理的錯。每個專案都有 CI 與可重跑的測試。

### [food-log](https://github.com/ssuyu0829/food-log) 飲食帳本 [![CI](https://github.com/ssuyu0829/food-log/actions/workflows/ci.yml/badge.svg)](https://github.com/ssuyu0829/food-log/actions/workflows/ci.yml)

Telegram 打一句話記飲食，看自己的手搖飲趨勢。

- **關鍵判斷**：飲料改存配方、從同一組參數推出熱量與糖，修掉同一杯隱含奶量差 20% 的矛盾；體重無法分開「AI 高估」與「漏記」，所以**刻意不輸出高估百分比**。
- **技術**：Telegram Bot API webhook · Gemini vision＋structured output · Supabase（Postgres、Deno Edge Functions、pg_cron）· GitHub Pages PWA
- **驗證**：96 tests · CI

### [multiply-dojo](https://github.com/ssuyu0829/multiply-dojo) 九九特訓場 [![CI](https://github.com/ssuyu0829/multiply-dojo/actions/workflows/ci.yml/badge.svg)](https://github.com/ssuyu0829/multiply-dojo/actions/workflows/ci.yml) · [Demo](https://ssuyu0829.github.io/multiply-dojo/)

兩位家教學生每天用的九九乘法與直式乘法練習。

- **關鍵判斷**：直式填空題出題前**窮舉驗證唯一解**；答錯自動分成進位、對位、九九本身三類，老師才看得出錯在哪一步。
- **技術**：零依賴 ES modules · Leitner 分箱＋反應時間 EMA · 離線佇列同步 Supabase RPC · RLS＋`SECURITY DEFINER`
- **驗證**：600 題唯一解測試 · 錯誤分類與引擎測試 · CI

### [meeting-assistant](https://github.com/ssuyu0829/meeting-assistant) 開會小助手 [![CI](https://github.com/ssuyu0829/meeting-assistant/actions/workflows/ci.yml/badge.svg)](https://github.com/ssuyu0829/meeting-assistant/actions/workflows/ci.yml)

填時段 → 熱力圖 → 組長拍板自動寄信 → 出席與會議紀錄，全部留在同一個會議底下。

- **關鍵判斷**：前身是 2021 年 Coding 101 競賽（全國第 3 名、最佳人氣獎）的五人團隊 tkinter 桌面版，由我一個人重寫成網站；重寫時找出並用測試鎖住**路徑遍歷**與**越權存取**兩個漏洞。
- **技術**：FastAPI · SQLAlchemy＋Alembic（9 張表）· JWT＋bcrypt · Resend Email API · Supabase Postgres（connection pooler）· Chart.js
- **驗證**：16 tests · CI

### [cat-favor](https://github.com/ssuyu0829/cat-favor) 貓罐頭紀錄 [![CI](https://github.com/ssuyu0829/cat-favor/actions/workflows/ci.yml/badge.svg)](https://github.com/ssuyu0829/cat-favor/actions/workflows/ci.yml)

拍成分標籤，記錄五隻貓各自的喜好。

- **關鍵判斷**：**AI 只負責擷取、不負責下結論**。Gemini 把標籤轉成欄位，營養換算交給可檢查的規則；缺值的假設直接顯示在畫面上。
- **技術**：React 19 · TypeScript · Vite PWA · Gemini vision · IndexedDB（資料不離開手機）· JSON 備份
- **驗證**：TypeScript typecheck＋production build · CI

### [coffee-map](https://github.com/ssuyu0829/coffee-map) 咖啡廳地圖 [![CI](https://github.com/ssuyu0829/coffee-map/actions/workflows/ci.yml/badge.svg)](https://github.com/ssuyu0829/coffee-map/actions/workflows/ci.yml) · [Demo](https://coffee-map.onrender.com)（冷啟動約 30 秒）

依行政區或目前位置找能讀書的咖啡廳。

- **關鍵判斷**：兩個資料源座標相距 **100 公尺內才合併，超過就不猜**；評論推斷的標籤用 Café Nomad 的人工評分補強，兩邊都沒證據就不加標籤。
- **技術**：Flask · Google Places API（Text／Nearby Search、Place Details）· Café Nomad API · 13 個標籤規則引擎
- **驗證**：8 tests · CI

---

## 工具

- **Research**：Python · R · PyTorch · HuggingFace Transformers · scikit-learn · XGBoost · pandas · FinLab · FinMind · Linux GPU server
- **Systems**：TypeScript · FastAPI · Flask · React · PostgreSQL／Supabase · SQL · GitHub Actions

## 聯絡

📫 b08303036@ntu.edu.tw
