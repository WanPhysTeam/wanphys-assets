# WanPhys Assets

WanPhys 的独立运行资产仓库。完整的机器人、模型或场景各自作为独立顶层包；包内保留 meshes/、textures/ 等相关依赖。

选择一个模型只下载它的包，不先下载全部示例资源，也不需要远端总索引。物理代码与示例编排保留在 WanPhys 代码仓库。

## 顶层包

原先 `example_assets/` 中的 30 个输入已拆成以下 22 个独立包。文件名、内容和各自所需的相对依赖保持不变，旧的大包目录与路径索引不再保留。

| 包 | 内容 |
| --- | --- |
| [`axis_cube/`](axis_cube/README.md) | 坐标轴/基础形状场景；1 个输入 |
| [`bunny/`](bunny/README.md) | 兔子网格、USD 场景和图像；4 个输入 |
| [`cartpole/`](cartpole/README.md) | cartpole 机器人场景；1 个输入 |
| [`corals/`](corals/README.md) | 流体示例使用的珊瑚几何；1 个输入 |
| [`soft_cube/`](soft_cube/README.md) | 低分辨率立方体体网格；1 个输入 |
| [`curved_surface/`](curved_surface/README.md) | 弯曲曲面/布料测试场景；1 个输入 |
| [`dragon/`](dragon/README.md) | 龙网格场景；1 个输入 |
| [`asset_metadata/`](asset_metadata/README.md) | 原 example_assets.json 历史来源清单；1 个输入 |
| [`h1_motion/`](h1_motion/README.md) | H1 示例使用的运动输入数据；1 个输入 |
| [`koifish/`](koifish/README.md) | 原始锦鲤及带关节的锦鲤场景；2 个输入 |
| [`lunar_apollo17/`](lunar_apollo17/README.md) | lunar_dtm_nac_apollo17_1.TIF 地形输入；1 个输入 |
| [`lunar_rumker/`](lunar_rumker/README.md) | lunar_dtm_rumkerdom10_1.TIF 地形输入；1 个输入 |
| [`lunar_spwrinkle/`](lunar_spwrinkle/README.md) | lunar_dtm_spwrinkle1_1.TIF 地形输入；1 个输入 |
| [`ant/`](ant/README.md) | Ant MJCF 场景；1 个输入 |
| [`humanoid/`](humanoid/README.md) | Humanoid MJCF 场景；1 个输入 |
| [`quadruped/`](quadruped/README.md) | Quadruped URDF 场景；1 个输入 |
| [`sensor_contact/`](sensor_contact/README.md) | 接触传感器示例的 USD 场景；1 个输入 |
| [`point_cloud_samples/`](point_cloud_samples/README.md) | 小型点云/网格输入样例集合；5 个输入 |
| [`sphere/`](sphere/README.md) | 球体 OBJ 网格；1 个输入 |
| [`soft_sphere/`](soft_sphere/README.md) | 低分辨率球体体网格；1 个输入 |
| [`unisex_shirt/`](unisex_shirt/README.md) | unisex shirt 布料网格；1 个输入 |
| [`watermill/`](watermill/README.md) | 水轮 USD 模型；1 个输入 |

另外若干包保持原内容和布局，或新增独立场景包：

| 包 | 内容 |
| --- | --- |
| [`geometry_samples/`](geometry_samples/README.md) | `mesh_to_points_input.obj` |
| [`gaussian_plant/`](gaussian_plant/README.md) | 植物 Gaussian `plant.ply` 与来源代码许可快照 |
| [`gaussian_kitchen/`](gaussian_kitchen/README.md) | GRay 厨房转换结果 `kitchen.ply` |
| [`gaussian_coast_cliff02/`](gaussian_coast_cliff02/README.md) | 海岸清单、Gaussian PLY、环境光和碰撞审计网格 |
| [`kinova_gen3/`](kinova_gen3/README.md) | 8 个 Gen3 DAE 网格位于 `meshes/`，附上游 LICENSE |
| [`new_largecity/`](new_largecity/README.md) | 城市洪水示例 OBJ/MTL 与调色板贴图；3 个输入 |
| [`skybox/`](skybox/README.md) | 天空盒 JPEG；3 个输入 |

每个包提供自己的 README 和 `inventory.json`。清单只登记本包实际输入的大小和 SHA-256，不把历史来源清单当成当前完整性证明。若模型原来就存在缺失依赖或无效文件，包内 README 会继续说明；按模型拆包不是修复这些内容。

