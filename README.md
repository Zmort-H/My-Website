# ZhangJinHao · 日常与留言

一个简洁的单文件静态网站，使用 GitHub Pages 托管，Supabase 保存公共留言。

## 文件

```text
网站/
├─ index.html        # 页面、样式、脚本、日常内容
├─ assets/
│  ├─ touxiang.jpg   # 日常列表头像
│  ├─ favicon.svg
│  └─ posts/         # 日常图片
├─ .gitignore
└─ README.md
```

## 添加日常

打开 `index.html`，找到：

```js
const POSTS = [
```

在数组最前面添加：

```js
{
  date: "2026-06-01",
  text: "今天发生了一件值得记录的小事。",
  image: "assets/posts/my-photo.jpg",
  location: "上海"
}
```

说明：

- `date` 使用 `YYYY-MM-DD` 格式
- `text` 是正文
- `image` 可以省略
- 图片放进 `assets/posts/`，页面会保持图片原始比例

保存后刷新页面即可看到，提交到 GitHub 后线上会自动更新。

## 更换头像

日常列表头像使用：

```text
assets/touxiang.jpg
```

直接用一张新的正方形图片覆盖这个文件即可。建议尺寸 512 × 512 或更小。

## 留言板

留言板已接入 Supabase：

- 项目名：`zhangjinhai-guestbook`
- 数据表：`public.guestbook`
- 所有访客共享留言
- 只需要填写留言内容，不需要名字
- 已配置只读和新增权限，不允许普通访客修改或删除留言

配置位于 `index.html` 底部：

```js
const SUPABASE_URL = "https://qsfmkzphwelnownngzem.supabase.co";
const SUPABASE_KEY = "你的 anon public key";
```

`anon public key` 是公开前端 key，可以放在网页里。不要把 `service_role` key 放进代码。

数据库密码单独保存在：

```text
C:\Users\ZJH\Desktop\Supabase-ZhangJinHao.txt
```

不要把这个文件上传到 GitHub。

## 本地预览

```bash
cd E:\网站
python -m http.server 8000
```

打开 <http://localhost:8000>。

## 部署到 GitHub Pages

1. 在 GitHub 新建仓库
2. 上传 `index.html`、`assets/`、`.gitignore` 和 `README.md`
3. 进入仓库 `Settings` -> `Pages`
4. Source 选择 `Deploy from a branch`
5. Branch 选择 `main`
6. 目录选择 `/ (root)`
7. 保存并等待部署

部署后留言仍然保存在 Supabase，不会因为更新 GitHub 页面而丢失。