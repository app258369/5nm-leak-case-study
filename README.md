# Case Study: Failure Analysis & Predictive Modeling of a 5nm Tool Leak
*A Physics-Informed Approach to Root Cause Analysis in Advanced Semiconductor Manufacturing*

[English Version](#english-version) | [中文版](#中文版)

---

<a name="english-version"></a>
## 📌 Project Overview (English)
This project presents a retrospective engineering analysis of a critical chemical leak incident during the **2018 TSMC 5nm experimental tool installation** phase in Taiwan. By abstracting field observations into a Python-based mass balance model, this case study demonstrates how to utilize **First-Principles Thinking** to resolve complex hardware failures and challenge conventional assumptions in high-pressure environments.

### 📖 The Story: Engineering Integrity & The "Absolute Victory"
> *"If your sink drains at 100ml/s but you continuously pour in water at 120ml/s, what happens?"*

**The Context & Pressure**
In 2018, while serving as a Machine Leader for a TEL subcontractor, our team was under immense pressure to meet aggressive 5nm installation deadlines. During this phase, a major chemical leak occurred—a plant-wide critical incident that threatened project continuity.

**The Confrontation & RCA**
During the emergency 8D Root Cause Analysis (RCA) meeting, the narrative was initially steered toward "human operational error." To defend my team’s professional integrity, I retrieved the **original piping schematics** to perform a deep-dive structural analysis.

**The "Smoking Gun"**
I presented a decisive rebuttal based on three physical facts:
1.  **Automation Log**: The leak occurred during an unmanned automated sequence with compressed purge intervals.
2.  **Elevation Logic**: The leak originated from a high-altitude vent, physically ruling out interference with sensors at the base.
3.  **Structural Bottleneck**: I identified that **Levels 1 through 6 shared a single, common discharge line**, creating a hydraulic limit.

By proving the leak was a **mathematical certainty of design capacity** rather than a human mistake, my team was fully exonerated. This project is a digital reconstruction of that logical victory.

---

### 🛠 Technical Specifications & System Assumptions
> **⚠️ Information Security Notice**: To comply with industry confidentiality, all physical parameters (flow rates, dimensions) have been **normalized and abstracted**. This model focuses on the "Back-pressure Logic" rather than proprietary OEM data.

1.  **Manifold Drainage Bottleneck**: 
    * Modeled as a multi-inlet system feeding into a single common path.
    * Failure is defined by the point where total instantaneous inflow ($Q_{in}$) exceeds the rated discharge capacity ($Q_{out}$).
2.  **Fluid Dynamics**: 
    * Incorporates the **Dynamic Equilibrium** between high-volatility solvent (e.g., RRC) and fab exhaust-driven evaporation.
3.  **Stability Thresholds**: 
    * **Stable State**: Residual accumulation < Total evaporation per interval.
    * **Risk State**: Residual > Evaporation ➔ **Linear accumulation** ➔ **Interlock Triggered**.

---

<a name="中文版"></a>
## 📌 專案概述 (中文版)
本專案是一份針對 **2018 年南科 5nm 實驗機台開發階段** 重大失效事故的技術復盤報告。透過將現場觀察抽象化為 Python 質量守恆模型，本案例展示了如何利用**第一性原理 (First Principles)** 解決複雜硬體失效，並在高壓環境下利用物理邏輯挑戰既定假設。

### 📖 背景故事：工程正義與「絕對勝利」
> *「如果你的水槽排水速度是 100ml/s，你卻不停倒入 120ml/s 的水，會發生什麼事？」*

**背景與壓力**
2018 年，我擔任 TEL 下包商的 Machine Leader，負責 5nm 實驗機台安裝。當時因應客戶縮短工期的壓力，排程被極度壓縮，隨後發生了嚴重的藥液洩漏事故，成為當時廠區的關注焦點。

**高壓對峙與根因分析 (RCA)**
在當晚的 8D 失效分析會議中，初步定調傾向於現場人員的「人為操失」。為了守護團隊的專業清白，我連夜調閱**原始配管圖紙**，針對硬體架構進行深度拆解。

**關鍵證據 (The Smoking Gun)**
我在會議中提出了三項具備物理強制力的證據：
1.  **自動化紀錄**：洩漏發生於無人值守的自動化作業，且當時噴嘴清洗間隔剛被縮短。
2.  **物理位置高度**：洩漏點源自機台高處溢流孔，物理上排除了人員在底部誤觸感測器的可能。
3.  **結構性瓶頸**：我指出圖紙上的致命傷——**垂直組件 1 到 6 層共用同一條排放主管。**

透過證明該事故是**設計容量極限下的數學必然**，而非人為錯誤，我的團隊最終獲得清白。這份「勝利」不僅保護了團隊，也促成了這份將物理邏輯數位化的案例研究。

---

### 🛠 技術規格與系統假設 (Technical Constraints)
> **⚠️ 資訊安全聲明**：為遵守保密協議，所有物理參數（流量、尺寸）均經過**歸一化與抽象化**處理。本模型旨在展示「背壓溢流邏輯」，而非展示特定設備之機敏數據。

1.  **匯流架構瓶頸 (Abstracted Manifold)**：
    * 模擬多個作業單元共用單一垂直排放路徑的物理受限。
    * 當瞬時進水量 ($Q_{in}$) 超過主管額定宣洩能力 ($Q_{out}$) 時，系統即進入飽和狀態。
2.  **環境動態因素**：
    * 考慮高揮發性溶劑（如 RRC）在 Fab 環境抽風下的質量損失，建立**動態平衡模型**。
3.  **穩定性判別**：
    * **穩定 (Stable)**：單次循環殘留量 < 間隔期總揮發量。
    * **風險 (Unstable)**：殘留量 > 揮發量 ➔ **線性累積** ➔ **觸發 Interlock**。

---

## 📊 Visualization & Analysis
# 穩定性檢查核心代碼
net_change_per_cycle = overflow_per_cycle - (evaporation_rate * interval_min)
is_permanently_safe = net_change_per_cycle <= 0
![Sensor Threshold Analysis](Leak_Case_Sensor_Threshold.png)


# 淨變化 = 每次循環溢流量 - (蒸發率 * 排程間隔)
![Leak Case Heatmap](Leak_Case_Heat_Map.png)


---

## 💻 Tech Stack
* **Python 3.8+**: Simulation Engine
* **NumPy / Matplotlib**: Mathematical Modeling & Visualization
* **Methodology**: Physics-Informed Root Cause Analysis (RCA)

---

© 2024 Your Name. All rights reserved. 
*This case study is for portfolio demonstration purposes only.*
