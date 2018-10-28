# 研究局部进展鼻咽癌样本的mRNA表达谱在评估鼻咽癌远端转移风险的预测能力。
#步骤如下

## 1.数据来源
     
     石蜡包埋样本，mRNA芯片

## 2.筛选差异基因，作为构建分类器的初始基因列表(命名为L)

    2.1 基因表达量的标准化:oligo package in R with Robust Multi-array Analysis (RMA) 
    2.2 差异表达(FC>1.5 && p <=0.05)： empirical Bayes (eBayes) in the limma package 。24对转移组和非转移组的样本做差异表达分析（该文章中获得137个差异表达基因），两个组的临床特征都要求一致（如性别、年龄、T、N、放疗、化疗等），样本量少可获得较多的差异表达基因，但又不能太少，导致差异表达基因检测不准确，后期再用大样本进行训练。

## 3.从410例样本的训练集提取L基因对应的表达量， 并利用penalised regression model构建基因分类器
  
    模型训练结果得到一个13个基因的分类器（命名为DMGN），能够将训练集分成高分险组和低分险组。
    3.1 在penalised regression model执行LASSO
    3.2 bootstrap method 验证候选基因的健壮性
    3.3 ROC曲线确定最终选择多少候选基因
    3.4 在训练集中根据Cox模型加权的回归系数构建预测模型 
    3.5 利用tile-software寻找分类的最优阈值（即the score that produced the largest χ² value in the Mantel–Cox test)


## 4.用一个内部测试集（204例样本）和两个外部数据集（165例样本和158例样本）验证基因分类器的诊断准确性
    
    
## 5.结论
  
   相对于低风险组，高分险组的metastasis-free survival,disease-free survival和overall survival更短。而且高分险组无法从同步化疗中获益。
   另外，根据这一结论可以预测化疗的获益人群。
   
## 6.讨论
   后续将结合DMGN和其他的临床指标如N stage, sex,serum lactate dehydrogenase，C-reactive protein concentrations等一起进行预后判断。
