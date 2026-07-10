# Edit_Scene 自动驾驶场景编辑与生成式仿真展示

> 本仓库仅用于个人技术能力展示与公开方向探索，主要展示自动驾驶场景编辑、新视角生成、三维场景表达与生成式仿真相关实验结果。  
> 仓库不包含公司内部代码、内部数据、模型权重、业务文档或可复现实验细节。展示内容仅用于技术交流。

## 项目简介

本项目围绕自动驾驶场景可控编辑、三维重建、合成点云和多视角视频生成进行展示。当前结果不再只停留在单一场景或单帧图像编辑，而是覆盖了从多数据建图、动态目标编辑、ego 轨迹变化、合成点云输出，到 6V 天气一致性编辑和 world model / video generation 适配的一整条实验链路。

展示内容主要对应以下能力：

- 多组采集数据共同构建同一大规模 3DGS 场景；
- 昼夜场景下的目标插入、目标移除和自车路线变化；
- 合成场景对应的 BEV 点云、实际采集点云和合成点云对比；
- 极端交通场景合成与点云级结果检查；
- 行人、电动车等非车辆目标的多视角重建；
- 6V 视频级天气编辑，包括雪天、雨天和夜晚风格迁移；
- 基于点云 / 3DGS guidance 的 world model 数据组织、推理和微调实验。

## 当前能力展示

当前展示结果由多个子方向组成，重点验证编辑后的视觉结果、空间关系和点云结果是否能够互相对应。

### 1. 多数据三维场景构建

基于多段数据的 SLAM / 点云结果，将不同采集片段对齐到同一场景中，并用于构建更完整的大规模 3DGS 背景。该部分主要服务于远处建筑、路面和大范围背景补全，减少单次采集导致的视角覆盖不足。

### 2. 目标级场景编辑

围绕动态目标进行可控编辑，展示了同一原始片段下的多种编辑结果：

- 动态目标移除；
- 外部车辆 / 目标插入；
- 目标位置与运动轨迹调整；
- 多目标组合场景构建；
- 编辑后 RGB 视频与合成点云同步输出。

### 3. 自车视角与行驶路线变化

支持改变 ego trajectory，并在新的自车路线下重新渲染场景。展示结果中包含“自车路线变化 + 新增目标”“自车路线变化 + 移除场景物体 + 新增目标”等组合，用于验证几何约束、遮挡关系和时序连续性。

### 4. 点云级合成与对比

除 RGB 结果外，当前展示同步给出 BEV 点云比较、实际采集点云和合成点云，用于检查插入目标、被移除物体、路面结构和背景之间的空间一致性。

### 5. 场景编辑交互工具探索

基于三维可视化工具进行二次开发，支持在点云 / 3D 场景中编辑目标轨迹、暂存多条轨迹并输出后续渲染和点云合成所需的数据。

### 6. 多视角天气与 world model 适配

展示了 6V 重建视频到雪天、雨天、夜晚等天气 / 光照条件的连续视频编辑。同时整理了面向 VISTA / driving world model 的数据集 meta、点云 guidance、LoRA 微调和推理结果输出流程。

## 技术方向

本项目主要关注以下技术方向：

- Multi-session SLAM / 点云融合辅助的大规模 3DGS 场景构建；
- 动态目标的 3DGS 资产接入、轨迹编辑和多视角渲染；
- 基于点云条件图的 RGB / depth / BEV 对齐检查；
- 自动驾驶长尾场景的数据合成与可视化验证；
- 6V / 多相机视频的一致性天气编辑；
- 面向 VISTA / world model 的数据组织、LoRA 微调和生成式仿真探索。

## 结果展示

### 场景编辑示例

**展示结果中，为了确保上传 GitHub 稳定，采用 5 fps 的 GIF 生成，实际视频为 10 fps。**

以下展示目标对象与驾驶场景融合后的效果，用于观察插入目标在连续帧、多视角和背景遮挡关系中的稳定性。

<img width="430" height="312" alt="object_modeling_example" src="https://github.com/user-attachments/assets/75cd8f47-8ca1-409e-9844-3f9b65c995a0" />

### 交互式轨迹编辑界面

