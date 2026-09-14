# 点云样例

小型点云/网格输入样例集合。顶层 `point_cloud_samples/` 是一个独立下载包，输入文件名和字节保持不变。

## 入口与依赖

- `simple_cloud.ply`
- `simple_test_cloud.ply`
- `test_cloud.ply`
- `test_cloud_new.ply`
- `test_mesh.ply`

使用 `wanphys.utils.download_asset("point_cloud_samples")` 获取本包目录，再拼接上面所需的文件名；不需要下载其他模型包。

这五个小型样例作为一个独立样例集合；没有因此引入其他顶层资产包的依赖。

## 坐标与尺度

文件的单位、坐标轴及 up_axis 尚未单独核实；不推断整包采用统一米制或 Z-up，也不改变调用方既有缩放。

## 来源、许可与校验

输入来自 [WanPhys 的 cc12e3a5 基线](https://github.com/WanPhysTeam/WanPhys/tree/cc12e3a5/wanphys/assets) 中的 `wanphys/assets/`。曾在本仓库的 `example_assets/` 包中保存，本次只改变包边界和路径；保留 Windows 工作树的原始字节，不格式化模型文件。

上游权利人和资产再分发许可尚未逐项核实；本包不授予统一许可证，物理引擎的代码许可证不能代替第三方模型、纹理或数据的真实许可。公开发布或再分发时必须确认相关权利和署名要求；不把来源未知改写为 Apache-2.0。

当前 `inventory.json` 列出本包每个输入的实际大小与 SHA-256。历史清单单独保存在 `asset_metadata/example_assets.json`；它不能替代当前核验，也不是本包运行依赖。

## 已知问题

simple_cloud.ply 原本就是空文件（0 bytes），不能把保留该文件或哈希一致视为有效点云验证。
