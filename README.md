# Edit_Scene 场景编辑与生成式仿真探索

> 本仓库仅用于个人技术能力展示与公开方向探索，主要展示自动驾驶场景编辑、新视角生成、三维场景表达与生成式仿真相关实验结果。  
> 仓库不包含公司内部代码、内部数据、模型权重、业务文档或可复现实验细节。展示内容仅用于技术交流。

## 项目简介

本项目围绕自动驾驶场景数据合成与生成式仿真方向进行探索，重点关注以下问题：

1. 如何基于多视角几何 / 三维重建结果构建可编辑的驾驶场景；
2. 如何结合 3D 场景表达与生成模型，实现新视角渲染、局部场景编辑和视觉补全；
3. 如何在场景编辑过程中保持较好的几何一致性、视角一致性和时序连续性；
4. 如何为后续自动驾驶世界模型、长尾场景构建、生成式仿真数据集建设提供基础能力。

整体目标不是单纯生成单帧图像，而是探索一种更适合自动驾驶场景的数据合成链路，使其能够支持：

- 场景动态元素编辑；
- 自车视角 / 行驶轨迹变化；
- 外部目标插入与位置调整；
- 新视角生成与局部视觉补全；
- 多视角一致性展示；
- 长尾交通场景构建；
- 生成一致性强的点云和7V摄像头拍摄数据
- 面向 world model 的数据组织与评估探索。

## 当前能力展示

目前已完成若干场景编辑与生成式仿真实验，主要包括：

### 1. 基础驾驶场景构建

基于公开/非敏感数据流程，对驾驶场景进行三维表达构建，并支持后续新视角渲染、场景编辑和结果可视化。

### 2. 场景动态元素编辑

支持对驾驶场景中的动态元素进行编辑实验，包括：

- 动态目标移除；
- 动态目标位置调整；
- 动态目标运动趋势编辑；
- 多目标组合场景构建；
- 输出构建后虚拟场景的点云数据。

### 3. 自车视角与行驶路线变化

支持对自车视角或行驶路线进行调整，用于模拟不同 ego trajectory 下的视觉结果，为后续长尾场景构建和生成式仿真提供基础。

### 4. 多视角一致性展示

针对插入目标或编辑目标，探索多相机 / 多视角下的显示一致性，关注目标外观、空间位置、遮挡关系和场景融合效果。

### 5. 场景编辑交互工具探索

基于开源三维可视化工具进行二次开发，探索面向场景目标和运动轨迹的交互式编辑能力。

## 技术方向

本项目主要关注以下技术方向：

- 3D 场景表达与新视角生成；
- 多视角几何约束下的场景编辑；
- 生成模型辅助的局部视觉补全；
- 自动驾驶场景数据合成；
- 长尾风险场景构建；
- 面向世界模型的数据组织与生成式仿真探索。

## 结果展示

### 场景编辑示例

| 原始数据 | 自车路线变化 + 动态目标移除 | 自车路线变化 + 新增目标 |
| :---: | :---: | :---: |
| ![原始视频](https://github.com/user-attachments/assets/6fa337da-f546-4aa0-b288-6db1fd43235f) | ![动态目标移除](https://github.com/user-attachments/assets/cb3e2373-3193-4c1f-bf3d-d3c77855d012) | ![新增目标](https://github.com/user-attachments/assets/d225bd38-7de9-4bab-b236-00dade2e48cb) |

### 交互式轨迹编辑界面

<img width="2455" height="1335" alt="trajectory_editing_interface" src="https://github.com/user-attachments/assets/b0ac605f-7cd6-47d7-a1e8-8d98ec7b41ef" />

### 目标建模与场景融合示例

以下展示目标对象与驾驶场景融合后的多视角效果，用于验证插入目标在不同视角下的空间一致性和外观一致性。

<img width="430" height="312" alt="object_modeling_example" src="https://github.com/user-attachments/assets/75cd8f47-8ca1-409e-9844-3f9b65c995a0" />

融合结果：

<img width="450" height="253" alt="camera_0" src="https://github.com/user-attachments/assets/b36d3f69-4c60-481b-bdb5-b48015cab35c" />
<img width="450" height="253" alt="camera_5" src="https://github.com/user-attachments/assets/26ea8ada-c0b4-4444-bab5-08107cf9d7da" />

### 自车视角变化示例

<img width="450" height="253" alt="ego_view_change" src="https://github.com/user-attachments/assets/0a876389-961d-4e00-b4f4-999bec401c20" />

### 目标运动趋势编辑示例

<img width="450" height="253" alt="object_motion_editing_1" src="https://github.com/user-attachments/assets/030fa7c7-7aed-4b2b-85c0-b122e45c6653" />
<img width="450" height="253" alt="object_motion_editing_2" src="https://github.com/user-attachments/assets/61416ee2-eb73-444f-9863-f7f71f8d591f" />

### 复杂目标运动示例

<img width="430" height="242" alt="complex_motion_1" src="https://github.com/user-attachments/assets/066d365e-cf4c-4f43-af07-88698a352ffc" />
<img width="430" height="242" alt="complex_motion_2" src="https://github.com/user-attachments/assets/0696b030-f7e0-489b-894e-e42051e19b29" />

### 多目标混合场景示例

<img width="430" height="242" alt="multi_object_scene_1" src="https://github.com/user-attachments/assets/5dc20847-9633-4714-b238-e3cbffa2bb12" />
<img width="430" height="242" alt="multi_object_scene_2" src="https://github.com/user-attachments/assets/391b6e6b-e108-41c5-afc5-cf608fb2f2af" />

### 特殊场景实例以及合成点云细节

<img width="430" height="242" alt="飞书20260429-172222" src="https://github.com/user-attachments/assets/1c5107ac-3d30-4ed0-8145-02fa2d50592f" />
<img width="1048" height="738" alt="image" src="https://github.com/user-attachments/assets/69aaa8b7-b2ad-48f4-9ba7-c175cb300a6b" />
<img width="951" height="742" alt="image" src="https://github.com/user-attachments/assets/426c529b-b04a-4d99-8f03-3103ec68bde6" />


## 后续探索方向

后续计划继续探索以下方向：

1. **连续片段级数据合成**  
   从单帧或短片段编辑扩展到更长时序的驾驶场景生成。

2. **长尾交通场景构建**  
   面向异常交通行为、复杂交互、危险 cut-in、逆行目标、碰撞风险等场景进行可控构建。

3. **多模态监督数据生成**  
   探索同时生成 RGB、depth、mask、pose、object state 等信息，为下游感知、预测和仿真任务提供数据支撑。

4. **世界模型数据集构建**  
   将数据组织为 history-condition-future 格式，为 future prediction、world model 微调和生成式仿真评估提供基础。

5. **生成模型 / 世界模型适配**  
   探索使用更强的 driving world model 或 video generation model，增强新视角补全、时序一致性和未来场景生成能力。

## 声明

本仓库仅作为个人技术能力展示和公开方向探索使用。

- 不包含公司内部代码；
- 不包含公司内部数据；
- 不包含公司内部模型权重；
- 不包含公司业务文档；
- 不包含可直接复现的完整工程实现；
- 不涉及任何未公开商业项目细节。

如相关展示内容存在不适合公开的部分，将及时进行调整或移除。