<img width="2455" height="1335" alt="trajectory_editing_interface" src="https://github.com/user-attachments/assets/b0ac605f-7cd6-47d7-a1e8-8d98ec7b41ef" />

### 0. 多数据构建大规模 3DGS 场景

基于 [Multi-Session SLAM](https://github.com/CYH040306/show_lidar-slam) 结果，将多组采集数据融合到同一场景坐标系中，再用于 3DGS 背景建模，提升大范围道路、建筑和远景区域的覆盖。

<img width="2417" height="1185" alt="image" src="https://github.com/user-attachments/assets/db230d3b-695a-44db-90d5-6ddfa72af280" />


### 1. 白天场景
白天场景展示原始数据、目标新增、ego 路线变化、场景物体移除以及多种编辑操作叠加后的结果。下方点云对比用于检查合成点云与实际采集点云在 BEV 结构上的一致性。

| 原始数据 | 新增目标车辆 | 自车路线变化 + 新增目标 | 移除场景物体 + 新增目标 |  自车路线变化 + 移除场景物体 + 新增目标 |
| :---: | :---: | :---: | :---: | :---: |
| <img src="https://github.com/user-attachments/assets/c58fb4cf-e3fc-46e7-b208-59613d65d619" alt="0000" width="600" /> | <img src="https://github.com/user-attachments/assets/dfc5123f-49aa-4d56-99d4-d131f6e3ed36" alt="2222" width="600" /> | <img src="https://github.com/user-attachments/assets/c6672e19-b873-489e-865b-338e9312b412" alt="1111" width="600" /> | <img width="600" height="338" alt="3333" src="https://github.com/user-attachments/assets/32d0400b-adb8-4f7a-834f-142f9ce3945c" /> | <img width="600" height="338" alt="4444" src="https://github.com/user-attachments/assets/6ca637de-5b76-4108-9467-7719fda8c5db" />

| BEV 点云比较 | 实际采集点云 | 合成点云 |
| :---: | :---: | :---: |
| <img width="1250" height="625" alt="直行停车_background_compare" src="https://github.com/user-attachments/assets/00bb8e84-4670-4da5-9afd-85db92a01583" /> | <img width="1100" height="623" alt="2" src="https://github.com/user-attachments/assets/4fed0cea-cb72-4fb6-b172-32da8cee4366" /> | <img width="1100" height="623" alt="1" src="https://github.com/user-attachments/assets/14e1bf6a-2078-4ec7-a2c8-69ac2b08bcb6" /> |


### 2. 夜晚场景
夜晚场景用于验证低照度条件下的目标插入、路线变化和物体移除效果，重点观察插入目标的亮度融合、道路关系和连续帧稳定性。

| 原始数据 | 新增目标车辆 | 自车路线变化 + 新增目标 | 移除场景物体 + 新增目标 |  自车路线变化 + 移除场景物体 + 新增目标 |
| :---: | :---: | :---: | :---: | :---: |
| <img width="600" height="400" alt="camera_0" src="https://github.com/user-attachments/assets/ba469a2a-65e6-4a1f-b7a6-0ed3742cbb6a" /> | <img width="800" height="450" alt="23-0" src="https://github.com/user-attachments/assets/0660fbba-b533-4f6e-be1e-3d63f1b171ff" /> | <img width="800" height="450" alt="23-0_novel" src="https://github.com/user-attachments/assets/59da0201-14d8-49a5-886c-c9f04e520592" /> | <img width="800" height="450" alt="23-0_delete" src="https://github.com/user-attachments/assets/ca42352d-23b1-4b82-b777-1914dfe9e815" /> | <img width="800" height="450" alt="23-0_novel_delete" src="https://github.com/user-attachments/assets/d46d535e-98e8-43f1-a951-6344d657631a" /> |


### 3. 极端场景合成（以夜晚为例）
该部分展示更复杂的夜晚长尾场景合成，同时给出 BEV 点云比较和局部细节检查，用于验证合成目标和背景点云在空间上的可解释性。

| 合成视频 | BEV 点云比较 | 具体比较 |
| :---: | :---: | :---: |
| <img width="430" height="242" alt="飞书20260429-172222" src="https://github.com/user-attachments/assets/1c5107ac-3d30-4ed0-8145-02fa2d50592f" /> | <img width="1000" height="500" alt="zhanshi_background_compare" src="https://github.com/user-attachments/assets/d06b2f5d-1fba-4a3b-8894-565ac0688ab2" /> | <img width="2360" height="1441" alt="image" src="https://github.com/user-attachments/assets/9e68642d-b2da-4337-ba28-d0df220b6fa3" /> |


### 4. 行人、电动车场景重建
除车辆外，也展示行人、电动车等交通参与者在不同相机视角下的重建结果，用于检查非刚性 / 小目标类别在多视角中的外观和位置一致性。

| 正向视角 | 侧向视角1 | 侧向视角2 |
| :---: | :---: | :---: |
| <img width="600" height="338" alt="cam_0" src="https://github.com/user-attachments/assets/ecdc2d2f-381c-4c56-9d2f-540af62682e6" /> | <img width="600" height="338" alt="cam_4" src="https://github.com/user-attachments/assets/9ac46082-b33b-47e1-bcb5-73190d4d881c" /> | <img width="600" height="338" alt="cam_5" src="https://github.com/user-attachments/assets/253007b8-e8e3-49ce-a3e9-41cec720d636" /> |

| 正向视角 | 侧向视角1 | 侧向视角2 |
| :---: | :---: | :---: |
| <img width="600" height="338" alt="0" src="https://github.com/user-attachments/assets/5ae096f9-0f5b-4d7d-acba-eff091407955" /> | <img width="600" height="338" alt="3" src="https://github.com/user-attachments/assets/9e77f8a2-61dc-4563-9c49-9fa844ea9d46" /> | <img width="600" height="338" alt="5" src="https://github.com/user-attachments/assets/9af40cc9-4bb5-457a-9961-00ed6b18e668" /> |


### 5. 6V 一致性天气编辑
基于重建后的 6V 视频结果进行天气和光照编辑，展示同一多相机片段在雪天、雨天和夜晚条件下的连续生成效果，关注跨视角风格一致性和时序稳定性。

#### 1. 重建6V视角视频
<img width="700" height="264" alt="0100_6v" src="https://github.com/user-attachments/assets/c130cad0-1a47-4ddc-aaad-7acc511a8b71" />

#### 2. 重建视频改雪天
<img width="700" height="264" alt="0100_6v_snowy gen" src="https://github.com/user-attachments/assets/fd9f5273-05d2-4e39-9fd6-b74f0635254e" />

#### 3. 重建视频改雨天
<img width="700" height="264" alt="0100_6v_rainy gen" src="https://github.com/user-attachments/assets/77f199fd-0736-4cfc-8384-67cb9f358d64" />

#### 4. 重建视频改夜晚
<img width="700" height="264" alt="0100_6v_night gen" src="https://github.com/user-attachments/assets/adbea2fd-0ee3-4dd0-afe5-1e04bd3b72a7" />


## 后续探索方向

后续会在当前展示链路基础上继续补强以下方向：

1. **连续片段级数据合成**  
   将当前短片段编辑和合成点云输出扩展到更长时序，重点提升长时间轨迹、遮挡变化和跨相机一致性。

2. **长尾交通场景构建**  
   面向异常交通行为、复杂交互、危险 cut-in、逆行目标、碰撞风险等场景进行可控构建，并同步输出 RGB、点云和轨迹信息。

3. **多模态监督数据生成**  
   在现有 RGB 和点云结果基础上，继续补齐 depth、mask、pose、object state 等监督信号，为下游感知、预测和仿真任务提供数据支撑。

4. **世界模型数据集构建**  
   将真实数据、编辑数据和合成点云组织为 history-condition-future 格式，用于 future prediction、world model 微调和生成式仿真评估。

5. **生成模型 / 世界模型适配**  
   继续适配 driving world model、video generation model 和多视角天气生成模型，增强新视角补全、时序一致性和未来场景生成能力。

## 声明

本仓库仅作为个人技术能力展示和公开方向探索使用。

- 不包含公司内部代码；
- 不包含公司内部数据；
- 不包含公司内部模型权重；
- 不包含公司业务文档；
- 不包含可直接复现的完整工程实现；
- 不涉及任何未公开商业项目细节。

如相关展示内容存在不适合公开的部分，将及时进行调整或移除。
