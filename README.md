# Camera M-Mode Pro/Core - 攝影參數提示詞生成節點

A ComfyUI node that simulates real camera M-mode operations, generating professional photography parameters and AI-friendly prompt words with one click. (模擬真實相機手動模式操作，一鍵生成專業攝影參數與AI友好提示詞)

## ✨ 核心亮點

- 📸 **還原真實相機操作**：所有參數均採用標準相機檔位（下拉選單），無需手動輸入小數、無拉桿誤差，小白也能輕鬆操作。

- 🤖 **AI 友好提示詞**：自動將攝影參數（光圈、快門等）轉化為大模型可精確理解的語義化描述詞，大幅提升生成圖片的可控性與專業度。

- 📌 **雙版本並存**：Core（基礎實用版）+ Pro（專業增強版），分別對應快速使用與高品質提示詞需求。

- ⚡ **穩定輕量**：無第三方依賴，相容所有 ComfyUI 版本，程式碼乾淨、無報錯、生成提示詞速度快。

## 📋 功能介紹

節點核心功能：透過直覺化的標準攝影參數選單，自動生成「人類可讀的專業參數 + AI 可理解的描述詞」組合提示詞，解決手動輸入參數不直觀、大模型難以識別攝影術語的問題。

### 1. 支援的參數（標準相機檔位）

|參數名稱|標準檔位範圍|預設值|
|---|---|---|
|光圈 (Aperture)|f/1.0, f/1.2, f/1.4, f/1.8, f/2.0, f/2.8, f/4.0, f/5.6, f/8.0, f/11, f/16, f/22|f/2.8|
|快門速度 (Shutter Speed)|1/8000, 1/4000, 1/2000, 1/1000, 1/500, 1/250, 1/125, 1/60, 1/30, 1/15, 1/8, 1/4, 1/2, 1s|1/125|
|ISO 感光度|50, 100, 200, 400, 800, 1600, 3200, 6400, 12800, 25600|200|
|曝光補償 (EV Comp)|-3.0, -2.0, -1.0, -0.7, -0.3, 0, +0.3, +0.7, +1.0, +2.0, +3.0|0|
|對焦模式 (Focus Mode)|Auto Focus, Manual Focus, Eye Focus, Background Blur|Auto Focus|
|白平衡 (White Balance)|Auto, Daylight, Cloudy, Warm, Cool|Auto|
|風格預設 (Style Preset)|General, Virtual Idol, Portrait, Night, Cinematic|General|
### 2. 自動生成的提示詞結構

提示詞分為兩部分，兼顧「專業性」與「AI 可讀性」：

- **專業參數（給人閱讀）**：例如 `f/1.4, 1/4000s, ISO 100, +0.3EV`

- **AI 描述詞（給大模型理解）**：根據參數自動切換，例如：
        

    - 光圈 f/1.4 → `extremely shallow depth of field, strong bokeh`（極淺景深、強烈散景）

    - 快門 1/4000 → `fast shutter speed, frozen motion`（高速快門、凝固動作）

    - ISO 100 → `ultra clean, sharp details, no noise`（超乾淨、無雜訊）

### 3. Core 版與 Pro 版差異

|版本|定位|核心差異|
|---|---|---|
|Camera M-Mode Core|基礎實用版|描述詞精簡，適合快速生成基礎攝影提示詞，輕量高效。|
|Camera M-Mode Pro|專業增強版|描述詞更細緻豐富，針對人像、虛擬偶像、電影感等場景優化，出圖品質更高。|
## 📥 安裝方法

1. 下載本項目壓縮包，內含三個核心文件：`__init__.py`、`core_nodes.py`、`pro_nodes.py`

2. 打開 ComfyUI 安裝目錄，進入 `ComfyUI/custom_nodes/` 資料夾

3. 建立一個新文件夾（建議命名為 `Camera_M_Mode/`）

4. 將 `__init__.py`、`core_nodes.py` 和 `pro_nodes.py` 複製到該新文件夾中

5. 重啟 ComfyUI，在節點列表的 `CustomCamera/MMode` 分類下，即可找到兩個節點

## 🔧 使用方法

1. 打開 ComfyUI，從節點列表拖出 `Camera M-Mode Core` 或 `Camera M-Mode Pro` 節點

2. 在節點上，透過下拉選單選擇所需的攝影參數（光圈、快門、ISO 等）

3. 將節點的 `camera_prompt` 輸出端，連接到圖像生成節點的提示詞輸入端（如 `CLIP Text Encode`）

4. 點擊執行，即可自動生成對應的專業提示詞，用於 AI 圖像生成

## 🎯 預期效果

例如，選擇參數：`f/1.4、1/4000、ISO 100、Warm、Portrait`，節點會自動生成以下提示詞：

```text
shot on DSLR, f/1.4, 1/4000s, ISO 100, eye focus, sharp eyes, warm tone, golden hour, orange tint, extremely shallow depth of field, strong bokeh, dreamy background, fast shutter speed, frozen motion, sharp action, no blur, ultra clean, sharp details, no noise, pristine image, portrait photography, soft light, smooth skin, shallow depth of field
```

## 📌 注意事項

- 本節點僅負責生成攝影相關提示詞，需配合 ComfyUI 原生圖像生成節點（如 Stable Diffusion）使用。

- 無需安裝額外依賴，複製文件、重啟 ComfyUI 即可使用。

- 若需自定義參數檔位、添加新風格，可直接修改兩個 `.py` 文件中的對應配置（程式結構清晰，易於維護）。

## 💡 後續可擴充方向（按需自行修改）

- 添加更多風格預設（如風景、商業攝影、復古膠片等）。

- 增加自定義提示詞輸入框，支援手動補充提示詞。

- 擴充更多相機標準檔位（如更長的長曝光時間、更多光圈選項）。

## 🤝 反饋與優化

若使用過程中遇到報錯、參數異常，或有新的功能需求，歡迎提交 Issues 或 PR，一起完善這個工具！
> （注：文档部分内容可能由 AI 生成）
