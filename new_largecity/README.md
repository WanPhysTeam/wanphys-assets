# 低多边形城市网格

城市洪水示例使用的组合 OBJ 网格、MTL 和调色板贴图。顶层 `new_largecity/` 是一个独立下载包。

## 入口与依赖

- `LowPoly_City_01Ready.obj`
- `LowPoly_City_01Ready.mtl`
- `textures/palette.jpg`

使用 `wanphys.utils.download_asset("new_largecity")` 获取本包目录，再拼接上面所需的文件名。MTL 通过 `map_Kd textures/palette.jpg` 引用调色板，三者必须同包。

不包含仓库中的 `new_largecity.zip` 压缩副本。

## 坐标与尺度

OBJ 以场景米制坐标写出。调用方（`fluid_grid_sparse_liquid_city`）负责缩放到网格域；本包不声明统一 `up_axis` 或 `metersPerUnit`。

## 来源、许可与校验

输入来自 [WanPhys 的 70073a41](https://github.com/WanPhysTeam/WanPhys) 中的 `wanphys/assets/new_largecity/`，曾随城市洪水示例以 Git LFS 保存在代码仓库。本次只改变包边界；保留 Windows 工作树的原始字节。

上游权利人和资产再分发许可尚未逐项核实；本包不授予统一许可证。不把来源未知改写为 Apache-2.0。

当前 `inventory.json` 列出本包每个输入的实际大小与 SHA-256。
