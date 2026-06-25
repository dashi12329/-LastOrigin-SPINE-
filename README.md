# Unity AssetBundle → Spine 3.8 转换工具

将 Unity 2D 骨骼动画 AssetBundle 转换为 [Spine](http://zh.esotericsoftware.com/) 3.8 格式（`skeleton.json` + `skeleton.atlas`），支持 SkinnedMeshRenderer 和 SpriteRenderer，同时提供 GUI 工具和 GIF 导出，本工具目前还是半成品，并且是由AI和我朋友的代码组成，还有不足的地方还希望各位能够帮忙进行完善和提交BUG。

## 功能

- **AssetBundle → Spine**：读取 Unity AssetBundle，自动提取骨骼、网格、精灵、动画曲线
- **GUI 工具**：基于 PyQt5 的图形界面，支持拖拽、批量转换、动画预览
- **GIF 导出**：将 AnimationClip 光栅化为 GIF 动画
- **Web 预览**：内置 Flask 服务器，可在浏览器中预览转换结果
- **Spine 3.8.99** 格式输出，可直接导入 Spine Editor

## 安装

```bash
pip install -r requirements.txt
```

依赖：
- `numpy`
- `opencv-python`
- `Pillow`
- `UnityPy`
- `PyQt5`
- `PyOpenGL`

## 使用

### 命令行

```bash
# 基本转换（输出到 spine_editor/ 目录）
python unity_to_spine.py path/to/__data

# 指定输出目录
python unity_to_spine.py path/to/__data --output path/to/output

# 运行时布局格式
python unity_to_spine.py path/to/__data --runtime

# 同时导出 GIF 动画
python unity_to_spine.py path/to/__data --gif

# 仅导出 GIF（指定宽度）
python unity_to_spine.py path/to/__data --gif-only --gif-width 720
```

### GUI 工具

```bash
python gui_converter.py
```

打开后拖拽 AssetBundle 文件到窗口即可自动转换并预览动画。

### Web 预览

```bash
python viewer_server.py path/to/spine_editor
```

浏览器访问 `http://localhost:5000` 查看 Spine 骨骼动画预览。

## 环境变量

| 变量 | 默认值 | 说明 |
|------|--------|------|
| `SPINE_FPS` | 30 | 动画采样帧率 |
| `SPINE_TARGET_W` | 1600 | 画布目标宽度 |
| `GIF_W` | 720 | GIF 输出宽度 |
| `GIF_FPS` | 24 | GIF 帧率 |
| `GIF_BG` | `ffffff` | GIF 背景色 |
| `GIF_WORKERS` | 0 | GIF 渲染线程数（0=自动） |

## 输出结构

```
spine_editor/
├── skeleton.json      # Spine 骨骼数据
├── skeleton.atlas     # 图集配置
└── images/            # 纹理图片
```

## 许可

MIT License