此布局替代原来的 `example_assets/` 大包，需要配套支持独立包名的 WanPhys 代码。仍使用旧聚合路径的代码应先更新；需要复现旧布局时可使用本仓库的历史提交。发布顺序应先资产、后调用代码，本地开发可使用下文的资产根目录配置。

## 配套 WanPhys 的访问方式

直接使用 WanPhys 原生公共接口下载选中的包：

```python
from pathlib import Path

from wanphys.utils import download_asset

asset_directory: Path = download_asset("bunny")
bunny_path: Path = asset_directory / "bunny.usd"
```

此调用只获取 `bunny/` 及其包内文件，不会连带获取珊瑚、月面地形或 Gaussian kitchen 等其他顶层包。需要可复现版本时，显式传入已发布的提交号作为 `revision`；已完成的同名分支缓存不会自动刷新。

配套 WanPhys 的 `wanphys.examples.get_asset("bunny.usd")` 继续作为旧文件名入口。旧分组名称（如 `meshes/bunny/bunny.usd`）也由 WanPhys 代码中的显式别名直接指向 `bunny/bunny.usd`，不下载远端索引或全部媒体。以配套代码版本为准。

`wanphys.examples.get_assets_dir(asset_folder)` 现在要求显式包名，例如 `get_assets_dir("bunny")`。旧的无参数调用及把全部资源当成一个目录的用法需要迁移；不再有聚合 `example_assets` 包或返回全部媒体目录的接口。

## 本地开发与 Git LFS

本地开发可通过 `WANPHYS_ASSET_PATH` 指向包含顶层包的目录，而不是包内部。变量使用操作系统的路径列表分隔符：Windows 为 `;`，Linux/macOS 为 `:`。

```powershell
$env:WANPHYS_ASSET_PATH = "E:\project\wanphys\wanphys-assets"
```

```bash
export WANPHYS_ASSET_PATH="/path/to/wanphys-assets:/path/to/other-asset-packages"
```

公共下载工具会在缺少包时获取该包的真实 Git LFS 内容；机器需要 Git、Git LFS 和可用的远端访问。若手动克隆仓库，可跳过全仓 LFS 自动展开，然后只拉需要的包：

```bash
GIT_LFS_SKIP_SMUDGE=1 git clone https://github.com/WanPhysTeam/wanphys-assets.git
cd wanphys-assets
git lfs install --local
git lfs pull --include="bunny/**" --exclude=""
```

上面的命令需要所选分支已经包含新布局。不要把 LFS 指针文本当作模型，也不必为了单个示例执行不带包限制的全仓 LFS 下载。

## 新增或更新一个包

- 顶层包名采用小写 `snake_case`；同一个机器人、模型或场景的必要网格、纹理和配置放在同一包内。保留上游文件名大小写与相对引用。
- 提供包内 README，列明用途、入口文件、依赖、单位、坐标系和 `up_axis`；未知内容明确写未知，不推断统一米制或轴向。
- 记录真实来源 URL、作者或权利人、版本/提交、转换步骤和源文件；保存实际适用的许可文本与署名要求。不把来源仓库的代码许可证直接当作模型许可证。
- 为实际输入生成包内 `inventory.json`，记录相对路径、字节数和 SHA-256；同时保留可核实的来源信息。改动后核验工作文件以及冷缓存/克隆后的真实 LFS 内容。
- 重型模型、图像和数值数据按 `.gitattributes` 使用 Git LFS；README 和当前清单保留普通 Git 文本。需要逐字节保留的原始 XML/URDF/JSON 或许可快照应设置 `-text`，避免换行归一化改变哈希。
- 在脱离原开发目录后检查依赖完整性；运行所需路径不能指向个人机器的绝对目录。不要为了拆包重写物理场景参数或几何内容。
- 不收录视频/截图输出、训练产物、运行日志、下载缓存、临时文件、凭据或嵌套 `.git`。Gaussian 包只收录运行输入，原开发目录中的历史材料不作为运行资产批量搬入。
- 发布新增包后，再更新 WanPhys 中需要的调用者或旧名称别名。没有可下载的远端包时，不把未发布布局声称为可在线运行。

## 许可边界

本仓库不对全部资产授予统一许可。每项资产的使用与再分发条件取决于真实来源；物理引擎的代码许可不能替代第三方模型、纹理或数据的许可。

历史来源和许可记录尚不完整，包内 README 保留已知事实与未决事项。文件迁移、提交、推送或哈希一致都不代表权利核验完成：未确认来源或再分发条件的资产，应在公开再分发前逐项审查，不能补写未经证实的作者、许可证或来源。
