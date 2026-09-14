# 历史资产来源记录

原 example_assets.json 历史来源清单。顶层 `asset_metadata/` 是一个独立下载包，输入文件名和字节保持不变。

## 入口与依赖

- `example_assets.json`

使用 `wanphys.utils.download_asset("asset_metadata")` 获取本包目录，再拼接上面所需的文件名；不需要下载其他模型包。

本包只供来源追溯，不是其他模型包的运行时依赖。

## 坐标与尺度

不适用：本包是来源元数据，不包含几何。

## 来源、许可与校验

输入来自 [WanPhys 的 cc12e3a5 基线](https://github.com/WanPhysTeam/WanPhys/tree/cc12e3a5/wanphys/assets) 中的 `wanphys/assets/`。曾在本仓库的 `example_assets/` 包中保存，本次只改变包边界和路径；保留 Windows 工作树的原始字节，不格式化模型文件。

上游权利人和资产再分发许可尚未逐项核实；本包不授予统一许可证，物理引擎的代码许可证不能代替第三方模型、纹理或数据的真实许可。公开发布或再分发时必须确认相关权利和署名要求；不把来源未知改写为 Apache-2.0。

当前 `inventory.json` 列出本包每个输入的实际大小与 SHA-256。历史清单单独保存在 `asset_metadata/example_assets.json`；它不能替代当前核验，也不是本包运行依赖。

## 已知问题

example_assets.json 只记录 6 个文件的历史路径、提交和校验值，其中部分大小/校验值与当前实际输入不一致。它不是当前资产完整性清单，也不是全包许可证明；保留原始字节，不静默更新这些历史值。
