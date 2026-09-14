# 兔子模型

兔子网格、USD 场景和图像。顶层 `bunny/` 是一个独立下载包，输入文件名和字节保持不变。

## 入口与依赖

- `bunny.ply`
- `bunny.png`
- `bunny.usd`
- `bunny.usda`

使用 `wanphys.utils.download_asset("bunny")` 获取本包目录，再拼接上面所需的文件名；不需要下载其他模型包。

此次检查未发现这些输入引用其他顶层资产包的文件。USD/URDF/OBJ 的相对依赖仍应整体保存在本包内；未来新增 meshes/、textures/ 等子目录时不能破坏原引用。

## 坐标与尺度

- `bunny.usd` 的原始 USD 元数据：`metersPerUnit=1.0`，`upAxis=Y`，`defaultPrim=root`。

以上是文件的原始声明，不是统一归一化结果。其他文件的单位、坐标轴及与场景缩放的关系未单独核实；应保留调用方既有配置。

## 来源、许可与校验

输入来自 [WanPhys 的 cc12e3a5 基线](https://github.com/WanPhysTeam/WanPhys/tree/cc12e3a5/wanphys/assets) 中的 `wanphys/assets/`。曾在本仓库的 `example_assets/` 包中保存，本次只改变包边界和路径；保留 Windows 工作树的原始字节，不格式化模型文件。

上游权利人和资产再分发许可尚未逐项核实；本包不授予统一许可证，物理引擎的代码许可证不能代替第三方模型、纹理或数据的真实许可。公开发布或再分发时必须确认相关权利和署名要求；不把来源未知改写为 Apache-2.0。

- `bunny.usd` 的历史来源路径与提交号见 `asset_metadata/example_assets.json`；此记录不证明当前字节与记录版本完全相同，也不授予再分发许可。

当前 `inventory.json` 列出本包每个输入的实际大小与 SHA-256。历史清单单独保存在 `asset_metadata/example_assets.json`；它不能替代当前核验，也不是本包运行依赖。

## 已知问题

bunny.usda 在第 9 行附近存在既有 OpenUSD 解析错误；bunny.usd 可解析，但两者不能擅自互换或覆盖。
