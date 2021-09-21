# nhkradio2-langs-record
NHKラジオ第２ 語学番組録音（汎用版）

- これはNHKラジオ第２放送の「語学ラジオ番組」を**自動録音**するものです。
- 全ての番組の録音に対応しています。

[NHK おうちで学ぼう！for school / 語学](https://www2.nhk.or.jp/gogaku/index.cgi)  

- ロシア語限定版には [nhkradio2-russian-record](https://github.com/ru-museum/nhkradio2-russian-record) があります。

### NHKラジオ第2 語学番組表

<table>
<tr>
  <th>番組名</th><th>コース分類</th><th>放送曜日</th><th>放送時間</th>
</tr>  
<tr>
  <td>まいにちロシア語</td><td>入門編 応用編</td><td>月〜水 木・金</td><td>8:50-9:05</td>
</tr>
<tr>
  <td>まいにちフランス語</td><td>入門編 応用編</td><td>月〜水 木・金</td><td>7:30-7:45</td>
</tr>
<tr>
  <td>まいにちドイツ語</td><td>入門編 応用編</td><td>月〜水 木・金</td><td>7:00-7:15</td>
</tr>
<tr>
  <td>まいにちイタリア語</td><td>入門編 応用編</td><td>月〜水 木・金</td><td>7:45-8:00</td>
</tr>
<tr>
  <td>まいにちスペイン語</td><td>入門編 応用編</td><td>月〜水 木・金</td><td>7:15-7:30</td>
</tr>
<tr>
  <td>まいにち中国語</td><td></td><td>月〜金</td><td>8:15-8:30</td>
</tr>
<tr>
  <td>ステップアップ中国語</td><td></td><td>月・火</td><td>22:00-22:15</td>
</tr>
<tr>
  <td>小学生の基礎英語</td><td></td><td>月・水・金</td><td>6:35-6:45</td>
</tr>
<tr>
  <td>中学生の基礎英語 レベル1</td><td></td><td>月〜金</td><td>6:00-6:15</td>
</tr>
<tr>
  <td>中学生の基礎英語 レベル2</td><td></td><td>月〜金</td><td>6:15-6:30</td>
</tr>
<tr>
  <td>中高生の基礎英語 in English</td><td></td><td>月〜金</td><td>6:30-6:45</td>
</tr>
<tr>
  <td>ラジオ英会話</td><td></td><td>月〜金</td><td>6:45-7:00</td>
</tr>
<tr>
  <td>ボキャブライダー</td><td></td><td>月〜金</td><td>9:05-9:10</td>
</tr>
<tr>
  <td>エンジョイ・シンプル・イングリッシュ</td><td></td><td>月〜金</td><td>9:10-9:15</td>
</tr>
<tr>
  <td>英会話タイムトライアル</td><td></td><td>月〜金</td><td>8:30-8:40</td>
</tr>
<tr>
  <td>高校生からはじめる「現代英語」</td><td></td><td>木・金</td><td>22:00-22:15</td>
</tr>
<tr>
  <td>遠山顕の英会話楽習</td><td></td><td>月〜水</td><td>10:30-10:45</td>
</tr>
<tr>
  <td>ラジオビジネス英語</td><td></td><td>月〜金</td><td>9:15-9:30</td>
</tr>
<tr>
  <td>ニュースで英語術</td><td></td><td>月〜金</td><td>12:55-13:00</td>
</tr>
<tr>
  <td>まいにちハングル講座</td><td></td><td>月〜金</td><td>8:00-8:15</td>
</tr>
<tr>
  <td>ステップアップ ハングル講座</td><td></td><td>木・金</td><td>10:30-10:45</td>
</tr>
<tr>
  <td>アラビア語講座</td><td></td><td>日</td><td>9:30-10:00</td>
</tr>
<tr>
  <td>ポルトガル語入門</td><td></td><td>土</td><td>18:45-19:00</td>
</tr>
</table>

# 動作環境  
- Linux(Debian: bash 使用)
- ffmpeg のインストールが必要です。

# 録音方法  
1. 作業フォルダ（設定例「NHKラジオ語学講座」）に nhkradio2-langs-record.sh を置き編集します。  

　録音時間（必要あれば）を指定します（参照：録音開始時間の微調整）。
 ```
# 録音時間設定値 ： 15分
REC_TIME="00:15:00" 
 ```

2. nhkradio2-langs-record.sh にアクセス権の実行を許可します。  
 ```
 # chmod 755 nhkradio2-langs-record.sh
 ```
3. 作業フォルダでヘルプを表示させ録音したい**講座ID番号**を確認します。
 ```
 # sh ./nhkradio2-langs-record.sh -h
 ```
 
4. CRON に登録し毎日(月-金)同時刻(8:50)に起動させます。  
\# vi /etc/crontab  
- **CRON への登録は講座毎に必要です。**  

**【設定例】**  
　NHKまいにちロシア語：月-水【入門編】/ 木・金【応用編】8:50-9:05  
- ファイルのオプション引数として講座ID番号を指定します。  
- 入門編及び応用編のある講座で何れかのみを録音したい場合は「曜日指定」で設定します。  
　　
<table>
<tr>
  <td>オプション指定</td><td>-i 0（講座番号）</td>
</tr>  
<tr>
  <td>録音時刻指定</td><td>50 8（8時50分）</td>
</tr>
<tr>
  <td>曜日指定</td><td>1-5（月〜金）<br>入門編のみ：1-3（月〜水）<br>応用編のみ：4,5（木・金）</td>
</tr>
</table>

- **username** は、root 或いは使用するユーザー名です（無いとエラーが出ます）。  
- 作業フォルダを「NHKラジオ語学講座」に設定した場合です。  
　**/your/directory/name/NHKラジオ語学講座/** は**絶対 PATH**で指定します。
 ```
50 8 * * 1-5 username bash /your/directory/name/NHKラジオ語学講座/nhkradio2-langs-record.sh -i 0
 ```
5. CRON を再起動させます。
 ```
 # /etc/init.d/cron restart
 ```
 <br> 
※ スクリプトが起動されると「作業フォルダ」にシステムファイル（languages.csv：番組リスト）が作成されます。
  <br>
  <br>
  
## 録音開始時間の微調整  
- 回線状況や配信（放送時刻）とPCの時計の時刻が正確に合致していない場合など、録音開始時間に**誤差**の生じる場合があります。  
- 当方の PC の内蔵時計では日本標準時との誤差は 0.2 秒でしたが、**36秒**の遅延調整が必要でした。  
　　[情報通信研究機構/日本標準時](https://www.nict.go.jp/JST/JST5.html)

**(A)** 開始時刻を遅らせる場合：録音開始時間調整の　**sleep** の値を変更します（初期値：0）。  
　例：開始時刻を**36秒**遅らせる
```
sleep 36　  
```
**(B)** 開始時刻を早める場合（稀なケース）： CRON で行います（CRON の再起動が必要）。  
　例：録音開始時刻を**20秒**早める：開始時刻を**1分**早め（初期値：50 ⇒ 49）開始時刻まで**40秒** sleep させます。
```
sleep 40

# CRON
49 8 * * 1-5 sleep 40; username bash /your/directory/name/NHKラジオ語学講座/nhkradio2-langs-record.sh -i 0  
```

## 実動作前のテスト  
1. 録音時間を**10秒**程度に設定します。
 ```
# 録音時間設定値 ： 10秒
REC_TIME="00:00:10" 
 ```
2.  CRON の起動時刻を数分後に設定し再起動します。
 ```
# CRON
49 8 * * 1-5 ……（略）
 ```
3. 「作業フォルダ」に講座名のフォルダと講座名の録音ファイルが保存されているかを確認して下さい。

## 録音ファイル  

- 保存された **m4a** は音声データフォーマットであり、iTunes や通常のプレイヤーで視聴出来ます。 

# 注意  
- 配信 URL は時期は不明ですが変更されています。  
旧URL: "https://nhkradioakr2-i.akamaihd.net/hls/live/511929/1-r2/1-r2-01.m3u8"  
新URL: "https://radio-stream.nhk.jp/hls/live/2023501/nhkradiruakr2/master.m3u8"
- **録音データは著作権上私的利用のみに限定されていますのでご注意下さい。**


