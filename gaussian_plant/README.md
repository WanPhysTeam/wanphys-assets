# Gaussian 植物

已从现有本地输入 `demo_assets/vomp_plant.ply` 复制为 `plant.ply`；原文件保留，PLY 内容没有修改。入口为 `download_asset("gaussian_plant") / "plant.ply"`，可作为 Gaussian 示例的 `--ply` 参数。

## 来源与文件

- 来源仓库：[nv-tlabs/VoMP](https://github.com/nv-tlabs/VoMP)。
- 固定提交：`ac6826f25ca5cfa122eb7bacb74be91b5a9eadf4`。
- 上游文件：[`gradio/examples/plant.ply`](https://github.com/nv-tlabs/VoMP/blob/ac6826f25ca5cfa122eb7bacb74be91b5a9eadf4/gradio/examples/plant.ply)。
- 已用本地 VoMP Git 对象验证：复制源与该提交的 PLY 是同一个 Git blob；复制后 SHA-256 也一致，详见 `inventory.json`。
- PLY 为 binary little-endian，包含 53,954 个 Gaussian 和最高三阶 SH 属性。它不声明物理单位或 `up_axis`，两者在资产层面仍为未知；示例的缩放与旋转不烘焙进此文件。

## 许可状态：`release_pending`

附带的 `LICENSE.source-code.txt` 是上述提交的仓库 LICENSE 内容，按文本保存并补齐末尾换行。它是 Apache-2.0 **源码许可参考**，不能单独证明本植物数据适用相同许可。

同一提交的 README 区分了源码的 Apache-2.0 与模型的 NVIDIA Open Model License，并说明部分植被数据不能公开发布。当前证据尚不能明确将 `plant.ply` 归入某项资产授权，因此不将其标为“Apache-2.0 植物资产”。公开再分发前，必须确认该文件自身的许可范围及必要署名。

本包没有包含 VoMP 代码、模型权重、训练数据或演示视频。
