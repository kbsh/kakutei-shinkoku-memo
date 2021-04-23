# ESPPとRSUの確定申告

とても参考になったこちらの記事のバックアップです。寄付できるようなので同じく助けになった方はご支援お願いします。
https://blog.puliyo.com/jp/posts/tax-return-espp-rsu/

## 目的
海外企業に勤めていて、ESPPやRSUを受け取ると日本で源泉徴収されないので自分で確定申告をしなければならない。

確定申告をする際ESPPとRSUの申告方法の資料があまり見当たらなかったので前回の申告を自分がどのようにして完了させたか備忘録として記す。

ちなみに、ESPPとRSUの申告に偽りがないこと証明せいといわれたことがある。そのときは[ここ](https://blog.puliyo.com/jp/posts/espp-rsu-evidence/)で紹介している方法で対応した。

## 予備知識
### W-8BEN
他国の納税者であることを証明する書類。

アメリカでESPPやRSUを受け取っていれば、アメリカ側での課税を回避するために必ず申告するべし。

大体はBroker（etrade 等）のユーザー設定のところに申告済みであるかステータスがあるのでそこを確認する。

わからなければヘルプに聞くといい。

### TTM, TTB, TTS
TTM, TTB, TTS　はそれぞれ為替レートのことを指す。

TTSは 円 → 外貨 と流れるときに使用するレート。

TTBは 外貨 → 円 と流れるときに使用するレート。

TTMはTTBとTTSの中間のレート。

[詳細について](https://wise.com/jp/blog/what-is-ttm-tts-ttb)

[みずほのサイト](https://www.mizuhobank.co.jp/market/quote/backnumber/index.html)に日付ごとの履歴があるのでそれを参考にするといい。

### 総合課税, 分離課税
「総合課税」は、さまざまな所得を合算した総所得金額に課税する方法。
所得税率は額によって異なる。[国税庁のサイト](https://www.nta.go.jp/taxes/shiraberu/shinkoku/tebiki/2013/taxanswer/shotoku/2260.htm)に率一覧がある。
住民税率は10%。

「分離課税」は、ほかの所得とは合算しないで別々に課税する方法。
一律課税であり、所得税率15.315%　住民税率5%　なので所得が195万円以下でない限り基本的にはこっちが有利。

### 取得費の平均（総平均法）
株を2回以上にわたって購入・受け取った場合、平均の取得費を算出しなければならない。

結構面倒くさい。

計算例はグーグルにいっぱい転がっているので検索するとたくさんヒットする。

公式にも例がある： https://www.nta.go.jp/taxes/shiraberu/taxanswer/shotoku/1466.htm

## ESPP
### 割引購入日
ESPP を購入した瞬間、安く変えた差額を「給与所得」（総合課税）として申告しなければならない。

次の計算式で算出する：

`(取得時株価 - 割引購入株価) * 株数 * 購入日のTTM`

ESPP オファー期間開始時の時価と購入日の時価いずれか安い株価を割引率分(10%~15%)引いて購入するので、その購入価格とマーケット価格の差額を株数とTTMで掛け算する。

例、

自分は etrade を使っているので、Benefit History 画面で必要な数値を確認

![image](https://user-images.githubusercontent.com/11205591/115802064-2366a800-a419-11eb-99f4-b9baf774add1.png)

上の画像だと下のような式になる：

`(50 - 20) * 258 * 107.80`

### 売却時
売却時は「譲渡所得」（分離課税）として申告しなければならない。

次の計算式で、確定申告の時に必要な値を算出する：

```
譲渡による収入金額 = 株数 * 売却時株価 * 売却日のTTB
取得費（取得価額） = 株数 * 取得時株価 * 取得日のTTS
売買にともなう経費 = 経費 * 支払い日のTTS
```

例、

etrade で Orders を開く

![image](https://user-images.githubusercontent.com/11205591/115802140-45f8c100-a419-11eb-8eff-5db06f18978e.png)

取引の詳細を開く

![image](https://user-images.githubusercontent.com/11205591/115802173-5a3cbe00-a419-11eb-8ca7-ce436f8cf772.png)

売却した株の取得時株価は “View Confirmation of Purchase” で確認する。

“View Confirmation of Purchase” を押したら開いたページの “Purchase Value per Share” を確認する。この数値が取得時株価になる。

上の画像だと下のような式になる：

```
譲渡による収入金額 = 258 * 53 * 108.15
取得費（取得価額） = 258 * 50 * 108.80
売買にともなう経費 = (21 + 1 + 0 + 25) * 110.15
```

### 配当金
配当金は「配当所得」（総合課税または分離課税）として申告しなければならない。

自分の会社は配当金を配布していないので、正確かわからないが、基本的に日本と同じ対処を取ると考えている。

https://www.nta.go.jp/taxes/shiraberu/taxanswer/shotoku/1330.htm

ということで次の計算式で算出する：

`受け取った金額 * 受け取った日のTTM`

留意点:

- もし配当金から税金が差し引かれていたら、外国税額控除を申請することができる
- 配当控除に該当しない

配当控除に該当しないので、所得が195万円以下でない限り分離課税として申告したほうが有利になる。

[参考リンク](https://www.mizuho-sc.com/beginner/useful/zeisei_hayawakari.html)

## RSU
### 権利確定時 (Vested)
権利付与（Grant）ではなく、Vestedになったときに税金が発生する。

受け取った株を「給与所得」（総合課税）として申告しなければならない。

次の計算式で算出する：

`取得時株価(権利確定時の株価) * 株数 * 権利確定時のTTM`

例、

etrade で Benefit History を開き、Restricted Stock まで移動する。

![image](https://user-images.githubusercontent.com/11205591/115802265-89ebc600-a419-11eb-856a-a346619860ee.png)

株が確定した日とその枚数が書かれているが、取得時株価はこの画面には表示されないので、“View Confirmation of Release” を押して株価を確認する。

“View Confirmation of Release” を押したら開いたページの “Market Value Per Share” を確認する。この数値が取得時株価になる。

`“Market Value Per Shareの額” * 10 * 108.52`

### 売却時
売却時は「譲渡所得」（分離課税）として申告しなければならない。

RSU売却時は ESPP売却時と同じ計算式になる。

```
譲渡による収入金額 = 株数 * 売却時株価 * 売却日のTTB
取得費（取得価額） = 株数 * 取得時株価 * 取得日のTTS
売買にともなう経費 = 経費 * 支払い日のTTS
```

例、

etrade で Orders を開きRSUの取引を開く。

![image](https://user-images.githubusercontent.com/11205591/115802333-a7209480-a419-11eb-8b9b-c17754840b12.png)

上の画像だと下のような式になる：

```
譲渡による収入金額 = 1 * 52 * 107.69
取得費（取得価額） = 1 * 47 * 108.45
売買にともなう経費 = (15.01 + 0.01 + 0 + 25) * 109.69
```

### 配当金
配当金は「配当所得」（総合課税または分離課税）として申告しなければならない。

RSU配当金は ESPP配当金と同じ内容になる。

## 確定申告書記入例
https://www.nta.go.jp/taxes/shiraberu/shinkoku/kakutei.htm

上記リンクを開き確定申告書をネットで作成する。

![image](https://user-images.githubusercontent.com/11205591/115802378-b7d10a80-a419-11eb-97b2-a486f6776054.png)

![image](https://user-images.githubusercontent.com/11205591/115802455-d9ca8d00-a419-11eb-9700-726ca95425f9.png)

「収入金額・所得金額の入力」ページまで来ると「総合課税の所得」と「分離課税の所得」で入力欄が別れている。

![image](https://user-images.githubusercontent.com/11205591/115802472-e7801280-a419-11eb-92be-d02cd0c35c68.png)

![image](https://user-images.githubusercontent.com/11205591/115802481-eea72080-a419-11eb-8f29-ab1cf6c9905c.png)

自分のその年の収入を適応した所得の種類に入力していく。

下記例：

#### 総合課税の所得 -> 給与所得 -> 年末調整済みの源泉徴収票の入力
- 会社での収入

![image](https://user-images.githubusercontent.com/11205591/115802548-15655700-a41a-11eb-9d27-3bac09662197.png)

#### 総合課税の所得 -> 給与所得 -> 年末調整済みでない源泉徴収票の入力
- ESPP割引購入日
- RSU割引購入日

![image](https://user-images.githubusercontent.com/11205591/115802577-231adc80-a41a-11eb-93fc-7b70ccf60414.png)

① に計算した値を入れる。

② と ③ は 0 でいい。

支払い者は会社の情報を入れる。

![image](https://user-images.githubusercontent.com/11205591/115802603-2c0bae00-a41a-11eb-948d-0574a903c68a.png)

#### 分離課税の所得 -> 株式等の譲渡所得等
- ESPP売却時
- RSU売却時

ページ中央ぐらいまでスクロールすると下記項目があるので、「特定口座（源泉徴収あり・源泉徴収なし）以外で上場株式等の売却がある。」にチェックを入れて入力ボタンをクリック。

![image](https://user-images.githubusercontent.com/11205591/115802643-3cbc2400-a41a-11eb-85e6-134c28705204.png)

「ESPP売却時」と「RSU売却時」の例を記入すると下記のようになる。

![image](https://user-images.githubusercontent.com/11205591/115802667-4b0a4000-a41a-11eb-8896-b21a1b1885d9.png)

「譲渡した株式等の銘柄」にはティッカーシンボルを入れてる。

小数点（端数）は切り捨て、四捨五入、切り上げ、どれでも構わない（と思う）。

今回、複数回に渡って株を購入・受け取っているので、平均取得費を入力している。

下の表は売却した株の"取得"に関する情報をまとめている。

取得日|9/10/2019|10/12/2018
---|---|---
種類|RSU|ESPP
株数|12|258
取得時株価|47|50
取得日TTS|108.45|108.8
取得費 $ (株数 * 株価)|564|12900
取得費 ¥ ($ * TTS)|61165.8|1403520

取得単価は下記になる。

`取得単価 = (61165.8 + 1403520) / (12 + 258) = 5424.762222`

取得単価に売却した株数を掛けて、平均取得費を算出。

```
5424.762222 * ESPP売却株数(258) = 1399588.653
5424.762222 * RSU売却株数(1) = 5424.762222
```

### 配当所得
- ESPP配当金
- RSU配当金

「総合課税の所得 -> 配当所得」
でも
「分離課税の所得 -> 上場株式等に係る配当所得等」
でも
結局同じページに飛ぶのでどちらかを押す。

「配当所得の課税方法の選択」で総合課税または分離課税のどちらかを選ぶ。迷ったら分離課税を選ぶ。

![image](https://user-images.githubusercontent.com/11205591/115802829-94f32600-a41a-11eb-981e-db01f4d80d0e.png)

ページ中央ぐらいまでスクロールすると下記項目があるので入力ボタンをクリック。

![image](https://user-images.githubusercontent.com/11205591/115802838-9ae90700-a41a-11eb-890d-551e516db263.png)

上場株式等の配当の場合は上の「入力する」ボタンをクリック。

上場株式ではない場合下の「入力する」ボタンをクリック。

下の画像は「申告分離課税」を選んでいて、上場株式等の配当の「入力する」ボタンをクリックした時に表示される画面。

![image](https://user-images.githubusercontent.com/11205591/115802868-ab00e680-a41a-11eb-99fc-bdadde6069c8.png)

① には「株式の配当」
② にはティッカーシンボル
③ にはブローカー名
④ には受け取った配当額
あとは 0 を記入

### 分離課税の場合 -> 先物取引に係る雑所得等
- FX

## 他参考リンク
- https://mytips.hatenablog.com/entry/2020/02/17/131845
- https://www.smbcnikko.co.jp/service/tax_sys/other/case01/index.html
- [自分がどのようにして証明したか](https://blog.puliyo.com/jp/posts/espp-rsu-evidence/)


