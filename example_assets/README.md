# 通用示例资产包

本包包含原 WanPhys 仓库 `wanphys/assets/` 的全部 30 个输入文件，现按相关模型和用途分组。此次只调整目录，不改变文件名、内容或场景参数；包内搬动前后逐文件 SHA-256 一致。`inventory.json` 记录分组后的相对路径以及原样保留的文件大小和 SHA-256，这不代表全部历史资产已经通过运行或许可审核。

## 分组布局

| 目录 | 内容 | 原输入数 |
| --- | --- | ---: |
| `meshes/bunny/` | `bunny.ply`、`bunny.png`、`bunny.usd`、`bunny.usda` | 4 |
| `meshes/primitives/` | `axis_cube.usda`、`sphere.obj` | 2 |
| `meshes/dragon/` | `dragon.usda` | 1 |
| `robots/` | `cartpole/`、`quadruped/`、`ant/`、`humanoid/`、`h1/` 分别存放对应机器人或运动数据 | 5 |
| `fluids/` | `corals/`、`koifish/`、`watermill/`；锦鲤的两个 USD 放在同一目录 | 4 |
| `cloth/` | `curvedSurface.usd`、`unisex_shirt.usd` | 2 |
| `soft/` | `Sphere_low.msh`、`cube_low.msh` | 2 |
| `terrain/lunar/` | 三份 lunar DTM TIFF | 3 |
| `sensors/contact/` | `sensor_contact_scene.usda` | 1 |
| `point_clouds/` | 五份 `simple_*` / `test_*` PLY | 5 |
| `metadata/` | 原始历史清单 `example_assets.json`，内容不变 | 1 |

`README.md`、`index.json` 和当前 `inventory.json` 是包级文档与索引，不计入上述 30 个历史输入。

## 路径接口

`wanphys.utils.download_asset("example_assets")` 返回本包根目录，直接使用时应拼接新的相对路径，例如 `meshes/bunny/bunny.usd`。

为保留旧场景中的名称，`index.json` 提供完整的 30 项映射：

```json
{
  "schema_version": 1,
  "assets": {
    "bunny.usd": "meshes/bunny/bunny.usd"
  }
}
```

上面是格式示意，实际索引包含全部原文件。配套 WanPhys 的 `wanphys.examples.get_asset("bunny.usd")` 应查找该索引；旧文件名不再表示根目录下存在同名文件。新代码也可使用明确的分组路径。现有场景继续选择原来的具体资产，不将相似名称视为可互换文件。

## 文件与坐标约定

模型、网格、地形数据和运动数据具有不同用途，不能假设全包采用同一单位或坐标轴。迁移时保留文件内的 USD 元数据、URDF 内容和既有场景的缩放配置；尚未逐资产核实的单位与 `up_axis` 均视为未知。

同一模型的 USD、材质和纹理必须一起管理；分组不修改文件内的引用。如果补充缺失依赖，应按照主文件原有相对引用放置。例如水车的纹理应位于 `fluids/watermill/textures/`，不能放回包根目录或随意重命名。

## 已知历史问题

以下问题在迁移前的资产检查中已存在，不是迁移完成的验收结果，也不应在迁移过程中被静默修复或删除：

| 文件 | 已知情况 |
| --- | --- |
| `meshes/bunny/bunny.usda` | OpenUSD Sdf 在第 9 行附近报告解析错误。另一个文件 `meshes/bunny/bunny.usd` 可以解析；二者不能擅自互相替换。 |
| `fluids/watermill/watermill.usdc` | 引用了 `./textures/color_0C0C0C.exr`，但原资产目录缺少该文件，分组后仍未补造纹理。 |
| `point_clouds/simple_cloud.ply` | 原文件为空，大小为 0 bytes。 |

公开发布或宣称场景可运行前，应单独确认这些文件的用途和处理决定。

## 来源、许可与核验

`metadata/example_assets.json` 是原来的 `example_assets.json`，仅记录了 6 个文件的历史源路径、提交号、文件大小和校验和，不是全包许可清单，也不是当前文件完整性的保证。迁移前检查已经发现其中部分大小和校验和与实际文件不符；保留其原始字节作为历史记录，不据此声称全部文件已通过校验。

其余文件也必须补齐可核实的来源、作者或权利人、版本以及真实许可文本。不能因为它们原先位于 WanPhys 仓库，就统一认定适用 WanPhys 代码许可。来源或再分发条件未确认的文件，公开发布前必须完成审查。

当前 `inventory.json` 与 `index.json` 已同步分组路径。后续变更应同时维护路径映射和实际文件的校验信息，并与 `metadata/` 下的历史记录明确区分。
