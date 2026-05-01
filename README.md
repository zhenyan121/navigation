# 夢の栞

二次元风格的个人导航站，Material Design 3 实现。

## 功能

- 随机动漫背景图（来自 [dmoe.cc](https://www.dmoe.cc)）
- 樱花飘落动画
- Live2D 看板娘
- 导航数据通过 JSON 文件配置，增删链接无需改代码
- 响应式布局

## 技术栈

Vue 3 + Vite，纯 CSS 实现 Material Design 3 风格，无 UI 框架依赖。

## 使用

```bash
npm install
npm run dev      # 开发模式
npm run build    # 构建到 dist/
```

## 自定义导航

编辑 `src/data/links.json`：

```json
[
  {
    "id": "唯一标识",
    "title": "分类名称",
    "links": [
      { "label": "站点名", "url": "https://example.com" }
    ]
  }
]
```

开发模式下 Vite HMR 自动热更新，无需手动刷新。

## 目录结构

```
src/
├── App.vue                       # 根组件
├── main.js                       # 入口
├── data/
│   └── links.json                # 导航数据
├── components/
│   ├── SakuraEffect.vue          # 樱花特效
│   └── CategorySection.vue       # 分类板块
└── assets/
    └── styles/
        └── theme.css             # M3 主题
```

## 许可

MIT
