# Gaussian 厨房

已从现有本地输入 `demo_assets/gray_kitchen/kitchen/gray_kitchen_15000.ply` 复制为 `kitchen.ply`。原文件保留，内容和坐标没有改变。入口为 `download_asset("gaussian_kitchen") / "kitchen.ply"`，供植物/机械臂示例的 `--kitchen-ply` 参数使用。

## 来源与文件

- 项目来源记录：[graphdeco-inria/gray](https://github.com/graphdeco-inria/gray)。本地 WanPhys 场景文档将该文件记录为 GRay 的预训练 Mip-NeRF360 kitchen 结果转换成标准 3DGS PLY。
- 本地同目录 `config.json` 记录 `source_path = data/360_v2/kitchen`、`iterations = 15000`、`sh_max_degree = 3`。这些是来源线索，不是再分发许可。
- PLY 头记录 binary little-endian、1,303,385 个 Gaussian；复制前后大小与 SHA-256 一致，见 `inventory.json`。
- 下载归档的固定版本、转换工具的确切提交、作者信息及数据单位与 `up_axis` 尚未完整核实，均不作推定。场景的桌面配准仍由 WanPhys 示例配置完成。

## 许可状态：`release_pending`

本地厨房输入目录未找到对应的许可证文本。源码、预训练重建结果和原始采集数据可能具有不同条款；不能根据 GRay 代码许可推断本 PLY 的许可。公开发布前须核实这个重建结果及源数据的再分发条件，保存真实许可与署名信息。

只复制该 PLY，不复制原 ZIP、训练检查点、TensorBoard 日志、相机训练清单、图像或测试输出。
