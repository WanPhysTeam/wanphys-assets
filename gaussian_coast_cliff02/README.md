# Gaussian 海岸与流体输入

本包从现有 `demo_assets/gaussian_coast_cliff02/` 逐字节复制以下运行输入，原目录保留。入口目录为 `download_asset("gaussian_coast_cliff02")`，供独立海岸示例的 `--coast-assets` 参数使用。

| 文件 | 用途 |
| --- | --- |
| `coast.json` | 场景清单、相机、外观、解析碰撞代理和来源记录。 |
| `coast.ply` | 960,000 个采样 Gaussian；不是原始 Gaussian Splashing 模型。 |
| `environment.npz` | Aristea Wreck 环境的线性 RGB 数据，数组键为 `rgb`。 |
| `collision_mesh.npz` | 与海岸同源的三角网格审计数据；不表示流体已使用精确三角碰撞。 |

四个文件总计 77,291,540 bytes，复制前后 SHA-256 一致，见 `inventory.json`。`coast.json` 关闭 Git 换行转换，以保留输入清单的原始字节。

## 来源与处理记录

`coast.json` 和已有本地 `coast_asset_candidates/ASSET_SOURCES.md` 记录：

- 海岸：[Poly Haven Coastal Cliff 02](https://polyhaven.com/a/coastal_cliff_02)，作者 Rob Tuytel，记录许可为 CC0-1.0；原始来源是带纹理的摄影测量网格。
- 环境：[Poly Haven Aristea Wreck](https://polyhaven.com/a/aristea_wreck)，作者 Greg Zaal，记录许可为 CC0；原始输入为 `aristea_wreck_2k.hdr`。
- 对应许可页面：[Poly Haven License](https://polyhaven.com/license)。这里记录的是本地已有来源证据，本次没有重新确认在线页面或上游文件版本。

已有离线转换脚本将海岸 glTF 转为 Z-up、米制，缩放为 `0.24`，平移为 `(1.9, 0.0, 0.15)`；完整旋转矩阵保存在 `coast.json` 的 `scan_transform` 中。流体波向为 `+X`。Gaussian 由纹理表面采样生成；碰撞清单采用湿岩壁的轴对齐分条近似，不能将其称为精确三角碰撞。

环境转换脚本将 Radiance RGBE 解码为线性 RGB，并按每个 2×2 像素块求均值后保存为 NPZ。本次不重新生成资产，也不更改相机、浪形、外观或录制参数。

## 发布核验

当前保留了来源 URL、作者和既有 CC0 声明，但本地没有独立的 CC0 许可文本快照；上游下载文件的固定版本和离线转换脚本版本也未完整归档。发布审核仍应补齐这些证据，不将本包整体改标为 Apache-2.0。

包内没有原始 glTF/纹理/HDR、站点预览图、参考视频、录制输出或调试状态；原始素材和历史输出仍在本地开发目录。
