# 陳思羽 Ssu-Yu Chen

**把問題拆成可以被驗證的規則——不管程式是誰寫的。**

臺大經濟系畢業，臺大資工系林守德教授實驗室專題研究生，研究台股新聞的文字特徵與樣本外評估。
關注 LLM 在金融文本上的可信度：前瞻偏誤、資訊重複，以及「看起來有效」和「真的有效」之間的距離。
*Economics graduate turned ML researcher at NTU CSIE. I care less about whether a model scores well and more about whether the score can be trusted.*

---

## AI 改變了我的什麼

2026 年，AI 讓「把程式寫出來」的成本降到接近零；我在 3–10 月用 Claude 做出下面五個系統。
但寫得快之後，瓶頸換了位置：**AI 很會產生看起來合理、其實錯的東西。** 所以我的工作變成三件 AI 不會替我做的事：

1. **定義問題**：要解決誰的什麼困擾、什麼範圍內算完成。
2. **決定什麼證據才算做對**：哪些性質要用測試鎖住、哪些數字不能輸出。
3. **抓出看似合理的錯**：例如飲料熱量表裡，同一杯的熱量與糖量隱含的鮮奶量差了 20%。

這也是我做研究的方式：負面結果是合法結果，相關的版本不能算成多份獨立證據。

> 開發分工：多數實作程式碼由 Claude 產生；問題定義、資料與系統設計、驗證標準與測試由我負責並審查。

---

## 研究（進行中）

- 中文 FinBERT 與 Qwen2.5 新聞情緒特徵，在既有價量基準之外是否有樣本外增額資訊
- 評估設計：時間切分、rank IC 差值、安慰劑檢定；2026-07 起的資料預先宣告為保留集

---

## 專案

每個專案都有 CI 與可重跑的測試；「關鍵判斷」是我在 AI 之外真正做的事。

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

- **關鍵判斷**：前身是 2020 年五人團隊的 tkinter 桌面版（Coding 101 全國第 3 名、最佳人氣獎），由我一個人重寫成網站；重寫時找出並用測試鎖住**路徑遍歷**與**越權存取**兩個漏洞。
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

- **Research**：Python · R · PyTorch · HuggingFace Transformers · scikit-learn · XGBoost · pandas · Linux GPU server
- **Systems**：TypeScript · FastAPI · Flask · React · PostgreSQL／Supabase · SQL · GitHub Actions

## 聯絡

📫 b08303036@ntu.edu.tw
