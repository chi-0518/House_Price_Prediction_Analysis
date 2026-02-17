# 房地產價格預測分析：基於四分位數分類與關鍵特徵篩選
(House Price Prediction & Multi-Model Analysis)

本專案利用機器學習技術，針對包含 **81 個原始特徵** 的房地產數據集進行深入分析。為了解決傳統二元分類（高/低房價）資訊量不足的問題，我們採用 **四分位數 (Quartiles) 分類法** 將房價精確分為四個層級，並透過特徵重要性篩選，優化多分類模型的預測準確度。

---

## 研究方法與特徵篩選

### 1. 關鍵特徵篩選 (Feature Selection)
原始資料集包含 81 個特徵欄位（包含土地分區、房屋屬性等）。為了提升模型效能並避免過度擬合 (Overfitting)，我們透過隨機森林模型計算 **特徵重要性評分 (Feature Importance Score)**，最終篩選出對房價影響最顯著的 **10 大關鍵因素**：

1. **OverallQual**: 房屋整體品質評分 (影響力權重最高)
2. **GrLivArea**: 地上居住面積 (反映空間大小)
3. **TotalBsmtSF**: 地下室總面積
4. **YearBuilt**: 建造年份 (反映屋齡與折舊)
5. **1stFlrSF**: 第一層樓面積
6. **GarageCars**: 車庫容量 (可容納車輛數)
7. **LotArea**: 土地總面積
8. **FullBath**: 浴室數量
9. **YearRemodAdd**: 改建年份
10. **MSZoning**: 住宅密度分類 (包含 RH, RL, RP, RM 等)



### 2. 住宅密度消融實驗結論
在研究過程中，我們特別針對 **RH (高密度)**、**RL (低密度)**、**RP (公園低密度)** 與 **RM (中密度)** 進行獨立測試。
* **實驗發現**：若僅依賴住宅密度指標進行預測，準確率會稍微下降。
* **原因分析**：數據集中樣本分佈不均（大部份數據集中於 RL），導致特徵影響力被稀釋。
* **最終決策**：模型必須整合「房屋品質」與「土地面積」等物理特徵，才能準確預測房價層級。

---

## 模型表現總結

透過多模型評估，本專案成功在四分類問題中取得優異表現：

| 模型名稱 | 準確率 (Accuracy) | 評價 |
| :--- | :--- | :--- |
| 🥇 **Random Forest** | **0.8402** | **最佳模型：對於多特徵與非線性關係處理能力最強** |
| 🥈 Stacking Classifier | 0.8174 | 表現優異，有效集成了多個弱學習器的優點 |
| 🥉 Extra Trees | 0.8037 | 穩定性佳，準確率位居第三 |



---

## 技術棧 (Tech Stack)
* **語言**: Python 3.x
* **數據處理**: Pandas, NumPy
* **機器學習**: Scikit-learn (Random Forest, Stacking, Extra Trees)
* **資料視覺化**: Seaborn, Matplotlib

---

## 專案結構
* `House_Price_Classification_Analysis.ipynb`: 包含從 81 欄位清洗、特徵重要性篩選到模型訓練的完整 Notebook。
* `data/`: 存放原始訓練數據 `train.csv`。
* `requirements.txt`: 執行環境所需套件清單。

---
