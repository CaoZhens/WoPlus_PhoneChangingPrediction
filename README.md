## 赛题回顾
[本赛题](https://www.kesci.com/apps/home/competition/56f37e6717f910f4347acf2e)提供用户在2015年1月至2015年12月的“用户终端使用变迁”数据，预测用户在2016年1至3月更换手机的概率。评测指标采用AUC。

## 数据集生成
根据数据说明：
>联通内部8月-9月之间品牌和机型的标签发生了变化。8月份之前，总部品牌和机型都是英文的；9月份之后，给的都是中文的。由于品牌和机型的标签是总部给的，上海联通没有机型变化对照表，内部一般是8月份的数据用8月份之前的数据预测，9月份之后的数据用9月份之后的数据预测。

**为了简化数据集处理流程，我们只选择9-12月数据进行训练和测试**

## 模型对比

**Baseline-1.1**
* 模型类别：**LR**
* 特征工程：**原始逻辑特征ohc + 原始连续特征Z-Score归一化**
* 训练集AUC： **0.59054**
* ROC Curve：
<img src="https://github.com/CaoZhens/WoPlus_PhoneChangingPrediction/blob/master/pic/ROC_Curve_Baseline_1.png" alt="" data-canonical-src="" />

**Baseline-1.2**
* 模型类别：**LR**
* 特征工程：**原始逻辑特征ohc + 原始连续特征正态归一化**
* 训练集AUC： **0.59226**
* ROC Curve：
<img src="https://github.com/CaoZhens/WoPlus_PhoneChangingPrediction/blob/master/pic/ROC_Curve_Baseline_1_2.png" alt="" data-canonical-src="" />

**Baseline-1.3**
* 模型类别：**LR**
* 特征工程：**原始逻辑特征ohc&正态归一化 + 原始连续特征正态归一化**
* 训练集AUC： **0.61448**
* ROC Curve：
<img src="https://github.com/CaoZhens/WoPlus_PhoneChangingPrediction/blob/master/pic/ROC_Curve_Baseline_1_3.png" alt="" data-canonical-src="" />

**Baseline-2.1**
* 模型类别：**LR**
* 特征工程：**原始逻辑特征ohc+原始连续特征decretization-ohc**
* 训练集AUC： **0.59688**
* ROC Curve：
<img src="https://github.com/CaoZhens/WoPlus_PhoneChangingPrediction/blob/master/pic/ROC_Curve_Baseline_2.png" alt="" data-canonical-src="" />

**Baseline-2.2**
* 模型类别：**LR**
* 特征工程：**原始逻辑特征ohc&正态归一化 + 原始连续特征decretization-ohc&正态归一化**
* 训练集AUC： **0.68032**
* ROC Curve：
<img src="https://github.com/CaoZhens/WoPlus_PhoneChangingPrediction/blob/master/pic/ROC_Curve_Baseline_2_2.png" alt="" data-canonical-src="" />

**Baseline-3.1**
* 模型类别：**LR**
* 特征工程：**原始逻辑特征ohc+原始连续特征decretization-ohc+外部终端库特征**
* 训练集AUC： **0.68922**
* ROC Curve：
<img src="https://github.com/CaoZhens/WoPlus_PhoneChangingPrediction/blob/master/pic/ROC_Curve_Baseline_3.png" alt="" data-canonical-src="" />

**Baseline-3.2**
* 模型类别：**LR**
* 特征工程：**原始逻辑特征ohc&正态归一化+原始连续特征decretization-ohc&正态归一化+外部终端库特征&正态归一化**
* 训练集AUC： **0.73619**
* ROC Curve：
<img src="https://github.com/CaoZhens/WoPlus_PhoneChangingPrediction/blob/master/pic/ROC_Curve_Baseline_3_2.png" alt="" data-canonical-src="" />