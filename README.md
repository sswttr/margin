# Margin

记录股票买卖、持仓盈亏和本人 / 对方分成的网页应用。纯静态页面，部署在 GitHub Pages 上，数据保存在同一个仓库的 `data.json` 里。

## 一、部署

1. 在 GitHub 新建一个**公开**仓库，例如 `margin`。
2. 把这些文件上传到仓库根目录：
   - `index.html`
   - `data.json`（你现在的数据）
   - `manifest.webmanifest`
   - `icon-180.png`
   - `icon-512.png`
   - `README.md`
3. 打开仓库的 Settings → Pages，Source 选 `Deploy from a branch`，分支选 `main`，目录选 `/ (root)`，保存。
4. 一两分钟后访问 `https://你的用户名.github.io/margin/`，就能直接看到你的数据。

## 二、让手机能修改并保存（每台设备做一次）

不填令牌也能打开查看。要在某台设备上登记、删除记录，并保存回 GitHub，需要一个只管这个仓库的访问令牌。

1. 打开 GitHub → 右上角头像 → Settings → Developer settings → Personal access tokens → **Fine-grained tokens** → Generate new token。
2. Token name 随便填，例如 `margin`；Expiration 选你能接受的最长期限。
3. Repository access 选 **Only select repositories**，只勾选 `margin` 这个仓库。
4. Permissions → Repository permissions → **Contents** 选 **Read and write**，其他保持默认。
5. 点 Generate token，复制以 `github_pat_` 开头的令牌。
6. 在 Margin 里点右上角齿轮 → 云端同步 → 访问令牌，粘贴后点「连接并同步」。

状态显示「已同步」就完成了。之后每次登记、删除或修改设置，1 秒左右就会自动保存到仓库的 `data.json`。在 GitHub 上能看到每一次提交，记错了可以从历史版本找回。

令牌只保存在这台设备的浏览器里。手机丢了或不想用了，可以在 GitHub 的令牌页面直接删除它。令牌过期后，同步状态会显示失败，重新生成一个粘贴进去即可。

## 三、说明

- **谁能看到数据**：仓库和网址是公开的，任何拿到网址的人都能看到记录，但只有填了令牌的设备能修改。
- **多设备**：填了令牌的设备每次打开都会直接从 GitHub 读取最新数据。没填令牌的设备读取的是网站上的 `data.json`，GitHub Pages 更新通常需要 1 分钟左右。
- **没填令牌时的修改**：只保存在那台设备上，页面顶部会有橙色提示；填上令牌后会自动合并、上传。
- **行情**：现价来自腾讯财经公开行情。交易时段（工作日 9:15–11:30、13:00–15:00）每秒刷新，其余时间每 30 秒刷新，可能有延迟。股票代码按名称自动匹配，可以在设置 → 行情代码里手动修正。
- **手续费**：买入默认按成交额万分之一，卖出默认万分之六（佣金万一加印花税万五），可以手动修改。
- **成本**：持仓成本按移动加权平均计算，包含手续费。
