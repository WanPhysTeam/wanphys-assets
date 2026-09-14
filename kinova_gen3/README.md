# Kinova Gen3 7-DoF 网格

本包只包含现有 Gaussian 植物/机械臂场景使用的 8 个 DAE 视觉网格，入口目录为 `download_asset("kinova_gen3") / "meshes"`。向示例的 `--kinova-mesh-directory` 传入该目录。

```text
meshes/
  base_link.dae
  shoulder_link.dae
  half_arm_1_link.dae
  half_arm_2_link.dae
  forearm_link.dae
  spherical_wrist_1_link.dae
  spherical_wrist_2_link.dae
  bracelet_no_vision_link.dae
```

## 来源和坐标

- 来源：[Kinovarobotics/ros2_kortex](https://github.com/Kinovarobotics/ros2_kortex)，上游目录为 `kortex_description/arms/gen3/7dof/meshes/`。
- 现有场景的来源记录指向 [`0.2.6`](https://github.com/Kinovarobotics/ros2_kortex/tree/0.2.6/kortex_description/arms/gen3/7dof/meshes)；本地副本来自 `demo_assets/kinova_gen3_0_2_6/`。
- 另已检查本地上游 Git checkout `c50057a02fb64e854b2759261994f43173bec703`：8 个 DAE 统一为 LF 后与该 checkout 的对应文件全部相同。本次没有把这个提交与 `0.2.6` 标签强行等同，也没有重新访问远程核实标签。
- 每个 DAE 都声明 `<unit name="meter" meter="1"/>` 和 `Z_UP`，即米制、Z-up；未发现外部 `init_from` 纹理引用。
- 复制保留现有输入的原字节，包括换行；校验结果见 `inventory.json`。这些是视觉网格，不是完整机器人 URDF、控制器或动力学参数包。

## 许可

`LICENSE` 从本地 `ros2_kortex/LICENSE` 原样复制，包含 Kinova inc. 的三条款 BSD 风格许可和原文件附带的 Protocol Buffer 许可段落。保留完整文本，不以 WanPhys 的许可替换它。

当前已保存源码仓库级许可和可核实的本地文件对应关系。正式公开发布前仍应核实所选网格适用条款、上游固定版本和署名要求；本地复制和哈希一致不等于完成全部发布审核。

原始 `demo_assets` 文件与上游 checkout 均未修改。本包不包含上游 `.git`、抓手资源、机器人控制软件或视频输出。
