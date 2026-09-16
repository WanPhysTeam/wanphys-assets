# 天空盒贴图

流体示例使用的环境立方体贴图 JPEG。顶层 `skybox/` 是一个独立下载包。

## 入口与依赖

- `clear_sky.jpg`（城市洪水默认天空）
- `cloudy_sky.jpg`
- `sky2.jpg`

使用 `wanphys.utils.download_asset("skybox")` 获取本包目录。调用方按文件名选择贴图。

## 坐标与尺度

2D 图像，无场景坐标。

## 来源、许可与校验

输入来自 [WanPhys 的 70073a41](https://github.com/WanPhysTeam/WanPhys) 中的 `wanphys/assets/skybox/`。保留 Windows 工作树的原始字节。

上游权利人和资产再分发许可尚未逐项核实；本包不授予统一许可证。不把来源未知改写为 Apache-2.0。

当前 `inventory.json` 列出本包每个输入的实际大小与 SHA-256。
