![](https://img.shields.io/github/license/laplacetw/tn-shopp-inv-app)
# 台南購物節發票登錄小幫手

2022-01-27<br>
據[PTT台南鄉民](https://www.ptt.cc/bbs/Tainan/M.1632065603.A.4B8.html)表示，19年以前是有APP可以直接掃QR Code的，不過後來沒有了。<!--more-->雖然許多人都有使用手機載具，難免還是有拿電子發票證明聯的時候，而輸入發票的頁面操作真的相當不便，特別是輸入賣方統編的部分。儘管活動已接近尾聲，不過都舉辦好幾年了，沒意外應該會繼續舉辦下去吧？因此就嘗試做了小工具來進行自動掃描與登錄。

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

## About QR Code Scanner
Power by [vue-qrcode-reader](https://github.com/gruhn/vue-qrcode-reader)