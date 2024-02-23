# -GPU -IMG -IMG_DIM
bash IKRL.sh 0 3 512 MMTransE
bash IKRL.sh 0 3 512 MMTransE1

bash IKRL.sh 0 1 512 MMTransE1
bash IKRL.sh 0 2 4096 MMTransE1
bash IKRL_random.sh 0 1 4096 MMTransE1

bash tb_kgc.sh 1 3 512 TBKGC
bash tb_kgc.sh 1 3 512 TBKGC1


bash IKRL.sh 0 1 512
bash IKRL.sh 0 3 512
bash IKRL.sh 0 2 4096

###分析实验：
YG15K：
（IKRL）
bash IKRL.sh 0 1 512 MMTransE1 1 (当model_name = MMTransE1时,最后一位不起作用)
-G：0.407 :/home/xuyajing/Ne-MMKGC/output/link_prediction/YG15K/MMTransE1/epoch=1439-Eval|mrr=0.406.ckpt
bash IKRL.sh 0 3 512 MMTransE1 1
-GWN: 0.401: /home/xuyajing/Ne-MMKGC/output/link_prediction/YG15K/MMTransE1/epoch=1079-Eval|mrr=0.400.ckpt
bash IKRL.sh 0 3 512 MMTransE 1
-GWN_R: 0.413: /home/xuyajing/Ne-MMKGC/output/link_prediction/YG15K/MMTransE/epoch=1679-Eval|mrr=0.409.ckpt

（TBKGC）
bash tbkgc.sh 0 1 512 TBKGC1 1 (当model_name = TBKGC1时,最后一位不起作用)
-G：0.423 :/home/xuyajing/Ne-MMKGC/output/link_prediction/YG15K/TBKGC1/epoch=1259-Eval|mrr=0.422.ckpt
bash tbkgc.sh 0 3 512 TBKGC1 1
-GWN: 0.421: /home/xuyajing/Ne-MMKGC/output/link_prediction/YG15K/TBKGC1/epoch=1039-Eval|mrr=0.418.ckpt
bash tbkgc.sh 0 3 512 TBKGC 1
-GWN_R: 0.429: /home/xuyajing/Ne-MMKGC/output/link_prediction/YG15K/TBKGC/epoch=1259-Eval|mrr=0.424.ckpt

FB15K:
(IKRL)
bash IKRL.sh 0 1 512 MMTransE1 1 (当model_name = MMTransE1时,最后一位不起作用)
-G：0.505 ：/home/xuyajing/Ne-MMKGC/output/link_prediction/FB15K/MMTransE1/epoch=1099-Eval|mrr=0.508.ckpt
bash IKRL.sh 0 3 512 MMTransE1 1
-GWN： 507 : /home/xuyajing/Ne-MMKGC/output/link_prediction/FB15K/MMTransE1/epoch=1259-Eval|mrr=0.510.ckpt
bash IKRL.sh 0 3 512 MMTransE 1
-GWN_R: 0.508 : /home/xuyajing/Ne-MMKGC/output/link_prediction/FB15K/MMTransE/epoch=1139-Eval|mrr=0.511.ckpt

(TBKGC)
bash tbkgc.sh 0 1 512 TBKGC1 1 (当model_name = TBKGC1时,最后一位不起作用)
-G：0.529 ：/home/xuyajing/Ne-MMKGC/output/link_prediction/FB15K/TBKGC1/epoch=1179-Eval|mrr=0.531.ckpt
bash tbkgc.sh 0 3 512 TBKGC1 1
-GWN： 529 : /home/xuyajing/Ne-MMKGC/output/link_prediction/FB15K/TBKGC1/epoch=1399-Eval|mrr=0.531.ckpt
bash tbkgc.sh 0 3 512 TBKGC 1
-GWN_R: 0.531: /home/xuyajing/Ne-MMKGC/output/link_prediction/FB15K/TBKGC/epoch=1239-Eval|mrr=0.533.ckpt


分析实验:
比较一下-GWN_R与-G相比，hits@1提升的实体中，那些实体属于学习了邻居信息的
#学习了邻居信息实体中(哪些是-GWN相比-G下降的，GWN_R相比-GWN提升)
学习了邻居信息实体中(哪些是-GWN相比-G下降的，GWN_R相比_G提升)


#另一个分析实验，探究一下是否图片的质量越高越有利于下游任务：

比较原始图片和带有邻居的图片在含有真实图片的链接预测效果
FB15K:_2 和 _3
YG15K:_2 和 _3


IKRL: 
YG15K: 0.372
_O: /home/xuyajing/Ne-MMKGC/output/link_prediction/YG15K/MMTransE1/epoch=1879-Eval|mrr=0.372.ckpt
bash IKRL.sh 0 2 4096 MMTransE1 1
FB15K: 0.496
_O: /home/xuyajing/Ne-MMKGC/output/link_prediction/FB15K/MMTransE1/epoch=1859-Eval|mrr=0.496.ckpt
bash IKRL.sh 0 3 512 MMTransE1 1

TBKGC: 
YG15K: 0.386
_O: /home/xuyajing/Ne-MMKGC/output/link_prediction/YG15K/TBKGC1/epoch=1899-Eval|mrr=0.387.ckpt
bash tbkgc.sh 0 2 4096 TBKGC1 1
FB15K: 0.515
_O: /home/xuyajing/Ne-MMKGC/output/link_prediction/FB15K/TBKGC1/epoch=1979-Eval|mrr=0.515.ckpt
bash tbkgc.sh 0 3 512 TBKGC1 1

将测试集中头尾预测不涉及含有真实图片的实体的三元组移除
