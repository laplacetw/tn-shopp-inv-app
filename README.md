![](https://img.shields.io/github/license/laplacetw/tn-shopp-inv-app)
# 台南購物節發票登錄APP

2022-01-27<br>
儘管此活動已舉辦多年，但我是去年聽朋友說才知道(￣▽￣)~* 而即使手機載具已經很普及，難免還是有拿電子發票證明聯的時候...且我發現長輩還是習慣索取紙本發票囧rz。<!--more-->據[PTT台南鄉民](https://www.ptt.cc/bbs/Tainan/M.1632065603.A.4B8.html)表示，19年以前是有APP可以直接掃QR Code的，不過後來沒有了。而輸入發票的頁面操作真的會令人煩躁，選完年份選月份、選完月份選日期...全部手動輸入可能好一些。還好現在很難拿到沒有QR Code的紙本發票了，雖然活動已接近尾聲，不過沒意外應該會繼續舉辦下去吧？看著手邊那疊發票，因此就寫了小工具來進行自動掃描與登錄。

### 使用說明
1. 
   - <span style="color:red;">請妥善保管自己的token</span>，即便它的有效性是短暫的。
   - 每回開始登錄發票前建議重新取得token，失效的token將導致登錄失敗。
   - 手機上操作：登入[台南購物節官網](https://tainanshopping.tw/news)後，打開瀏覽器的瀏覽記錄，找到網址為「tainanshopping.tw / oauth...」的瀏覽紀錄，複製該筆瀏覽紀錄的網址。為方便擷取需要的部分，將剛剛複製的網址貼到手機內建的備忘錄或Line Keep，然後將「token=」等號後面的整串文字(token)複製起來。<br><br>
      ![](https://i.imgur.com/um0AuNU.png)
   - 電腦上操作：登入[台南購物節官網](https://tainanshopping.tw/news)後，<span style="color:red;">重新整理頁面</span>，按下F12叫出開發人員工具、點選視窗上方的Console頁籤，輸入下方程式碼並將輸出的整串文字(token)複製起來。
      ```js
      const arr = document.getElementsByTagName('script');Object.keys(arr).forEach(key => {if(arr[key].text.includes('window.__NUXT__')) console.log(arr[key].text.match(/(token:").*(?=",email)/)[0].split('"')[1]);});
      ```
      - Mac使用者如何叫出瀏覽器開發人員工具？按下「command + option + i」。<br><br>
      ![](https://i.imgur.com/8Zz4K9F.png)
      ![](https://i.imgur.com/uxBe9GH.png)
   <br><br>

2. 免安裝，用瀏覽器打開[APP](https://laplacetw.github.io/proj/tainanshopping/)，點選「開始掃描」，請允許APP使用相機。

3. 掃描成功會顯示發票號碼、購買日期等相關資訊，將步驟一所複製的token填入視窗最上方的「Token」欄位。
   - token只需要填入一次。

![](https://i.imgur.com/oQSjCMO.jpg)

4. 確認發票資訊<span style="color:red;">正確無誤</span>後點選送出，登錄成功與否都會有提示訊息，請等待官網伺服器回應。
   - 有可能會讀取到右邊的QR Code，但那不是我們需要的資訊，如要避免請於掃描時遮蔽該QR Code。

### 免責聲明
此應用程式僅為方便快速登錄發票而製作的<span style="color:red;">非官方</span>APP，無私分享供他人使用，不對任何錯誤或遺漏承擔責任。建議您可以嘗試透過APP登錄一張發票，並前往官網確認有無登錄成功，再決定是否繼續使用。

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