# 🏆 Playground Series - S4E10: Loan Approval Prediction
🔗 [Kaggle Competition Overview](https://www.kaggle.com/competitions/playground-series-s4e10/overview)

**競賽目標: 根據申請人的資料，預測其是否能獲得貸款批准。**

## 資料處理流程概覽
1. **初始處理**：移除 `id` 欄位與 `target` 分離
2. **資料視覺化**: 
    * 發現目標變數存在類別不平衡現象
    * 透過features與target間的boxplot發現多個特徵資料存在嚴重右偏問題，可能因為少數高收入群體拉高平均質。
3. **偏態處理**：以 `log1p` 處理偏態 > 1 的欄位
4. **標準化**：所有數值型欄位使用 `StandardScaler`
5. **類別型資料處理**：
   * home ownership、loan intent: 資料類別不多且互相無關聯，採用`One-Hot Encoding`
   * loan grade: 因資料類別有順序性，故採用`Ordinal Encoding`
   * cb_person_default_on_file: binary類別，採用`Label Encoding`(0/1)
6. **資料切分與SMOTE**：切分訓練資料集與驗證資料集後，對訓練資料做oversampling，以解決資料不平衡的問題。
7. **模型訓練與評估**：使用 RandomForest / XGBoost / CatBoost 預測與比較

---

## 🧠 這次練習中釐清與學習的新觀念

| Issues              | 收穫與澄清                                   |
| --------------- | --------------------------------------- |
| **偏態處理順序**      | 偏態處理應在離群值處理之前進行，有助於穩定數值分布並提升模型學習效果      |
| **標準化時機**       | 標準化應在完成缺失值處理、離群值處理與類別資料編碼之後，僅對數值欄位執行    |
| **SMOTE對象與時機點** | SMOTE僅能用於訓練資料，不能應用於整體資料或測試集，以避免資料洩漏    |
| **資料集是否要push至github?**      | 應透過 `.gitignore` 避免將資料集等大型或有權限問題的檔案publish到github上 |