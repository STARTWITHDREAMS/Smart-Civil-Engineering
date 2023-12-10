# 岷江纯玩白鹤亮翅项目
实现挂篮在使用过程中的受力（应力）和变形监测、预警。采用图形化和数据化模式呈现不同施工阶段下，实时的应力情况监测和变形情况监测。有预警预制。单套成本控制在3万元以内。
# 团队：『起个名字』小组
杨丰宇、邹雅琳、徐捷、冯梦丹、胡骢
# 共情
![Central_Topic](https://github.com/STARTWITHDREAMS/Smart-Civil-Engineering/assets/139680265/6b72ed3a-a14e-45f9-8aeb-92c70cd35965)
# 定义
## 痛点
### 1.桥梁维护工程师：
各方面数据多而不直观；
难以准确获取桥梁挂篮的应力和变形监测数据；
操作中设备遭到破坏但检测不及时导致作业和安全问题发生；
恶劣天气条件下停止作业，并将挂篮设备固定在合适位置。  
### 2.施工单位联合体：
安装复杂，成本高；
难以全面了解桥梁的工况和状态：检查各点位对人力成本要求高且精确度有上限，分析环境分析数据的专业人士成本高；
## HMW定义
为【具有专业知识的设备操作员和相应的施工单位联合体】设计制作一个【结构简单，可靠性高，实时监测各点位，实时分析的挂篮智能监控系统】，使得【投资成本降低，实现安全施工】
# 构想
![image](https://github.com/STARTWITHDREAMS/Smart-Civil-Engineering/assets/139680265/458addf8-2af3-4231-88e2-16818e16b0d0)

## 摄像头监测
### 摄像头安置
### 基于光流的运动目标检测算法
利用图像序列中像素在时间域上的变化以及相邻帧之间的相关性来找到上一帧跟当前帧之间存在的对应关系，从而计算出相邻帧之间物体的运动信息
![image](https://github.com/STARTWITHDREAMS/Smart-Civil-Engineering/assets/139680265/5633ab2c-51fe-4414-bc1a-647d7f4ac089)
### 模型的优势
仅经过一次细化，GMFlow在具有挑战性的Sintel基准测试中胜过了31次细化的RAFT。

基本的GMFlow模型（无需细化）在Sintel数据（436x1024）上在V100上运行时间为57ms，A100上为26ms。

在高端GPU上（例如A100），GMFlow比RAFT获得更多的加速，因为GMFlow不需要大量的顺序计算。

GMFlow还简化了反向流计算，无需两次前向网络。双向流可以用于通过前向-后向一致性检查进行遮挡检测。
### 数据集的组织
```
datasets
├── FlyingChairs_release
│   └── data
├── FlyingThings3D
│   ├── frames_cleanpass
│   ├── frames_finalpass
│   └── optical_flow
├── HD1K
│   ├── hd1k_challenge
│   ├── hd1k_flow_gt
│   ├── hd1k_flow_uncertainty
│   └── hd1k_input
├── KITTI
│   ├── testing
│   └── training
├── Sintel
│   ├── test
│   └── training

```
### 模型的评估
可以通过运行以下命令来对模型进行一个评估
`CUDA_VISIBLE_DEVICES=0 python main.py --eval --val_dataset things sintel --resume pretrained/gmflow_things-e9887eda.pth `
### 模型的训练
FlyingChairs、FlyingThings3D、Sintel 和 KITTI 数据集上的所有训练脚本都可以在 scripts/train_gmflow.sh 和 scripts/train_gmflow_with_refine.sh 中找到。

请注意，基本的 GMFlow 模型（未经优化）可以在 4 个 16GB V100 GPU 上训练。为了进行精细的训练，默认情况下需要 8 个 16GB V100 或 4 个 32GB V100 或 4 个 40GB A100 GPU。可能需要根据硬件调整批处理大小和训练迭代。
### 实验结果
![image](https://github.com/STARTWITHDREAMS/Smart-Civil-Engineering/assets/139680265/65354917-eda9-4044-80d5-e06a04fe0ae1)
### 数据的实时现实
设计一个数据显示系统，将位移情况实时的反映到显示屏上，并且根据位移进行受力分析。

## 传感器监测
![image](https://github.com/STARTWITHDREAMS/Smart-Civil-Engineering/assets/139680265/671f38cb-085d-4589-8d43-4d0ce63d2e21)
# 核心技术分析
## 痛点匹配检查表
![image](https://github.com/STARTWITHDREAMS/Smart-Civil-Engineering/assets/139680265/0cf653c9-118c-4f68-9c13-536013f6f471)
![image](https://github.com/STARTWITHDREAMS/Smart-Civil-Engineering/assets/139680265/7c0b70b7-2fc5-4915-afe8-2b7eeedc4b68)
## 核心技术分析-论文综述
![image](https://github.com/STARTWITHDREAMS/Smart-Civil-Engineering/assets/139680265/82614484-e9a2-435f-9666-40981c18ec8e)
