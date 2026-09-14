# Geometry samples

`mesh_to_points_input.obj` 原样迁自 WanPhys `cc12e3a5` 的
`wanphys/_src/geometry/assets/mesh_to_points_input.obj`。保留 Windows 工作区字节；
坐标单位、上轴和更早的资产作者/许可尚未确认，公开分发前须补充核验。
这是历史网格输入样例，当前没有 WanPhys 默认运行调用方。不是新的物理算法。

```python
from pathlib import Path
from wanphys.utils import download_asset

mesh_path: Path = download_asset("geometry_samples") / "mesh_to_points_input.obj"
```
