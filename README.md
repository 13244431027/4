# 静态资源展示页开发文档

## 1. 项目概述
基于 GitHub Pages 的静态资源展示系统。通过 `信息.json` 驱动内容，支持搜索、分页及动态链接显示。

## 2. 目录结构
```text
├── .github/workflows/deploy.yml  # 自动部署配置
├── index.html                    # 主页面
├── 信息.json                     # 数据源
└── 封面/                         # 图片资源
    └── {id}.png                  # 命名规则：ID.png
```

## 3. 数据规范 (`信息.json`)
UTF-8 编码。字段说明如下：

| 字段 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| `id` | String | ✅ | 唯一标识，对应封面文件名 |
| `name` | String | ✅ | 项目名称 |
| `desc` | String | ✅ | 简介 |
| `authors` | Array | ✅ | 作者列表 `[{name, url}]` |
| `tags` | Array | ✅ | 标签列表 `[]` |
| `fileUrl` | String | ✅ | 文件下载链接 |
| `docUrl` | String | ❌ | 文档链接 1 (空则隐藏) |
| `docUrl2` | String | ❌ | 文档链接 2 (空则隐藏) |
| `exampleUrl`| String | ❌ | 示例链接 (空则隐藏) |
| `uploadTime`| String | ✅ | 上传时间 |

**示例：**
```json
{
  "id": "1001",
  "name": "示例项目",
  "desc": "项目描述",
  "authors": [{"name": "作者", "url": "https://..."}],
  "tags": ["标签"],
  "fileUrl": "https://...",
  "docUrl": "", 
  "docUrl2": "",
  "exampleUrl": "",
  "uploadTime": "2023-10-01"
}
```

## 4. 功能说明
1.  **分页渲染**：每页 20 条，自动计算分页。
2.  **实时搜索**：支持搜索名称、介绍、标签、作者。
3.  **动态按钮**：链接字段为空时，对应按钮自动隐藏。
4.  **图片容错**：封面缺失时自动隐藏图片区域。

## 5. 维护与故障排除
### 5.1 新增资源
1.  上传封面至 `封面/` 文件夹，命名为 `{id}.png`。
2.  在 `信息.json` 中添加对应对象。
3.  提交推送，触发自动部署。
