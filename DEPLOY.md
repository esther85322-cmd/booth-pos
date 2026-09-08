# 部署筆記

網站網址：https://farmers-market-pos.web.app
Firebase 專案：farmers-market-pos

## 之後要改程式碼、重新上線

1. 編輯 `index.html`
2. 在這個資料夾執行：
   ```bash
   firebase deploy --only hosting --project farmers-market-pos
   ```

## 如果要改資料庫安全規則

編輯 `firestore.rules`，然後執行：
```bash
firebase deploy --only firestore:rules --project farmers-market-pos
```

## 帳號密碼登入的運作方式

每個攤位代碼會對應一個 Firebase Authentication 帳號（信箱格式是
`<攤位代碼>@booths.boothpos.local`，密碼就是註冊時設定的密碼）。
`firestore.rules` 只允許登入成功、且帳號信箱對得上該攤位代碼的人讀寫
`booths/<攤位代碼>` 這份文件，其他人（包含知道代碼但沒有密碼的人）
完全無法讀取或修改。

`booths_index/list` 這份文件只存攤位代碼與名稱（給登入畫面顯示清單用），
任何人都可以讀取，但只有登入過的攤位帳號可以寫入。

## 管理 Firebase 專案

- 主控台：https://console.firebase.google.com/project/farmers-market-pos
- 「Authentication」分頁可以看到所有已註冊的攤位帳號（信箱前面是攤位代碼）
- 「Firestore Database」分頁可以直接看/改資料，但不建議手動改，容易破壞格式
