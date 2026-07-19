# 読書Podcast(自分専用)

Open Notebookで作った本の対話音声を、GitHub経由でApple Podcastsアプリから聞くための非公開Podcast。

1つの番組の中に、本ごとに「シーズン(Season)」を分けて追加していく方式。

## シーズン一覧

| Season | 本のタイトル | エピソード数 | 状態 |
|---|---|---|---|
| 1 | ロバート・キーガン『なぜ私たちは現代社会で「生きづらさ」を抱えているのか』(成人発達理論) | 11話 | 完了 |

新しい本を追加したら、この表に1行足してください。

## 新しい本を追加する手順

1. **音声を作る**
   Open Notebookでいつも通り、本の音声(mp3)を各話ごとに作成する。

2. **ファイルをこのフォルダに置く**
   `my-private-podcast` フォルダの中に、mp3ファイルをそのままコピーする(サブフォルダに分けなくてよい)。ファイル名は前の本と被らないようにする(例: `〇〇No.1.mp3`)。

3. **feed.xmlに項目を追加する**
   `feed.xml` を開き、`</channel>` の直前に、話数の数だけ `<item>` ブロックを追加する。1話分は以下の形。

   ```xml
   <item>
     <title>第1話:章タイトル</title>
     <description>この話の内容を1〜2文で</description>
     <itunes:season>2</itunes:season>
     <itunes:episode>1</itunes:episode>
     <enclosure url="https://raw.githubusercontent.com/lessentielestinvisiblepouryeux-beep/my-private-podcast/main/ファイル名.mp3" length="ファイルサイズ(バイト)" type="audio/mpeg"/>
     <guid>season2-episode01</guid>
     <pubDate>Wed, 01 Jul 2026 00:00:00 GMT</pubDate>
   </item>
   ```

   ポイント:
   - `itunes:season` は本ごとに1つ増やす(2冊目なら2、3冊目なら3)。これでApple Podcastsアプリ内で本ごとにシーズン分けして表示される。
   - `itunes:episode` はその本の中の話数(1から)。
   - `guid` は他のどの話とも重ならない文字列にする(例: `season2-episode01`)。
   - `enclosure` の `url` は、GitHubにファイルをpushした後の raw.githubusercontent.com のURL。ファイル名に日本語が入る場合は自動でURLエンコードされるので、GitHub上のファイルページのURLをコピーすればよい。
   - `length` はmp3ファイルのバイト数(だいたいでよい場合はファイルの「サイズ」を確認)。

4. **GitHubに反映する(コミット&プッシュ)**
   いつも使っている方法(GitHub Desktopやgitコマンド)で、mp3ファイルと更新した`feed.xml`をコミットしてプッシュする。

5. **Apple Podcastsアプリで確認する**
   登録済みの番組を開き、下に引っ張って更新すると、新しいシーズンのエピソードが表示される。

## 番組全体の設定(channelタグ)を変えたいとき

- `<title>`: 番組全体の名前。特定の本の名前ではなく、シリーズ全体を表す名前にしてある。
- `<description>`: 番組全体の説明。新しい本を始めたら、ここに一言追記してもよい(必須ではない)。
- `<itunes:image>`: 番組のカバー画像。`cover.jpg`を差し替えれば全シーズン共通のカバーが変わる。
