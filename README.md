# WanPhys Assets

WanPhys 的独立运行资产仓库。采用“一个顶层目录就是一个可下载资产包”的布局：代码保留在 WanPhys，场景模型、网格、纹理和必要的模型数据保存在这里。目录结构参考独立资产仓库的组织方式。

## 资产包布局

| 顶层目录 | 内容与状态 |
| --- | --- |
| `example_assets/` | 原 `wanphys/assets/` 的 30 个文件已按模型和用途分组，文件名与内容不变；`index.json` 保留旧文件名映射。 |
| `geometry_samples/` | 已迁入 `mesh_to_points_input.obj`。 |
| `gaussian_coast_cliff02/` | 已复制海岸场景清单、Gaussian PLY、环境光和碰撞审计网格，共 4 个运行输入。 |
| `gaussian_plant/` | 已复制植物 `plant.ply`，与 VoMP 固定提交中的文件一致；资产再分发许可待审查。 |
| `gaussian_kitchen/` | 已复制 GRay 厨房转换结果 `kitchen.ply`；来源版本和资产再分发许可待审查。 |
| `kinova_gen3/` | 已复制 8 个 Gen3 DAE 网格到 `meshes/`，附上游 LICENSE。 |

上述状态表示本地输入文件已经安装，不表示已经提交、推送、发布，或完成所有许可与运行验证。每个包的当前文件大小与 SHA-256 见 `inventory.json`；来源和未决事项见包内 README。

Gaussian 包只收录运行需要的输入。原 `demo_assets` 中的输入副本仍保留，历史视频、截图、训练检查点、训练数据和调试输出没有搬入本仓库。

`example_assets/` 将同一模型的网格、场景和纹理放在一起。例如，兔子的四个文件位于 `example_assets/meshes/bunny/`，机器人、流体、布料、软体、地形和点云分别归类。目录映射见包内 README 和 `index.json`。USD、URDF、材质和纹理之间的相对依赖必须整体保留。

## 配套 WanPhys 的访问约定

WanPhys 侧的目标调用接口是其原生公共工具；具体可用性以配套代码版本和实际迁移验证为准：

```python
from pathlib import Path

from wanphys.utils import download_asset

asset_directory: Path = download_asset("example_assets")
bunny_path: Path = asset_directory / "meshes" / "bunny" / "bunny.usd"
```

配套 WanPhys 的旧名称接口 `wanphys.examples.get_asset("bunny.usd")` 通过 `example_assets/index.json` 解析分组后的路径；不要再假设旧名称对应包根目录的平铺文件。

本地开发可通过 `WANPHYS_ASSET_PATH` 指向包含这些顶层包的目录，而不是某个包内部。该变量采用操作系统的路径列表分隔符：Windows 为 `;`，Linux/macOS 为 `:`。

```powershell
$env:WANPHYS_ASSET_PATH = "E:\project\wanphys\wanphys-assets"
```

```bash
export WANPHYS_ASSET_PATH="/path/to/wanphys-assets:/path/to/other-asset-packages"
```

已使用 Git LFS 管理的文件需要下载真实内容，不能把 LFS 指针文本当成模型文件使用。在本仓库目录执行：

```bash
git lfs install --local
git lfs pull
```

## 新增或更新资产包

- 顶层包名使用小写 `snake_case`。已迁移文件和上游包内部的文件名应保留大小写，不为命名整齐而破坏引用。
- 每个包必须提供 README，写清用途、入口文件、依赖文件、单位、坐标系和 `up_axis`；未知信息明确标为未知。
- 保存真实的上游许可文本、作者或权利人、来源 URL、版本或提交号，以及必要的署名要求。转换、裁剪或重建的资产还应记录源文件和处理方法。
- 整体迁移 USD/URDF 的相对依赖；在脱离原开发目录后验证模型可以加载。不要保留指向个人机器的绝对路径。
- `.gitattributes` 中列出的重型模型、纹理和数值数据使用 Git LFS。README、许可文本和来源元数据保持普通文本。
- 不提交视频输出、截图结果、运行日志、下载缓存、临时文件、凭据或其他 Git 仓库的 `.git` 目录。确有必要的演示媒体应单独说明用途和来源，而不是混入运行输出。
- 完成实际迁移后再生成文件大小和校验和清单，并验证仓库克隆后的真实 LFS 内容；不以历史清单代替当前文件核验。

## 许可与发布边界

本仓库不对全部资产授予统一许可。每个资产的使用和再分发条件由其真实来源许可决定；WanPhys 代码的许可不能替代第三方模型、纹理或数据的许可。

历史资产的来源和许可记录尚不完整。将文件放入本仓库不等于完成权利核验：**未确认来源或再分发条件的资产，在公开发布前必须逐项审查**。保留原始记录，不补写未经证实的作者、许可、来源或校验和。
