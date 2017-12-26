## 赛题回顾
[赛题](https://www.kesci.com/apps/home/competition/56f37e6717f910f4347acf2e)提供用户在2015年1月至2015年12月的“用户终端使用变迁”数据，预测用户在2016年1至3月更换手机的概率。评测指标采用AUC。

## 数据集生成
根据数据说明：
>联通内部8月-9月之间品牌和机型的标签发生了变化。8月份之前，总部品牌和机型都是英文的；9月份之后，给的都是中文的。由于品牌和机型的标签是总部给的，上海联通没有机型变化对照表，内部一般是8月份的数据用8月份之前的数据预测，9月份之后的数据用9月份之后的数据预测。

**为了简化数据处理流程，以下只选择9-12月数据生成训练集和测试集。**

## 特征工程
**备注：模型均为LR**  

| 序号 | 处理方法 | AUC | 对照项 |
|:------------:|:--------------:|:-------------:|:-------------:|
| FE1.1        | 逻辑特征OHE+连续特征**Z-Score**   | 0.59054 |         |
| FE1.2        | 逻辑特征OHE+连续特征**正态归一化**  | 0.59226 | 0.59054 FE1.1  |
| FE1.3        | 逻辑特征OHE&**正态归一化**+连续特征**正态归一化**  | 0.61448 | 0.59226 FE1.2 |
| FE2.1        | 逻辑特征OHE+连续特征**离散化&OHE**  | 0.59688 | 0.59054 FE1.1 0.59226 FE1.2 |
| FE2.2        | 逻辑特征OHE&**正态归一化**+连续特征**离散化&OHE&正态归一化**  | 0.68032| 0.59688 FE2.1 |
| FE3.1        | 逻辑特征OHE+连续特征**离散化&OHE**+外部数据终端库  | 0.68922| 0.59688 FE2.1 |
| FE3.2        | 逻辑特征OHE&**正态归一化**+连续特征**离散化&OHE&正态归一化**+外部数据终端库**正态归一化**  | 0.73619| 0.68922 FE3.1 |

## 基线模型 Baseline Model
|  序号  |  特征工程  |  所用模型  |  AUC |
|:------------:|:--------------:|:-------------:|:-------------:|
|  Baseline1   |  FE3.2  |  Logistic Regression  | 0.73619 |
|  Baseline2   |  FE3.1  |  GBDT                 | 0.70549 |
|  Baseline3   |  FE3.2  |  GBDT                 | 0.79367 |

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