# QR 管理室

無須購買網域、無須 QR 平台訂閱。靜態 PWA，使用 GitHub 專用權杖更新 `links.json`。

## 第一次上線（約 10 分鐘）

1. 登入 GitHub，新增 **Public** 儲存庫，例如 `qr-links`，勾選建立 README。
2. 在儲存庫選 **Add file → Upload files**，上傳本專案內容，保持 `vendor/qrcodegen.js` 的資料夾結構。不要上傳 ZIP 當作網站；應解壓後上傳。`.nojekyll` 也一併上傳。
3. 在 **Settings → Pages → Build and deployment** 選 **Deploy from a branch**，分支選 `main`、資料夾選 `/ (root)`，Save。
4. 等待 Pages 顯示網站網址，如 `https://你的帳號.github.io/qr-links/`。開啟網站，即是管理介面。
5. 到 https://github.com/settings/personal-access-tokens/new 建立 Fine-grained token：Resource owner 選自己；Repository access 選 **Only select repositories**，僅勾選 `qr-links`；Repository permissions 的 **Contents → Read and write**。不需要給 Workflows 權限。設定適當效期並複製權杖。
6. 在 PWA 輸入帳號、儲存庫、分支及剛才的 Pages 網址，貼入權杖，按「連線並讀取清單」。
7. 批次建立 50 組，按「發布全部變更」。看到發布完成後，即可列印 QR。網址尚未指定時會顯示「內容準備中」。

Chrome／Edge 可使用安裝功能加入桌面；iPhone Safari 使用分享 → 加入主畫面。權杖只在目前視窗記憶體中，網站不會自行保存；可使用 Chrome 密碼管理員儲存與自動填入。若沒有提示儲存，可在 Chrome 密碼管理員手動新增網站 https://labaraylin.github.io 、使用者名稱為 GitHub 帳號、密碼為專用權杖。權杖到期或更換後也需更新已儲存的密碼；不要把權杖傳給別人或寫進檔案。

## 日常使用

開啟 PWA → 輸入權杖 → 連線讀取 → 修改網址 → 發布。可以批次修改後一次發布。停用不會刪除編號，已印出的 QR 會顯示停用提示；再次啟用可恢復。

「QR」可下載單張 SVG；「下載全部 SVG ZIP」一次下載所有圖片。批次使用「列印全部 QR」，可印出或另存 PDF。JSON 備份包含編號、名稱、目的網址與啟用狀態，不包含權杖。匯入只更新草稿，需要再按發布。

連線讀取會取代草稿，所以若有未發布資料，先下載備份。換裝置時先讀取 GitHub；發生版本衝突時先備份，再重新讀取並合併，避免覆蓋他人修改。

## 本機預覽

在專案資料夾執行 `node serve.cjs`，開啟 http://localhost:4173 。本機預覽時，Pages 網址仍要填最終上線網址，QR 才能供外部手機掃描。

## 限制與隱私

- GitHub 免費 Pages 使用公開儲存庫。清單、名稱、目的網址與歷史版本都是公開資訊，勿填入密碼或私人資訊。
- QR 編碼的是 Pages 的 `go.html?id=001`，發布網址確定後再印。不要改帳號、儲存庫名稱、QR 編號或網站路徑。
- 網址更新需要 Pages 完成部署。本介面最多等待約兩分鐘確認清單版本；超時仍可能稍後部署成功。
- 掃描需要網路。掃描頁與網址清單不使用離線快取；離線時顯示錯誤，避免開啟舊目的網址。
- 草稿、帳號與儲存庫設定會存於本機瀏覽器；權杖不會寫入 localStorage、備份、程式碼或 QR。
- 此版無掃描統計、無多使用者權限管理。離線可編輯草稿，發布需要網路。
- GitHub Pages 有使用政策與服務限制，不提供永久可用保證；不適合拿來經營商用 SaaS／交易網站。參閱 https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits 。

QR 產生器由 Project Nayuki 提供（MIT），授權文字保留於 `vendor/qrcodegen.js`，所有 QR 圖片均在本機產生。
