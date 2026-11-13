# 明宫三维 · Ming Palace 3D

**在浏览器里自由环视一座明代宫殿。**  
重檐庑殿顶、三层汉白玉台基，以及面阔十一间的红柱与金钉朱门，全部由 JavaScript 在运行时生成。

[在线体验](https://norwinyu.github.io/deepseek-flash-1017-ming-palace/) · [GitHub 仓库](https://github.com/NorwinYu/deepseek-flash-1017-ming-palace)

![太和殿 3D 预览](preview.png)

## 概览

以紫禁城太和殿为灵感，这个单文件 3D 场景将屋面、台基、栏杆、门窗、斗拱和庭院全部程序化生成，再用原生 WebGL2 渲染。无外部模型、贴图或第三方库。

拖动鼠标即可环视建筑，滚轮缩放，双击复位；移动端支持单指旋转与双指缩放。

> A dependency-free WebGL2 study of Ming imperial architecture. Everything is generated at runtime and rendered with custom shaders. No external models, textures, or libraries.

这是对明代官式建筑的风格化演绎，并非测绘级或考古级复原。

## 生成说明

本项目源自一次模型代码生成实验。

- **模型**：DeepSeek Flash 1017
- **输入**：一条中文提示词
- **产物**：单文件 `index.html`，包含场景、交互与渲染代码

<details>
<summary>查看原始提示词</summary>

> 用html和js做一个3D的宫殿，中国明朝建筑风格，可以用鼠标拖动来看这个宫殿不同的侧面。独立完成，不参考其他文件和网络资料

</details>

## 亮点

- **重檐庑殿顶**：双层曲面屋顶、瓦垄、正脊、垂脊与脊兽
- **三层汉白玉台基**：栏板望柱、丹陛石与三层御路台阶
- **面阔十一间**：红柱、五座金钉朱门、格扇窗、额枋与斗拱
- **细部**：蓝底金字“太和殿”匾额、宫灯、铜鼎、庭院宫墙
- **实时渲染**：平行光阴影、天空渐变、雾化与抗锯齿
- **完全自包含**：无外部请求、无统计脚本、无需构建

## 交互

| 操作 | 效果 |
| --- | --- |
| 鼠标拖动 / 单指拖动 | 360° 环视宫殿侧面 |
| 滚轮 / 双指捏合 | 拉近、拉远 |
| 双击 | 复位初始视角 |
| 右侧“正面 / 侧观 / 背面 / 俯瞰” | 切换预设视角 |
| “巡游”按钮 | 开启或暂停自动环绕 |
| 键盘方向键 | 旋转与俯仰 |
| 空格 | 暂停 / 继续巡游 |
| `R` | 复位 |

## 实现

| 维度 | 实现 |
| --- | --- |
| 渲染 | 原生 WebGL2 + GLSL ES 3.0 |
| 几何 | JavaScript 程序化生成 |
| 阴影 | 静态深度贴图 + PCF 软阴影 |
| 匾额 | Canvas 2D 生成纹理 |
| 依赖 | 无 |
| 构建步骤 | 无 |

主场景以一次大网格绘制完成，阴影贴图只烘焙一次。相机使用带阻尼的球面轨道控制；设备像素比上限为 2，以兼顾清晰度与移动端性能。

可通过查询参数快速进入指定视角：

```text
?view=front | side | back | aerial
?still=1
```

`?still=1` 会关闭自动巡游，适合截图或录制。

## 本地运行

无需安装依赖，启动任意静态文件服务器即可：

```bash
python3 -m http.server 8000
```

然后打开 <http://localhost:8000>。

## 部署

纯静态站点，无构建流程，已部署在 GitHub Pages。Fork 后在仓库的 **Settings → Pages** 中选择 `main` 分支和 `/ (root)` 目录即可。

## 项目结构

```text
.
├── index.html      # 单文件 3D 场景（HTML / CSS / JS）
├── preview.png     # 场景预览图
├── favicon.svg     # 站点图标
├── README.md
├── .nojekyll       # GitHub Pages：跳过 Jekyll
└── .gitignore
```

## 浏览器支持

需要支持 WebGL2 的现代浏览器：Chrome / Edge 90+、Safari 15+、Firefox 90+。不支持时页面会显示错误提示。

## 素材与隐私

页面不加载任何第三方字体、图片、统计脚本或 CDN 资源，运行期间不发起第三方网络请求。`preview.png` 是场景的直接渲染截图，已清除图片元数据。

---

用原生 JavaScript 与 WebGL2 构建。建筑的每一根柱子、每一片瓦垄，都在代码里。
