# 專案：基於 RFM 模型的電商客戶分群分析

## 1. 專案目標 (Project Objective)

在電商領域，並非所有客戶都具有相同的價值。將有限的行銷資源平均分配給所有客戶，往往導致效率低下。本專案旨在解決以下商業問題：

*   **如何區分高價值與低價值客戶？**
*   **如何識別具有增長潛力的客戶與面臨流失風險的客戶？**
*   **如何針對不同客戶群體，制定差異化的精準行銷策略以提升客戶終身價值 (CLV)？**

本專案將利用一份公開的英國電商交易數據集，透過 **RFM 模型** 與 **K-Means 分群演算法**，對客戶進行價值分層，並提出可執行的商業建議。

---

## 2. 使用技術 (Tech Stack)

| 領域 | 技能/工具 | 在本專案中的應用 |
| :--- | :--- | :--- |
| **數據處理** | `Python`, `Pandas` | 讀取、清洗超過 54 萬筆的交易數據，處理缺失值、異常值與資料格式轉換。 |
| **特徵工程** | `Pandas`, `RFM Model` | 從交易流水帳中，為每個客戶建構 **R (Recency)**, **F (Frequency)**, **M (Monetary)** 三大核心特徵。 |
| **機器學習** | `Scikit-learn` | 使用 `StandardScaler` 進行數據標準化，並應用 `KMeans` 演算法對客戶進行自動化分群。 |
| **數據視覺化** | `Matplotlib`, `Seaborn` | 透過箱型圖 (Boxplot) 視覺化比較各客戶群體在 RFM 維度上的差異，使分析結果更直觀。 |
| **開發環境** | `Jupyter Notebook`, `VS Code` | 在 Notebook 環境中進行探索式分析、模型訓練與迭代。 |

---

## 3. 分析流程 (Analysis Workflow)

本專案遵循一套完整的數據分析流程，從數據的原始樣貌到最終的商業洞察：

1.  **數據載入與初探 (Data Loading & First Look)**
    *   載入數據集，檢視其規模、結構與基本品質。
    *   **發現問題**：存在大量 `CustomerID` 缺失值、`Quantity` 與 `UnitPrice` 為負的異常紀錄，以及 `InvoiceDate` 格式不正確。

2.  **數據清洗 (Data Cleaning)**
    *   刪除 `CustomerID` 為空的紀錄。
    *   篩選掉所有 `Quantity` 與 `UnitPrice` 小於等於 0 的無效交易。
    *   將 `InvoiceDate` 轉換為標準的 `datetime` 格式，為後續計算 Recency 做準備。

3.  **特徵工程 (Feature Engineering)**
    *   **核心任務**：將視角從「交易」轉換為「客戶」。
    *   計算每筆訂單的總價 `TotalPrice`。
    *   以客戶為單位進行分組 (`groupby`)，計算出每個客戶的 **Recency**, **Frequency**, **Monetary**。

4.  **建模與分群 (Modeling & Clustering)**
    *   對 RFM 三個特徵進行**標準化**，以消除不同單位的尺度影響。
    *   應用 **K-Means 演算法**將客戶分為 4 個群體。

5.  **結果分析與視覺化 (Analysis & Visualization)**
    *   計算並分析各群體的 RFM 平均值與客戶規模佔比。
    *   使用**箱型圖**直觀地比較各群體特徵，驗證分群的有效性與差異性。

6.  **商業洞察與建議 (Business Insights & Recommendations)**
    *   為每個群體進行**客戶畫像 (Persona)**，並賦予其商業名稱。
    *   基於各群體的特徵，提出針對性的行銷策略。

---

## 4. 主要發現與商業建議 (Key Findings & Recommendations)

透過 K-Means 分群，我們成功將客戶劃分為四個具有顯著差異的群體：



| 群組命名 | 客戶規模 | 特徵 (R/F/M) | 商業洞察與策略 |
| :--- | :--- | :--- | :--- |
| 👑 **超級VIP客戶** | **0.3%** | 低 / 極高 / 極高 | **公司命脈**，人數極少但價值驚人。應採取**一對一專人維護**，提供極致尊榮服務，不惜代價防止流失。 |
| 🚀 **高價值核心客戶** | **4.7%** | 低 / 高 / 高 | **忠誠主力**，是會員制度與忠誠度計畫的核心目標。應透過高回饋獎勵，並引導其**向上升級**。 |
| 🌱 **潛力/一般客戶** | **70.4%** | 中 / 低 / 中 | **公司基本盤**，最具提升潛力。應透過**自動化行銷**與個性化推薦，提升其活躍度與消費頻次。 |
| 💤 **沉睡/流失客戶** | **24.6%** | 極高 / 極低 / 低 | **待喚醒群體**，佔比龐大。應透過**高吸引力的召回方案**（如大額折扣）進行定期喚醒，並設定停損點。 |

---

## 5. 如何運行此專案 (How to Run This Project)

1.  **Clone 專案庫**
    ```bash
    git clone 
    cd ecommerce-analysis
    ```

2.  **建立並啟用虛擬環境**
    ```bash
    python -m venv venv
    .\venv\Scripts\activate  # Windows
    # source venv/bin/activate  # macOS/Linux
    ```

3.  **安裝所需套件**
    ```bash
    pip install -r requirements.txt
    ```

4.  **開啟 Jupyter Notebook**
    *   在 VS Code 中直接打開 `notebook` 資料夾下的 `.ipynb` 檔案。
    *   或在終端機輸入 `jupyter notebook` 並在瀏覽器中開啟。

