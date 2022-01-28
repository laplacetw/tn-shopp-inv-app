![](https://img.shields.io/github/license/laplacetw/tn-shopp-inv-app)
# 台南購物節發票登錄小幫手

2022-01-27<br>
據[PTT台南鄉民](https://www.ptt.cc/bbs/Tainan/M.1632065603.A.4B8.html)表示，19年以前是有APP可以直接掃QR Code的，不過後來沒有了。<!--more-->雖然許多人都有使用手機載具，難免還是有拿電子發票證明聯的時候，而輸入發票的頁面操作真的相當不便，選完年份選月份、選完月份選日期...。儘管活動已接近尾聲，不過都舉辦好幾年了，沒意外應該會繼續舉辦下去吧？因此就嘗試做了小工具來進行自動掃描與登錄。

## 使用說明
1. 在<span style="color:red;">電腦</span>瀏覽器登入[台南購物節官網](https://tainanshopping.tw/news)，按下F12叫出開發人員工具、點選視窗上方的Console頁籤，輸入下方程式碼取得並複製token。
<br>＊<span style="color:red;">請妥善保管自己的token</span>，即便它的有效性是短暫的。
<br>＊Mac使用者如何叫出瀏覽器開發人員工具？按下「command + option + i」。
<br>＊我不確定token的有效時間，可能僅有數小時，因此開始登錄發票前都應該取得新的token。
```js
const arr = document.getElementsByTagName('script');Object.keys(arr).forEach(key => {if(arr[key].text.includes('window.__NUXT__')) console.log(arr[key].text.match(/(token:").*(?=",email)/)[0].split('"')[1]);});
```

2. 打開[小幫手](https://laplacetw.github.io/proj/tainanshopping/)，點選「開始掃描」，請允許小幫手使用相機。

3. 掃描成功會顯示發票號碼、購買日期等相關資訊，將步驟一所複製的token填入視窗最上方的「Token」欄位。
<br>＊token只需要填入一次。

4. 確認發票資訊<span style="color:red;">正確無誤</span>後點選送出。

## 財政部-電子發票二維碼規格
[https://www.einvoice.nat.gov.tw/home/DownLoad?fileName=1378690240719_0.pdf](https://www.einvoice.nat.gov.tw/home/DownLoad?fileName=1378690240719_0.pdf)

### 左方二維條碼記載事項:
1. 發票字軌 (10 位):記錄發票完整十碼號碼。
2. 發票開立日期 (7 位):記錄發票三碼民國年、二碼月份、二碼日期。
3. 隨機碼 (4 位):記錄發票上隨機碼四碼。
4. 銷售額 (8 位):記錄發票上未稅之金額總計八碼，將金額轉換以十六進位方式記載。若營業人銷售系統無法順利將稅項分離計算，則以00000000 記載。
5. 總計額 (8 位):記錄發票上含稅總金額總計八碼，將金額轉換以十六進位方式記載。
6. 買方統一編號 (8 位):記錄發票上買受人統一編號，若買受人為一般消費者則以 00000000 記載。
7. 賣方統一編號 (8 位):記錄發票上賣方統一編號。
8. 加密驗證資訊 (24 位):將發票字軌十碼及隨機碼四碼以字串方式合併後使用 AES 加密並採用 Base64 編碼轉換。
- 以上欄位總計 77 碼。下述資訊為接續以上資訊繼續延伸記錄，且每個欄位前皆以間隔符號":"(冒號)區隔各記載事項，若左方二維條碼不敷記載， 則繼續記載於右方二維條碼。

## About QR Code Scanner
Power by [vue-qrcode-reader](https://github.com/gruhn/vue-qrcode-reader)