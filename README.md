# Muse 邀请码互助社区

网址（部署后）：https://pip799439-tech.github.io/muse-invite/

站长邀请码 `4U157W` 固定在队列第 1 位。

## 文件

- `index.html` — 全部页面（样式、逻辑都在这一个文件里，无需其他依赖）

## 部署步骤（GitHub Pages）

1. 登录 GitHub，新建公开仓库 `muse-invite`（不要勾选 Add README，避免冲突也可以勾选，后续覆盖）。
2. 在仓库页点 **Add file → Upload files**，把 `index.html` 上传到根目录，提交（Commit changes）。
3. 进仓库 **Settings → Pages**：
   - Source 选 **Deploy from a branch**
   - Branch 选 **main**，目录选 **/ (root)**，保存。
4. 等 1–3 分钟，Pages 设置页顶部会出现网址：`https://pip799439-tech.github.io/muse-invite/`
5. 打开网址测试：复制按钮、确认轮换、刷新后进度保留、手机端显示。

## 如何添加更多真实邀请码

编辑 `index.html`，找到脚本顶部的 `INVITE_CODES` 数组，在 `4U157W` 后面按顺序追加：

```js
var INVITE_CODES = [
  "4U157W",
  "AB12CD",
  "XY34ZW"
];
```

- 每个邀请码必须是六位大写字母或数字。
- 第一个永远是 `4U157W`，不要改动它的位置。
- 只填真实有效的邀请码，不要随机编造。

## 当前版本的边界（静态版）

- 轮换队列是随页面发布的预置队列，对所有访客一致；每位访客的“已使用进度”保存在各自浏览器本地（localStorage），互不影响。
- 提交功能在静态版仅保存在提交者本机浏览器，并明确标注“待审核（本机记录）”，**不会**同步给其他访客。
- “我已使用此邀请码”是访客自我确认，不代表 Muse 官方验证或兑换成功。

## 如需真正的多人共享与管理员审核（第二阶段）

GitHub Pages 只能托管静态文件，无法独立完成跨用户数据同步和安全管理员登录。第二阶段可接免费后端（任选其一，均有免费额度）：

- **Supabase**（免费档）：用它的数据库存邀请码队列与提交记录，用 Auth 做管理员登录，网页通过官方 JS 库读写。管理员在后台批准/拒绝/删除/排序，访客端实时读取已批准队列。
- **Firebase**（免费 Spark 档）：Firestore + Authentication，模式与上面相同。

接入后端后需要：数据库表（codes: code、position、status、created_at；usage_logs: code、visitor_id、created_at）、行级安全策略（普通访客只能读已批准队列、只能新增提交；只有管理员账号能改状态/顺序），管理页用管理员登录后才显示。这些都不能把管理密码写进公开前端代码。
