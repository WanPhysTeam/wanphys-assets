# 水轮场景

水轮 USD 模型。顶层 `watermill/` 是一个独立下载包，输入文件名和字节保持不变。

## 入口与依赖

- `watermill.usdc`

使用 `wanphys.utils.download_asset("watermill")` 获取本包目录，再拼接上面所需的文件名；不需要下载其他模型包。

本包有一项缺失的历史相对依赖，见下方“已知问题”。保持 watermill.usdc 与 textures/ 同属本包，不将纹理移到其他顶层包。

## 坐标与尺度

- `watermill.usdc` 的原始 USD 元数据：`metersPerUnit=1.0`，`upAxis=Z`，`defaultPrim=root`。

以上是文件的原始声明，不是统一归一化结果。其他文件的单位、坐标轴及与场景缩放的关系未单独核实；应保留调用方既有配置。

## 来源、许可与校验

输入来自 [WanPhys 的 cc12e3a5 基线](https://github.com/WanPhysTeam/WanPhys/tree/cc12e3a5/wanphys/assets) 中的 `wanphys/assets/`。曾在本仓库的 `example_assets/` 包中保存，本次只改变包边界和路径；保留 Windows 工作树的原始字节，不格式化模型文件。

上游权利人和资产再分发许可尚未逐项核实；本包不授予统一许可证，物理引擎的代码许可证不能代替第三方模型、纹理或数据的真实许可。公开发布或再分发时必须确认相关权利和署名要求；不把来源未知改写为 Apache-2.0。

当前 `inventory.json` 列出本包每个输入的实际大小与 SHA-256。历史清单单独保存在 `asset_metadata/example_assets.json`；它不能替代当前核验，也不是本包运行依赖。

## 已知问题

watermill.usdc 引用 ./textures/color_0C0C0C.exr，但原资产目录没有该纹理，本次没有补造。将来若补齐，应放入本包 textures/，保持原相对路径。
