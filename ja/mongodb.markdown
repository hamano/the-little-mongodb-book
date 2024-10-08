---
title: MongoDBの薄い本
subtitle: The Little MongoDB Book
author: Karl Seguin
translator: HAMANO Tsukasa
authors: Karl Seguin 著 / 濱野　司 訳
keywords: MongoDB 薄い本 チュートリアル
version: 2.6.0
stylesheet: stylesheet.css
---

\frontmatter
\tableofcontents

# この本について # {-}

## ライセンス ## {-}
MongoDBの薄い本はAttribution-NonCommercial 3.0 Unportedに基づいてライセンスされています。***あなたはこの本を読む為にお金を支払う必要はありません。***

この本を複製、改変、展示することは基本的に自由です。しかし、この本は常に私(カール・セガン)に帰属するように求めます。そして私はこれを商用目的で使用する事はありません。
以下にライセンスの全文があります:

<http://creativecommons.org/licenses/by-nc/3.0/legalcode>

## 著者について ## {-}
カール・セガンは幅広い経験と技術を持った開発者です。 彼は.Netのエキスパートであると同時にRubyの開発者です。彼はOSSプロジェクトのセミアクティブな貢献者であり、テクニカルライターや時々講演を行っています。MongoDBに関して、彼はC#のMongoDBライブラリNoRMの主要な貢献者であり、インタラクティブ・チュートリアル[mongly](http://openmymind.net/mongly/)や[Mongo Web Admin](https://github.com/karlseguin/Mongo-Web-Admin)を書きました。彼のカジュアルなゲーム開発者の為のサービス、[mogade.com](http://mogade.com/)はMongoDBで稼動しています。

カールは過去に[Redisの薄い本](http://openmymind.net/2012/1/23/The-Little-Redis-Book/)も書いています。

彼のブログは <http://openmymind.net> 、つぶやきは[\@karlseguin](http://twitter.com/karlseguin)で見つかります。

## 謝辞 ## {-}
[Perry Neal](http://twitter.com/perryneal)が私に彼の目と意見と情熱を貸してくれたことに感謝します。ありがとう。

## 最新バージョン ## {-}
この本はMongoDB 2.6に対応するようAsya Kamskyによって更新されました。

原書の最新のソースはこちら:

<http://github.com/karlseguin/the-little-mongodb-book>

## 訳者より ## {-}
内容の誤りや誤訳などありましたら[\@hamano](http://twitter.com/hamano)まで連絡下さい。翻訳を手伝ってくれた[\@tamura__246](http://twitter.com/tamura__246)さんと誤字、誤訳を指摘下さった[matsubo](https://github.com/matsubo)さん、[honda0510](https://github.com/honda0510)さん、[\@ponta_](https://twitter.com/ponta_)さん、[ttaka](https://github.com/ttaka)さんに感謝します。

翻訳版のソース:
<http://github.com/hamano/the-little-mongodb-book>

\mainmatter

# 序章 # {-}
 > この章が短いことは私の誤りではありません、MongoDBを学ぶ事はとても簡単です。

技術は激しい速度で進歩しているとよく言われます。それは新しい技術と技術手法が公開され続けているという点で真実ですが、私の見解ではプログラマによって利用される基礎的な技術の進歩は非常に遅いと考えています。何年もかけて習得した技術には少なからず基礎技術と関連があります。注目すべき点は確立した技術が置きかえられる速度です。長い歴史を持つ技術に対する開発者の関心はあっという間に移り変わる恐れがあります。

既に確立されているリレーショナルデータベースに対して発展してきたNoSQLはこの様な急転換の典型的な事例です。いつの日か、RDBMSで運用されるWebは少なくなり、NoSQLが実用に足るソリューションとして確立されるかもしれません。

たとえこれらの技術が一晩で移り変わったとしても、実際的な実務でこれらが受け入れられるには何年もかかります。初期の段階では比較的小規模な会社や開発者の情熱によって突き動かされます。新しい技術は彼らのような人々の挑戦によってゆっくりと普及しソリューションや教育環境が洗練されていきます。念の為言っておくと、NoSQLは昔ながらのストレージソリューションを置き換える手段ではないという事について大部分は事実です。しかしある特定の分野では従来のものに優る価値を提供します。

何よりもまず初めに、NoSQLが何を意味しているのかを説明すべきでしょう。それは人によって異なる意味を持つ広義の用語です。私は個人的にそれをデータストレージの役割を果たすシステムという意味で使用しています。言い換えれば、(私にとっての)NoSQLはあなたが執着する単一のシステムに必ずしも責任を持つようなものではありません。歴史的に見て、リレーショナルデータベースベンダーはどんな規模にも適応する万能なソリューションとしてソフトウェアを位置づけてきました。NoSQLスタックをMySQLといったリレーショナルデータベースの様に利用する事も出来るでしょうが、NoSQLは与えられた仕事を達成する為の最適なツールとしてより小さい単位の役割に向かう傾向があります。そして、Redisもまた参照性能というシステムの特定部位に執着し、同じようにHadoopもデータ処理に集中的です。簡単に言うと、NoSQLはオープンであり、既存のものの代替や付加的なパターンを意識し、データを管理する為のツールです。

あなたはMongoDBが多くの状況に適応する事に驚くかもしれません。MongoDBはドキュメント指向データベースとしてよりNoSQLソリューションに汎用化されています。それはリレーショナルデータベースの代替の様に見られるでしょうが、リレーショナルデータベースと比較すると、もっと専門化したNoSQLソリューションにおいて恩恵を得ることが出来ます。MongoDBには利点と欠点がありますのでそれには後ほどこの本の中で触れます。

# はじめよう # {-}
この本の大部分はMongoDBの機能面に注目します。その為に私たちはMongoDBシェルを利用します。MongoDBドライバを利用するようになるまで、MongoDBシェルは学習に役立つだけでなく、便利な管理ツールとなるでしょう。

MongoDBについてまず最初に知るべきことを取り上げます: それはドライバです。MongoDBは各種プログラミング言語向けに[数多くの公式ドライバ](http://docs.mongodb.org/ecosystem/drivers/)が用意されています。これらのドライバは恐らくあなたがすでに慣れ親しんでいる各種データベースのドライバと似たようなものだと考えて良いでしょう。これらのドライバに加えて、開発コミュニティでは更にプログラミング言語/フレームワーク用のライブラリが開発されています。例えば、[NoRM](https://github.com/atheken/NoRM)はLINQを実装したC#のライブラリで、[MongoMapper](https://github.com/jnunemaker/mongomapper)はActiveRecordと親和性の高いRubyライブラリです。プログラムから直接MongoDBのコアドライバを利用するか、他の高級なライブラリを選択するかはあなた次第です。何故、公式ドライバとコミュニティライブラリの両方が存在するのかについてMongoDBに不慣れな多くの人に混乱があるようなので説明しておきます。前者はMongoDBの中核的な通信と接続性に、後者はプログラミング言語や特定のフレームワークの実装により特化しています。

これを読みながらあなたは私の実習を実際に反復し、自分自身で疑問を探っていく事を推奨します。MongoDBの準備と実行は簡単です、今から数分の時間をかけてセットアップしてみましょう。

 1. [公式ダウンロードページ](http://www.mongodb.org/downloads)へ進み、一番上の行からOSを選択してバイナリを手に入れましょう(安定バージョンを推奨)。開発目的であれば32ビット64ビットのどちらを選んでも構いません。

 2. アーカイブを適当な場所に展開し、`bin`サブフォルダへ移動します。まだ何も実行しないこと、`mongod`がサーバープロセスであり、`mongo`がクライアントシェルであることは知っておいて下さい。その2つはこれから私たちが最も時間を費やす実行ファイルです。

 3. `bin`サブフォルダの中に`mongodb.config`という名前で新しいテキストファイルを作成します。

 4. `mongodb.config`に以下の1行を追記します:

        dbpath=データーベースファイルを格納する場所

    例えば、Windowsでは`bpath=c:\mongodb\data`を指定し、Linuxでは`dbpath=/var/lib/mongodb/data`と指定します。

 5. 指定した`dbpath`を作成する。

 6. mongodを`--config /path/to/your/mongodb.config`パラメーターを付けて起動します。

Windowsユーザーの為の例を示すと、もしダウンロードファイルを`c:\mongodb\`に展開したのなら`c:\mongodb\bin\mongodb.config`に`dbpath=c:\mongodb\data\`を指定すると、`c:\mongodb\data\`が作成されます。次に、コマンドプロンプトから `c:\mongodb\bin\mongod --config c:\mongodb\bin\mongodb.config`を実行して`mongod`を起動します。

無駄を少なくする為に、ご自由に`bin`フォルダをパスに追加して下さい。MacOSXとLinuxユーザーはほとんど同じやり方に従うことが出来ます。あなたがすべきことはパスを変更することくらいです。

うまくいけば今あなたはMongoDBを実行しているでしょう。もしエラーが起こったのならメッセージを注意深く読んで下さい。サーバーは何がおかしいのかを丁寧に説明してくれます。

あなたは`mongo`(**d**は付かない)を起動し、実行中のサーバーのシェルに接続する事が出来ます。全てが動作しているか確認するために`db.version()`と入力してみて下さい、うまくいっていればインストールされているバージョンを確認することが出来るでしょう。

# 基礎
MongoDBの動作の基本的な仕組みを知ることからはじめましょう。当然これはMongoDBの核心を理解することです。しかしこれはMongoDBについての高レベルな質問の答えを見つけ出す為にも役立ちます。

最初に、私たちは6つの概念を理解する必要があります。

1. MongoDBはあなたが既に慣れ親しんでいる**データベース**と同じ概念を持っています(あるいはOracleでいうところのスキーマ)。MongoDBインスタンスの中には0個以上のデータベースを持つことが出来、それぞれは高レベルコンテナの様に作用します。

2. データベースは0個以上の**コレクション**を持つことが出来ます。コレクションは従来の**テーブル**とほぼ共通しているので、この2つが同じものだと思っても支障は無いでしょう。

3. コレクションは0個以上の**ドキュメント**を作成できます。先ほどと同様にドキュメントを**行**と思って構いません。

4. ドキュメントは1つ以上の**フィールド**を作成できます。あなたは恐らくこれを**列**に似ていると推測できるでしょう。

5. MongoDBでの**インデックス**機能はRDBMSのものとよく似ています。

6. **カーソル**はこれまでの5つの概念とは異なりとても重要で見落とされがちですので詳しく説明する必要があると思います。カーソルについて理解すべき重要な点は、MongoDBにデータを問い合わせるとカーソルと呼ばれる結果データへのポインタを返します。カーソルは実際のデータを取り出す前に、カウントやスキップの様な操作はを行うことが出来ます。

要点をまとめると、MongoDBは**データベース**を作成し、その中には**コレクション**を含みます。**コレクション**は**ドキュメント**を作成します。それぞれの**ドキュメント**は**フィールド**を作成します。**コレクション**は**インデックス化**可能であり、これは参照やソートの性能を改善します。最後に、MongoDBからデータを取得する際、**カーソル**を経由して操作を行います。これは実際に実行する際に必要不可欠なものです。

なぜ新しい専門用語を利用するのでしょうか(コレクションとテーブル、ドキュメントと行、フィールドと列)。物事を複雑にするだけでしょうか?これらの概念がリレーショナルデータベースの機能と良く似ているという点ではその通りですが、これらは全く同じではありません。主要な違いは、リレーショナルデータベースが**テーブル**のレベルに**列**を定義しているのに対し、ドキュメント指向データベースは**ドキュメント**のレベルに**フィールド**を定義している事です。**コレクション**の中の**ドキュメント**はそれ自身の独自の**フィールド**を持つことが出来ると言えます。という訳で、**コレクション**は**テーブル**に比べ、より使い易いコンテナとなり、さらに**ドキュメント**は**行**に比べてより多くの情報を持つようになります。

これを理解することは重要ですが、もしこれをまだ完全に理解出来ていなくても心配することはありません。この本当の意味を確かめる為にはまだもう少し説明が必要でしょう。突き詰めていくとコレクションの中に何が入るかが厳密ではない事が要点です(スキーマレスの事)。フィールドは特定のドキュメントに対して追従します。あとの章で利点と欠点に気がつくでしょう。

さあハンズオンをはじめましょう。まだ動かしていないのなら、どうぞ`mongod`サーバーとmongoシェルを起動して下さい。シェルはJavaScriptを実行できます。`help`や`exit`の様な、幾つかのグローバルコマンドを実行することが出来ます。例えば、`db.help()`や`db.stats()`といったコマンドは、現在のデータベース`db`オブジェクトに対して実行します。`db.unicorns.help()`や`db.unicorns.count()`といったコマンドは、`db.COLLECTION_NAME`オブジェクトの様に、指定したそれぞれのコレクションに対して実行します。

どうぞ、`db.help()`と入力してみて下さい。`db`オブジェクトに対して実行可能なコマンド一覧を得ることが出来るでしょう。

余談ですが、あなたが丸カッコ`()`を含めずにメソッドを実行した場合、メソッドの実行ではなくメソッドの本体が表示されます。これはJavaScriptシェルだからです。あなたが最初にこれをやった時、`function (...){`という応答が返ってきても驚かないように、この事に触れておきました。たとえば、丸カッコ無しで`db.help`と入力すると`help`メソッドの内部実装を見ることが出来ます。

まず私たちはグローバルな`use`ヘルパー使ってデータベースを切り替えます。どうぞ`use learn`と入力してみて下さい。そのデータベースが実際に存在していなくても構いません。最初のコレクションを`learn`に作成しましょう。今あなたはデータベースの中にいて、`db.getCollectionNames()`という様なデータベースコマンドを発行できます。これを実行すると、恐らく空の配列(`[ ]`)が返ってくるでしょう。コレクションはスキーマレスですので、それらを明確に作成する必要はありません。私たちは、単純にドキュメントをコレクションに作成する事が出来ます。それでは、`insert`コマンドを使ってコレクションにドキュメント挿入してみましょう。

~~~ {.javascript}
db.unicorns.insert({name: 'Aurora', gender: 'f', weight: 450})
~~~

上記のコマンドは一つの引数を受け取り`unicorns`コレクションに対して`insert`を行います。
MongoDBの内部ではBSONというバイナリでシリアライズされたJSONフォーマットを利用します。
外側から見るとJSONをいろいろ使っているように見えます。
ここで`db.getCollectionNames()`を実行すると`unicorns`コレクションが表示されます。

これで、`unicorns`に対し`find`コマンドを使用してドキュメントのリストを取得出来るようになりました。

~~~ {.javascript}
db.unicorns.find()
~~~

あなたが挿入したデータに`_id`フィールドが追加されていることに注目して下さい。全てのドキュメントはユニークな`_id`フィールドを持たなくてはいけません。これは`ObjectID`型の値を自分で生成するかMongoDBに生成させる事になります。ほとんどの場合MongoDBに生成させたいと思うでしょう。`_id`フィールドには既定でインデックスが貼られます。これは`getIndexes`コマンドで確認できます。

~~~ {.javascript}
db.unicorns.getIndexes()
~~~

あなたはインデックスを含むフィールドに対して作成されたデータベースやコレクションのインデックス名を確認することが出来ます。

スキーマレスコレクションの話に戻りましょう。`unicorns`コレクションに以下の様な完全に異なるドキュメントを入れてみます:

~~~ {.javascript}
db.unicorns.insert({name: 'Leto', gender: 'm', home: 'Arrakeen', worm: false})
~~~

再度`find`を利用してドキュメントを表示してみて下さい。MongoDBの興味深い振る舞いについて前に少しだけ話しました、何故従来の技術がうまく適応しなかったのかが解り始めて来たのではないでしょうか。

## セレクターの習得 ##
次の話題に進む前に、先程説明した6つの概念に加え、MongoDBの実用面でしっかりと理解すべきことがあります。それはクエリーセレクターです。MongoDBのクエリーセレクターはSQL構文の`where`節によく似ています。そういうわけで、これはドキュメントを見つけ出したり、数えたり、更新したり、削除したりする際に使用します。セレクターはJSONオブジェクトです。最も単純な`{}`は全てのドキュメントにマッチします(`null`も同じです)。もしメスのユニコーンを見つけたい場合、`{gender:'f'}`と指定します。

セレクターについて掘り下げていく前に、演習の為のデータを幾つかセットアップしましょう。まず、これまでに`unicorns`コレクションに入れたドキュメントを`db.unicorns.remove({})`を実行して削除します。さて、以下を実行して演習に必要なデータを挿入しましょう(コピペ推奨):

~~~ {.javascript}
db.unicorns.insert({name: 'Horny', dob: new Date(1992,2,13,7,47),
                    loves: ['carrot','papaya'], weight: 600,
                    gender: 'm', vampires: 63});
db.unicorns.insert({name: 'Aurora', dob: new Date(1991, 0, 24, 13, 0),
                    loves: ['carrot', 'grape'], weight: 450,
                    gender: 'f', vampires: 43});
db.unicorns.insert({name: 'Unicrom', dob: new Date(1973, 1, 9, 22, 10),
                    loves: ['energon', 'redbull'], weight: 984,
                    gender: 'm', vampires: 182});
db.unicorns.insert({name: 'Roooooodles', dob: new Date(1979, 7, 18, 18, 44),
                    loves: ['apple'], weight: 575,
                    gender: 'm', vampires: 99});
db.unicorns.insert({name: 'Solnara', dob: new Date(1985, 6, 4, 2, 1),
                    loves:['apple', 'carrot', 'chocolate'], weight:550,
                    gender:'f', vampires:80});
db.unicorns.insert({name:'Ayna', dob: new Date(1998, 2, 7, 8, 30),
                    loves: ['strawberry', 'lemon'], weight: 733,
                    gender: 'f', vampires: 40});
db.unicorns.insert({name:'Kenny', dob: new Date(1997, 6, 1, 10, 42),
                    loves: ['grape', 'lemon'], weight: 690,
                    gender: 'm', vampires: 39});
db.unicorns.insert({name: 'Raleigh', dob: new Date(2005, 4, 3, 0, 57),
                    loves: ['apple', 'sugar'], weight: 421,
                    gender: 'm', vampires: 2});
db.unicorns.insert({name: 'Leia', dob: new Date(2001, 9, 8, 14, 53),
                    loves: ['apple', 'watermelon'], weight: 601,
                    gender: 'f', vampires: 33});
db.unicorns.insert({name: 'Pilot', dob: new Date(1997, 2, 1, 5, 3),
                    loves: ['apple', 'watermelon'], weight: 650,
                    gender: 'm', vampires: 54});
db.unicorns.insert({name: 'Nimue', dob: new Date(1999, 11, 20, 16, 15),
                    loves: ['grape', 'carrot'], weight: 540,
                    gender: 'f'});
db.unicorns.insert({name: 'Dunx', dob: new Date(1976, 6, 18, 18, 18),
                    loves: ['grape', 'watermelon'], weight: 704,
                    gender: 'm', vampires: 165});
~~~

さて、データが入りましたのでセレクターを習得しましょう。`{field: value}`は`field`というフィールドが`value`と等しいドキュメントを検索します。`{field1: value1, field2: value2}`は`and`式で検索します。`$lt`、 `$lte`、 `$gt`、 `$gte`、 `$ne`はそれぞれ、未満、以下、より大きい、以上、非等価、を意味する特別な演算子です。例えば、性別がオスで体重が700ポンドより大きいユニコーンを探すにはこのようにします:

~~~ {.javascript}
db.unicorns.find({gender: 'm', weight: {$gt: 700}})
// このセレクターは以下と同等です。
db.unicorns.find({gender: {$ne: 'f'}, weight: {$gte: 701}})
~~~

`$exists`演算子はフィールドの存在や欠如のマッチに利用します。例えば:

~~~ {.javascript}
db.unicorns.find({vampires: {$exists: false}})
~~~

ひとつのドキュメントが返ってくるはずです。`$in`演算子は配列で渡した値のいずれかにマッチします。例えば:

~~~ {.javascript}
db.unicorns.find({loves: {$in:['apple','orange']}})
~~~

これで`apple`または`orange`が好きなユニコーンが返ります。

異なるフィールドに対してANDなどではなくORを利用したい場合、`$or`演算子を利用して、ORをとりたいセレクターの配列を指定します。

~~~ {.javascript}
db.unicorns.find({gender: 'f', $or: [{loves: 'apple'},
                                     {weight: {$lt: 500}}]})
~~~

上記は全てのメスのユニコーンの中からりんごが好き、もしくは体重が500ポンド未満の条件で検索します。

最後2つはとてもイカした用例です。お気づきと思いますが`loves`フィールドは配列です。MongoDBはファーストクラスオブジェクトとしての配列をサポートしています。これはとんでもなく便利な機能です。一度これを使ってしまうと、これ無しでは生活できなくなる恐れがあります。何よりも興味深いのは配列の値に基づいて簡単に選択できることです。`{loves: 'watermelon'}` は`loves`の値に`watermelon`を持つドキュメントを返します。

これまでに見てきた他に、演算子はまだまだあります。最も柔軟な`$where`は指定したJavaScriptをサーバー上で実行します。MongoDBのドキュメントの[Query Selectors](http://docs.mongodb.org/manual/reference/operator/query/#query-selectors)の項に全てが記載されています。これまでに紹介してきたものはあなたが使い始めるのに必要な基本です。もっと使いこなせるようになるには多くの時間がかかるでしょう。

これまでセレクターは`find`コマンドで利用できることを見てきました。これらは以前ちょっとだけ利用した`remove`コマンドやまだ使っていない`count`コマンド、後で出てくる`update`コマンドでも利用できます。

`ObjectId`はMongoDBが生成した`_id`フィールドを選択するために利用します:

~~~ {.javascript}
db.unicorns.find({_id: ObjectId("TheObjectId")})
~~~

## 章のまとめ ##
私たちはまだ`update`コマンドや、`find`で出来る幾つかの手の込んだ操作については学んでいませんが、`insert`コマンドと`remove`コマンドについて簡単に学びました(これまで見てきた以上のものはそれほど多くありません)。
私たちは`find`の紹介とMongoDBの`selectors`というものも見てきました。私たちは順調なスタートと、来たるべき時の為の盤石な基礎を築く事が出来ました。信じようと信じまいと、実際にあなたはMongoDBを使い始めるために知るべき殆どの事を知っています(素早く学習し、簡単に使えるようになるという意味でです)。
次に移る前に、演習のデータをローカルコピーすることを強く推奨します。恐らく、新しいコレクションで違うドキュメントを挿入したり、セレクターと似たようなものを使います。`find`や`count`や`remove`も使います。いろいろ試しているうちに、なにかマズイ事が起こった場合に最初の状態に戻れるようにしておいた方が良いでしょう。


# 更新
1章ではCRUD(作成、読み込み、更新、削除)の4つのうちの3つの操作を紹介しました。この章では、省略していた`update`に専念します。その理由は、`update`には幾つかの意外な振る舞いがあるからです。

## 更新: 置換 と $set ##
最も単純な形式では`update`に2つの引数を渡します。セレクター(where条件)と更新を適用するフィールドです。もしRoooooodlesの体重を少し増やしたい場合は以下を実行します:

~~~ {.javascript}
db.unicorns.update({name: 'Roooooodles'}, {weight: 590})
~~~

(もし前回の演習で作成した`unicorns`コレクションを残していない場合、1章に戻って、全てのドキュメントを`remove`し、挿入し直して下さい。)

アップデートされたレコードを確認する場合、以下のようにします:

~~~ {.javascript}
db.unicorns.find({name: 'Roooooodles'})
~~~

あなたは`update`の動作に驚くはずです。
2番目のパラメータに更新演算子を指定しなかったので元のデータを**置き換える**動作となり、元のドキュメントは見つかりません。
言い換えると、`update`はドキュメントを`name`で検索し、ドキュメント全体を2番目のパラメータで置き換えます。
SQLの`update`文にこれと同等の機能はありません。
本当に動的な更新を行いたい場合などの特定の状況で、これは理想的な動作です。
しかし、ひとつか複数のフィールドの値を変更したい場合はMongoDBの`$set`演算子を利用すべきです。
以下のように実行して消えたフィールドをもとに戻します:

~~~ {.javascript}
db.unicorns.update({weight: 590}, {$set: {name: 'Roooooodles',
                                          dob: new Date(1979, 7, 18, 18, 44),
                                          loves: ['apple'],
                                          gender: 'm',
                                          vampires: 99}})
~~~

このように`weight`を指定しなければ上書きできません。以下を実行します:

~~~ {.javascript}
db.unicorns.find({name: 'Roooooodles'})
~~~

期待する結果が得られました。従って、最初に行いたかった体重を変更する正しい方法は以下の通りです:

~~~ {.javascript}
db.unicorns.update({name: 'Roooooodles'}, {$set: {weight: 590}})
~~~

## 更新演算子 ##
`$set`に加え、その他の演算子を利用するともっと粋なことが出来ます。これらの更新演算子は、フィールドに対して作用します。なのでドキュメント全体が消えてしまうことはありません。例えば、`$inc`演算子はフィールドの値を増やしたり、負の値で減らす事が出来ます。もしPilotが`vampire`を倒した数が間違っていて2つ多かった場合、以下のようにして間違いを修正します:

~~~ {.javascript}
db.unicorns.update({name: 'Pilot'}, {$inc: {vampires: -2}})
~~~

もしAuroraが突然甘党になったら、`$push`演算子を使って、`loves`フィールドに値を追加することが出来ます:

~~~ {.javascript}
db.unicorns.update({name: 'Aurora'}, {$push: {loves: 'sugar'}})
~~~

その他の有効な更新演算子はMongoDBマニュアルの[更新演算子]((http://docs.mongodb.org/manual/reference/operator/update/#update-operators)に情報があります。

## Upsert ##
`update`の使い方にはもっと驚く愉快なものがあります。その一つは`upsert`を完全にサポートしている事です。`upsert`はドキュメントが見つかった場合に更新を行い、無ければ挿入を行います。`upsert`は可読性が良く、よくあるシチュエーションで重宝します。`update`の3番目の引数に`{upsert:true}`を渡す事で`upsert`を利用できます。

一般的な例はWebサイトのカウンターです。複数のページのカウンターをリアルタイムに動作させたい場合、ページのレコードが既に存在しているか確認し、更新を行うか挿入を行うか決めなければなりません。`upsert`パラメータを省略(もしくはfalseに設定)して実行すると、以下のようにうまくいきません:

~~~ {.javascript}
db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}});
db.hits.find();
~~~

しかし、upsertオプション加えると違った結果になります。

~~~ {.javascript}
db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}}, {upsert:true});
db.hits.find();
~~~

`page`というフィールドの値が`unicorns`のドキュメントが存在していなければ、新しいドキュメントが挿入されます。2回目を実行すると既存のドキュメントが更新され、`hits`は2に増えます。

~~~ {.javascript}
db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}}, {upsert:true});
db.hits.find();
~~~

## 複数同時更新 ##
最後の驚きは、`update`はデフォルトで一つのドキュメントに対してのみ更新を行う事です。これまでの様に、まず例を見ていきましょう。以下のように実行します:

~~~ {.javascript}
db.unicorns.update({}, {$set: {vaccinated: true }});
db.unicorns.find({vaccinated: true});
~~~

あなたは全てのかわいいユニコーン達に予防接種を受けさせた(vaccinated)としましょう。これを行うには、`multi`オプションをtrueに設定します:

~~~ {.javascript}
db.unicorns.update({}, {$set: {vaccinated: true }}, {multi:true});
db.unicorns.find({vaccinated: true});
~~~

## 章のまとめ ##
この章でコレクションに対して行う基本的なCRUD操作を紹介し終えました。私たちは`update`の詳細を確認し、3つの興味深い振る舞いを観察しました。まず、MongoDBの`update`は更新演算子を使わないと既存のドキュメントを置き換えます。通常は`$set`などの様々な演算子を利用してドキュメントを変更します。次に、`update`は直感的な`upsert`オプションをサポートしています。これはドキュメントが存在するかどうか分からない時に便利です。最後に、デフォルトで`update`は最初にマッチしたドキュメントしか更新しません。マッチしたすべてのドキュメントを更新したい場合は`multi`オプションを指定してください。

私たちはシェルの視点からMongoDBを見てきた事を思い出して下さい。ドライバやライブラリの場合でも、デフォルトの振る舞いを切り替えて使用したり、異なるAPIに触れる事になります。

例えば、Rubyのドライバでは最後の2つのパラメータを一つのハッシュにまとめています:

~~~ {.javascript}
{:upsert => false, :multi => false}
~~~

同様に、PHPのドライバも最後の2つのパラメータを配列にまとめています。

~~~ {.javascript}
array('upsert' => false, 'multiple' => false)
~~~

# 検索の習得
1章では、`find`コマンドについて簡単に説明しました。ここでは`find`やセレクターについての理解を深めていきます。`find`が**カーソル**を返却することについては既に述べましたので、もっと正確な意味を見ていきましょう。

## フィールド選択 ##
**カーソル**について学ぶ前に、`find`に任意で設定出来る"projection"という2番目のパラメータについて知る必要があります。このパラメーターは取得、もしくは除外したいフィールドのリストです。例えば、以下の様に実行して、全てのユニコーンの名前をその他のフィールドを除外して取得します。

~~~ {.javascript}
db.unicorns.find({}, {name: 1});
~~~

デフォルトで、`_id`フィールドは常に返却されます。明示的に`{name:1, _id: 0}`を指定する事でそれを除外する事が出来ます。

`_id`に関する余談ですが、包含条件と排他条件を混ぜることが出来るのかどうか、気になるかもしれません。あなたはフィールドを含めるか除くかのどちらかを選択することが出来ます。

## 順序 ##
これまでに何度か`find`が必要な時に遅延して実行されるカーソルを返すと説明しました。しかしシェルは`find`を即座に処理を実行しているように見えるます。これはシェルだけの動作です。カーソルの本当の動作は`find`にメソッドをひとつ連結することで観測出来ます。まずはソートを見てみましょう。JSONドキュメントのフィールドを昇順でソートを行いたい場合はフィールドと1を指定し、降順で行いたい場合は-1を指定します。例えば:

~~~ {.javascript}
//重いユニコーンの順
db.unicorns.find().sort({weight: -1})

//ユニコーンの名前とvampiresの多い順:
db.unicorns.find().sort({name: 1, vampires: -1})
~~~

リレーショナルデータベースと同様に、MongoDBもソートの為にインデックスを利用出来ます。インデックスの詳細は後で詳しく見ていきますが、MongoDBにはインデックスを使用しない場合にソートのサイズ制限があることを知っておく必要があります。すなわち、もし巨大な結果に対してソートを行おうとするとエラーが返ってきます。実際の話、その他のデータベースにも、最適化されていないクエリーを拒否する機能があった方が良いと考えています。(私はこの動作をMongoDBの欠点とは考えていませんし、データベースの最適化が下手な人達にこの機能を使って欲しいと強く願っています。)

## ページング ##
ページングはcursorの`limit`メソッドや`skip`メソッドを利用して実現できます。2番目と3番目に重いユニコーンを得るにはこうやります:

~~~ {.javascript}
db.unicorns.find().sort({weight: -1}).limit(2).skip(1)
~~~

`limit`と`sort`を組み合わせると、インデックス化されていないフィールドでソートする場合の問題を避けることができます。

## カウント ##
シェルではcollectionに対して直接`count`を呼び出す事が出来ます。例えば:

~~~ {.javascript}
db.unicorns.count({vampires: {$gt: 50}})
~~~

実際には`count`は`cursor`のメソッドであり、シェルは単純なショートカットを提供しているだけです。この様なショートカットを提供しないドライバでは以下の様に実行する必要があります(これはシェルでも動きます):

~~~ {.javascript}
db.unicorns.find({vampires: {$gt: 50}}).count()
~~~

## 章のまとめ ##
`find`や`cursor`の率直な使われ方を見てきました。これらの他に、あとの章で触れるコマンドや特別な状況で使われるコマンドが存在しますが、あなたは既にMongoDBの基礎を理解し、mongoシェルを安心して触れるようになったでしょう。

# データモデリング
さて、MongoDBのもっと抽象的な話題に移っていきましょう。幾つかの新しい用語や、些細な機能の新しい文法について説明していきます。新しいパラダイムであるモデリングについての話題は簡単ではありません。モデリングに関する新しい技術について、大抵の人々はまだ何が役に立ち、役に立たないのかをよく知りません。まずは講話から始めますが、最終的には実際のコードで学び、実践を行っていきます。

モデリングに関して言うと、NoSQLデータベースの中でドキュメント指向データベースはリレーショナルデータベースと多くの部分で共通しています。しかし重要な違いがあります。

## Joinがありません ##
まず最初に、最も根本的な違いであるMongoDBにJoinが存在しない事に対して安心する必要があるでしょう。MongoDBが何故joinの文法をサポートしていないのか、特別な理由を私は知りませんが、Joinがスケーラブルでない事は一般的に知られています。すなわち、一度データの水平分割を行うと、最終的にクライアント(アプリケーションサーバー)側でJoinを行う事になります。理由はどうあれ、データはリレーショナルである事に変り在りませんが、MongoDBはJoinをサポートしていません。

とにかく、Join無しの世界で生活するためにはアプリケーションのコード内でJoinを行わなくてはなりません。それには基本的に2度の`find`クエリーを発行して2つ目のコレクション内の関連データを取得する必要があります。これから準備するデータはリレーショナルデータベースの外部キーと違いはありません。しばらく素敵な`unicorns`コレクションから視点を外して、`employees`コレクションに注目してみましょう。まず最初に、社員を作成します。(分かり易く説明する為に、`_id`フィールドを明示的に指定しています)

~~~ {.javascript}
db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d730"), name: 'Leto'})
~~~

さて、`Leto`がマネージャーとなる様に設定した社員を何人か追加してみましょう:

~~~ {.javascript}
db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d731"), name: 'Duncan',
                     manager: ObjectId("4d85c7039ab0fd70a117d730")});
db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d732"), name: 'Moneo',
                     manager: ObjectId("4d85c7039ab0fd70a117d730")});
~~~

(上記に倣って、`_id`はユニークになる必要があります。
ここで実際に指定した`ObjectId`を、以降も同じ様に使用する事になります。)

言うまでもなく、Letoの社員を検索するには単純に以下を実行します:

~~~ {.javascript}
db.employees.find({manager: ObjectId("4d85c7039ab0fd70a117d730")})
~~~

これは何の変哲もありません。
最悪の場合、joinの欠如はただ単に余分なクエリーが多くの時間を占めるかもしれません
(恐らくインデックス化されているでしょうが)。

### 配列と埋め込みドキュメント ###
MongoDBがjoinを持たないからといって、切り札が無いという意味ではありません。MongoDBのドキュメントがファーストクラスオブジェクトとしての配列をサポートしている事を簡単に確認したのを思い出してください。これは、多対一、多対多の関係を表現する際にとても器用に役立つ事が分かります。簡単な例として、社員が複数のマネージャーを持つ場合、単純にこれらを配列で格納する事が出来ます:

~~~ {.javascript}
db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d733"), name: 'Siona',
                     manager: [ObjectId("4d85c7039ab0fd70a117d730"),
                               ObjectId("4d85c7039ab0fd70a117d732")]})
~~~

特に興味深い事は、ドキュメントはスカラ値であっても構わないし、配列であっても構わないという点です。最初の`find`クエリーはどちらであっても動作します:

~~~ {.javascript}
db.employees.find({manager: ObjectId("4d85c7039ab0fd70a117d730")})
~~~

これによって、多対多のjoinテーブルよりもっと便利に素早く配列の値を見つけることが出来ます。

配列に加えて、MongoDBは埋め込みドキュメントをサポートしています。次に進んで入れ子になったドキュメントを挿入してみてください:

~~~ {.javascript}
db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d734"), name: 'Ghanima',
                     family: {mother: 'Chani',
                              father: 'Paul',
                              brother: ObjectId("4d85c7039ab0fd70a117d730")}})
~~~

驚くでしょうが、埋め込みドキュメントはクエリーにドット表記を使用できます:

~~~ {.javascript}
db.employees.find({'family.mother': 'Chani'})
~~~

埋め込みドキュメントがどの様な場所に適合し、どの様に使用するかを簡単に説明します。

2つのコンセプトを組み合わせて埋め込みドキュメントの配列を埋め込むこともできます。

~~~ {.javascript}
db.employees.insert({_id: ObjectId(
                     "4d85c7039ab0fd70a117d735"),
                     name: 'Chani',
                     family: [ {relation:'mother',name: 'Chani'},
                               {relation:'father',name: 'Paul'},
                               {relation:'brother', name: 'Duncan'}]})
~~~


### 非正規化 ###
joinを代替するもうひとつの方法はデータを非正規化する事です。従来、非正規化はパフォーマンス特化の為やスナップショットデータ(監査ログの様な)の為に利用されてきました。ところが、NoSQLの人気が高まるにつれて、joinを行わないことや非正規化は次第に一般的なモデリング手法として認められるようになってきました。これは各ドキュメントで各情報の断片を重複させろという意味ではありません。データの重複を恐れながら設計するのではなく、データがどの情報に基づいていてどのドキュメントに属しているかをよく考えてモデリングしましょう。

例えば、掲示板のWEBアプリケーションを作っているとします。伝統的な方法では`posts`テーブルに`ユーザーID`を持たせて**ユーザー**と**投稿**を関連付けます。この様なモデルでは`users`テーブルを検索(もしくはjoin)しなければ**投稿**を表示することが出来ません。有効な代替案は各投稿エントリに単純にユーザーIDに対応するユーザー名を保持することです。埋め込みドキュメントでは以下のようにしします。

~~~ {.javascript}
`user: {id: ObjectId('Something'), name: 'Leto'}`
~~~

もちろんこうした場合、ユーザーが名前を変更すると全てのドキュメントを更新しなければなりません(1回のマルチアップデートで済みます)。

この種の取り組みを調整する事はそれほど簡単ではありません。多くの場合、この様な調整は非常識で効果が無いかもしれません。しかし、この取り組みへの実験を恐れないでください。状況によっては適切ではありませんが、その取り組みが効果的で最良の対処になることもあるでしょう。

### どちらを選ぶ? ###
1対多や多対多の関係のシナリオでIDを配列にする事は有用な戦略です。しかし一般的に新しい開発者は埋め込みドキュメントを利用するか手動で参照を行うか悩んでしまうでしょう。

まず、各ドキュメントのサイズは16MByteまでに制限されていることを知らなければなりません。ドキュメントのサイズに制限があるとわかった所で、気前よく替りにどの様にすれば良いかのアイディアを提供しましょう。現在の所、開発者が巨大なリレーションを行いたい場合、大抵は手動で参照しなければならない様に思われます。埋め込みドキュメントは頻繁に利用されますが、ほとんどの場合親ドキュメントと同時に取得したい小さなデータです。以下は各ユーザーのアカウントに住所を持たせる実例です:

~~~ {.javascript}
db.users.insert({name: 'leto',
                 email: 'leto@dune.gov',
                 addresses: [{street: "229 W. 43rd St",
                              city: "New York", state:"NY",zip:"10036"},
                             {street: "555 University",
                              city: "Palo Alto", state:"CA",zip:"94107"}]})
~~~

これを単に手っ取り早く書き込むための短縮記法だと過小評価してはいけません。直接ドキュメントを持つ事は、データモデルをより単純にし、多くの場合Joinの必要性を無くします。これは特に埋め込みドキュメントや配列のインデックスフィールドのクエリーに適応します。

## 少ないコレクションと多いコレクション ##
コレクションがスキーマを強制しないのであれば、単一のコレクションに様々なドキュメントをごちゃ混ぜにしたシステムを作ることも出来ますが、こんなことをしてはいけません。多くのMongoDBシステムはよく見るリレーショナルデータベースと同じ様に設計されますが、それよりもコレクションは少なくなります。
言い換えると、リレーショナルデータベースのテーブルは多くはMongoDBのコレクションで置き換えることが可能です。(多対多のJoinは重要な例外です)。

埋め込みドキュメントの懸念について面白い話題があります。よくある例はブログシステムです。`posts`コレクションと`comments`コレクションを別々に持つべきか、`post`ドキュメントにコメントの配列を埋め込むべきでしょうか?多くの開発者はまだコレクションを分割することを好むようですが、16MByteの制限はひとまず考えないようにしてみてはどうでしょうか(**ハムレット**の全文は200KByte以下です、あなたのブログはこれより有名なのですか?)。
それはより単純明快で、より良いパフォーマンスが得られます。
MongoDBの柔軟なスキーマはこの2つのアプローチを組み合わせて、別々のコレクションに分けたまま、少ない数のコメントを投稿に埋め込む事が出来ます。これは1回のクエリーで欲しいデータをまとめて取得するという原則に従っています。

16MByteの制限はそれほど難しいルールではありません。ぜひ今までと違った手法を試してみて、何が上手く行って何がうまく行かないのかを自分で確かめてみて下さい。

## 章のまとめ ##
この章の目標はMongoDBでデータをモデリングする為のガイドラインを示すことでした。ドキュメント指向システムのモデリングはリレーショナルデータベースの世界と異なりますが、それほど多くの違いはありません。あなたは多くの柔軟性と一つの制約を知りましたが、新しいシステムであれば上手く適合させることが出来るでしょう。誤った方向に進む唯一の方法は挑戦を行わない事です。

# どんな時MongoDBを利用するか
そろそろ、MongoDBを何処にどの様にして既存のシステムに適合させる為の感覚をつかむ必要があるでしょう。MongoDBにはその他多くの選択肢を簡単に凌駕する十分新しい競合ストレージ技術があります。

私にとって最も重要な教訓はMongoDBとは関係がありません。それはあなたがデータを扱う際に単一の解決手段に頼らなくてもよい様にすることです。たしかに、単一の解決手段を利用することは利点があります。多くのプロジェクトで単一の解決手段に限定することは場合によっては賢明な選択でしょう。異なるテクノロジを使用*しなければならない*と言うことではなく、異なるテクノロジを使用*できる*という発想です。あなただけが、新しいソリューションを導入することの利益がコストを上回るかどうかを知っています。

そんな訳で、これまで見てきたMongoDBの機能は一般的な解決手段として見なすことを期待しています。ドキュメント指向データベースがリレーショナルデータベースと共通する所が多い点については既に何度か言及してきました。そのために、MongoDBが単純にリレーショナルデータベースの代替になると言い切る事を慎重に扱って来ました。Luceneが全文検索インデックスによってリレーショナルデータベースを強化し、Redisが永続的なKey-Valueストアと見なすことが出来るように、MongoDBはデータの中央レポジトリとして見なすことが出来ます。

MongoDBはリレーショナルデータベースを*そのまま置き換える*様なものではなく、どちらかというと*別の代替手段*であると言っていることに注意して下さい。それはその他のツールと同様にツールなのです。MongoDBに向いている事もあれば、向いていない事もあります。それではもう少し詳しく分析してみましょう。

## 動的スキーマ ##
ドキュメント指向データベースの利点としてよくもてはやされるのは動的スキーマです。これは従来のデータベーステーブルに比べてはるかに柔軟性をもたらします。私は動的スキーマを素晴らしい機能だと認めますが、それが主な理由でない事に多くの人は言及しません。

人々はスキーマレスについて、突然狂った様にごちゃ混ぜなデータを格納し始めるのではないか、という様な事を話します。たしかにリレーショナルデータベースと同様のモデルで実際に痛みを伴うデータセットと領域が存在しますが、特殊なケースでしょう。スキーマレスは凄いのですが、殆んどのデータは高度に構造化されてしまいます。特に新しい機能を導入する場合、時々不整合を起こしやすいのは確かです。しかしNULLカラムが実際に上手く解決出来ない様な問題となる事は無いでしょう。

私にとって動的スキーマの本当の利点はセットアップの省略とオブジェクト指向プログラミングとの摩擦の低減です。これは、静的型付け言語を利用している場合に特に当てはまります。私はこれまでC#とRubyでMongoDBを利用してきましたが、違いは顕著です。Rubyのダイナミズムと有名なActiveRecord実装は既にオブジェクトとリレーショナルDBの摩擦を十分低減しています。それは実際にMongoDBがRubyと上手く適合していないと言っているわけではありません。どちらかというと多くのRuby開発者はMongoDBを追加の改善として見ると思います。一方、C#やJava開発者はこれらのデータ相互作用を根本的な変化として見るでしょう。

ドライバ開発者の視点で考えてみて下さい。オブジェクトを保存する際にJSON(正確にはBSONだけど大体同じ)にシリアライズしてMongoDBに送信します。プロパティマッピングや、型マッピングもありません。アプリケーション開発者が単純明快に実装できます。

## 書き込み ##
MongoDBが適合する専門的な役割のひとつはロギングです。MongoDBには書き込みを速くする2つの性質があります。1つ目は、送信した書き込み命令は実際の書き込み完了を待たず即座に戻ってくるオプションがあります。2つ目は、データの耐久性に関する動作を制御できる事です。これらの設定は何台のサーバーに書き込んだら成功とするかを設定することで書き込み性能と耐久性を絶妙にコントロール出来ます。

パフォーマンスに加え、ログデータはスキーマレスの利点を活かす事が出来るデータセットの一つです。最後に、MongoDBの[Cappedコレクション](http://docs.mongodb.org/manual/core/capped-collections/)と呼ばれる機能を紹介します。これまで作成してきたコレクションは暗黙的に普通のコレクションを作成してきました。cappedコレクションは`db.createCollection`コマンドにフラグを指定して作成します:

~~~ {.javascript}
// このCappedコレクションを1Mbyteで制限します
db.createCollection('logs', {capped: true, size: 1048576})
~~~

Cappedコレクションが1MByteの上限に達すると、古いドキュメントは自動的に削除されます。`max`オプションを指定することでドキュメントのサイズではなく数で制限できます。Cappedコレクションは幾つかの興味深い性質を持っています。例えば、ドキュメントの更新を行なってもサイズは増えません。挿入した順序を維持するので時間でソートする為のインデックスを貼る必要はありません。Unixのtail -f <ファイル名>コマンドのように、1回のクエリーでCappedコレクションをtailできます。

データを時間で有効期限切れにしたい場合、TTL(有効期間)インデックスを利用できます。

## 耐久性 ##
MongoDBバージョン1.8までは1台構成のサーバーに耐久性はありませんでした。サーバーがクラッシュした場合データを失う可能性が高かったのです。
解決策はMongoDBを複数台で構成するしかありませんでした(MongoDBはレプリケーションをサポートしています)。
ジャーナリングは1.8で追加された重要な機能のひとつです。
MongoDBバージョン2.0以降ジャーナリングは既定で有効になっているのでクラッシュや電源喪失からの迅速な復旧が可能です。

ここで耐久性に関して触れたのは、MongoDBに関する多くの情報の中で単一サーバーの耐久性に関する情報が不足していたからです。ググってみるとMongoDBにはジャーナリングが無いという古い情報が見つかります。

## 全文検索 ##
正真正銘の全文検索機能は最近のMongoDBに追加されました。
15の言語でステミング(語幹抽出)とストップワードに対応しています。
MongoDBは配列と全文検索に対応していますので、もっと強力な検索機能が必要な場合のみ、その他の全文検索エンジンと組み合わせる必要があるでしょう。

## トランザクション ##
MongoDBはトランザクションを持っていません。２つの代替手段を持っていて、１つめは素晴らしいのですが利用に制限があります、もうひとつの方法は柔軟性は高いのですが面倒です。

１つめの方法はアトミック操作です。それは素晴らしく実際の問題に適合します。既に`$inc`や`$set`などの単純な例を見てきました。`findAndModify`というドキュメントの更新と削除をアトミックに行うコマンドもあります。

２つめは、アトミック操作が不十分で二層コミットをフォールバックする際に利用します。二層コミットはJoinに手動参照するトランザクションです。それはコードの中で行うストレージから独立した解決手段です。二層コミットは複数のデータベースにまたがってトランザクションを行う為の方法としてリレーショナルデータベースの世界ではとても有名です。MongoDBのWebサイトに一般的なシナリオを解説した[例があります](http://www.mongodb.org/display/DOCS/two-phase+commit)(銀行口座)。基本的な考え方は、実際のドキュメントの中にトランザクションの状態を格納し、init-pending-commit/rollbackの段階を手動で行います。

MongoDBがサポートしている入れ子のドキュメントとスキーマレスな設計は二層コミットの痛みを少し和らげます。しかし初心者にとってはまだあまり良い方法では無いでしょう。

## データ処理 ##
バージョン2.2より前のMongoDBはデータ処理の殆どの仕事をMapReduceに頼っていました。
バージョン2.2以降、アグリゲーション・フレームワークやパイプラインと呼ばれる強力な機能が追加されましたので、MapReduceを使う必要があるのはパイプラインでサポートしていない複雑な関数での集約が必要な稀なケースに限られます。
アグリゲーション・パイプラインとMapReduceの詳細については次の章で説明します。
いまの所これらはグループ化する為の機能豊富な方法がいくつかある、と思っていてください。(控えめな言い方ですが)
巨大なデータを並列処理するにはHadoopの様なものと連携する必要があるでしょう。
ありがたい事に、お互いに補完し合う2つのシステムをつなげるためのMongoDBコネクタがHadoopにはあります。

もちろん並列データ処理はリレーショナルデータベースもそれほど得意とするものでもありません。MongoDBの将来のバージョンでは巨大なデータセットをもっと上手く扱えるようにする計画があります。

## 位置情報 ##
非常に強力な機能としてMongoDBは[位置情報インデックス](http://docs.mongodb.org/manual/applications/geospatial-indexes/)をサポートしています。geoJSONまたはxとyの座標をドキュメントに格納し、`$near`で指定した座標で検索したり、`$within`で指定した四角や円で検索を行えます。この機能は図で説明したほうが分かりやすいので[5分間位置情報チュートリアル](http://mongly.openmymind.net/geo/index)を試すことをお勧めします。

## ツールと成熟度 ##
既に知っていると思いますが、MongoDBはリレーショナルデータベースより新しいシステムです。何をどの様に行いたいかに依りますが、この事はよく理解しておくべきでしょう。それにしても率直に評価するとMongoDBは新しく、あまり良いツールが在るとは言えません。(とはいえ、成熟したリレーショナルデータベースのツールにも怖ろしく酷いものはあります!)例を挙げると、10進数での浮動小数点の欠如はお金を扱うシステムでは明らかな懸念点です。(それほど致命的ではありませんが)

良い面を挙げると、多くの有名な言語のドライバが存在します。プロトコルは単純で現代的で目まぐるしい速度で開発されています。MongoDBは多くの企業の製品に利用され、成熟度に関する懸念は急速に過去のものになりつつあります。

## 章のまとめ ##
この章で伝えたかったことは、MongoDBは大抵の場合リレーショナルデータベースを置き換えられるということです。もっと率直に言えば、それは速さの代わりに幾つかの制約をアプリケーション開発者に課します。トランザクションの欠如は正当で重要な懸念です。また、人々は尋ねます **「MongoDBは新しいデータストレージ分野の何処に位置するのでしょうか?」** 答えは単純です: **「ちょうど真ん中あたりだよ」**

# データの集計

## アグリゲーション・パイプライン ##
アグリゲーション・パイプラインはコレクション内のドキュメントを変換・結合する方法です。
ドキュメントをパイプラインに渡すという方法は出力データを別のコマンドに渡すUnixの「パイプ」とちょっと似ています。

最も単純なアグリゲーション（集約）はたぶん知っていると思いますがSQLの`GROUP BY`です。
既に`count()`関数を説明しましたが、ユニコーンをオスとメスで別々に集約したい場合はどうやるのでしょうか?

~~~ {.javascript}
db.unicorns.aggregate([{$group:{_id:'$gender',
                                total: {$sum:1}}}])

~~~

シェル内ではパイプライン演算子を配列で渡す`aggregate`ヘルパー関数があります。
何かを単純にグループ化して集約するには`$group`というオペレーターを利用します。
これはSQLの`GROUP BY`と似たようなもので、`_id`で指定したフィールドでグループ化(ここではgender)とその他フィールドの集約結果(ここでは特定の性別にマッチするドキュメントの合計数)で新しいドキュメントを生成します。
多分気がついていると思いますが`_id`フィールドには`gender`でなく`$gender`を渡しています。
フィールド名の前の`$`はドキュメントのフィールド値に置き換えられます。

他にはどんなパイプライン演算子があるのでしょうか。
`$match`演算子は`$group`演算子の前後でよく使われます。
これは`find`メソッドと同じ様に条件にマッチする、あるいはマッチしないドキュメントの部分集合を集約します。

~~~ {.javascript}
db.unicorns.aggregate([{$match: {weight:{$lt:600}}},
                       {$group: {_id:'$gender',  total:{$sum:1},
                                 avgVamp:{$avg:'$vampires'}}},
                       {$sort:{avgVamp:-1}} ])
~~~


ここで紹介したパイプライン演算子`$sort`はたぶんあなたの期待通りに動作します。
もちろん`$skip`や`$limit`もあります。
また`$group`演算子で`$avg`を使用しています。

MongoDBの配列は強力でDBに格納されているデータはなんでも集約できます。
これらを全て正しく数え上げるにはデータを「平ら」にしてやる必要があります。

~~~ {.javascript}
db.unicorns.aggregate([{$unwind:'$loves'},
                       {$group: {_id:'$loves',  total:{$sum:1},
                                 unicorns:{$addToSet:'$name'}}},
                       {$sort:{total:-1}},
                       {$limit:1} ])
~~~

これは最も多くのユニコーン達に好まれている食べ物と各好物を好きなユニコーンの名前のリストを表示します。
`$sort`と`$limit`の組み合わせはいわゆる「トップN」のランキングを集計します。

findで指定する"projection"とよく似た[`$project`](http://docs.mongodb.org/manual/reference/operator/aggregation/project/#pipe._S_project)という強力なパイプライン演算子があります。
これは特定のフィールドを含めるだけでなく、既存のフィールドの値に基づいて新しいフィールドを作成・計算することができます。
たとえば、算術演算子を利用して複数のフィールドを足し合わせて平均値を求めたり、文字列演算子を利用して既存のフィールドの文字列を結合した新しいフィールドを生成できます。

ここで説明したのはアグリゲーションで出来ることのほんの一部です。
2.6でアグリゲーションは更に強力になりました。集約命令の結果をカーソルに戻したり`$out`パイプライン演算子を利用して結果を新しいコレクションに書き込むことが出来ます。
サポートされている更に多くのパイプラインと式演算子の利用例は[MongoDBマニュアル](http://docs.mongodb.org/manual/core/aggregation-pipeline/)を参照してください。

## MapReduce ##
MapReduceは2段階のステップに分かれています。最初にmapを行い、次にreduceを行います。mappingの段階で入力されたドキュメントを変換し、key=>valueのペアを出力します(キーと値は複合できます)。次にkey/valueペアをkey毎にグループ化します。reduceの段階で出力されたキーと値の配列から最終的な結果を生成します。mapとreduce関数はJavaScriptで記述します。

MongoDBでは、コレクションに対して`mapReduce`命令を呼び出してMapReduceを行います。
`mapReduce`の引数にはmap関数とreduce関数、そして出力ディレクティブを引き渡します。
mongodbのシェルではJavaScriptの関数を定義して引数に指定します。
多くのライブラリでは関数を文字列で渡してやります(ちょっとカッコ悪いけど)。
3番目の引数にはドキュメント解析するためのフィルターやソート、リミットなどの追加のオプションを指定します。
さらに、`reduce`段階の後に評価される`finalize`メソッドを指定することも出来ます。

恐らくあなたは殆どのケースでMapReduceを使う必要はないでしょう。
もしその必要があった場合は[私のブログ](http://openmymind.net/2011/1/20/Understanding-Map-Reduce/)や[MongoDBマニュアル](http://docs.mongodb.org/manual/core/map-reduce/)を参照にしてください。

## 章のまとめ ##
この章ではMongoDBの[アグリゲーション機能](http://docs.mongodb.org/manual/aggregation/)を紹介しました。
アグリゲーションパイプラインはデータをグループ化する為の強力な手段であり、データ構造を把握していれば比較的単純に記述できます。
MapReduceはより理解するのが難しいですがJavaScriptで記述できるのでその能力は際限がありません。

# パフォーマンスとツール
最後の章では、パフォーマンスに関する話題とMongoDB開発者に有効な幾つかのツールを紹介します。どちらの話題にも深くは追求しませんがそれぞれの最も重要な部分を分析します。

## インデックス ##
まず最初に`getIndexes`コマンドで表示されるコレクション内のインデックス情報を見ていきましょう。
MongoDBのインデックスはリレーショナルデータベースのインデックスと同じように動作します。すなわち、これらはクエリーやソートのパフォーマンスを改善するのに役立ちます。インデックスは`ensureIndex`を呼んで作成されます:

~~~ {.javascript}
// この "name" はフィールド名です
db.unicorns.ensureIndex({name: 1});
~~~

そして、`dropIndex`を呼んで削除します:

~~~ {.javascript}
db.unicorns.dropIndex({name: 1});
~~~

2番目のパラメーターに`{unique: true}`に設定することでユニークインデックスを作成できます。

~~~ {.javascript}
db.unicorns.ensureIndex({name: 1}, {unique: true});
~~~

インデックスは埋めこまれたフィールドと配列フィールドに対して作成できます。
複合インデックスも作成できます:

~~~ {.javascript}
db.unicorns.ensureIndex({name: 1, vampires: -1});
~~~

インデックスの順序(1は昇順、-1は降順)は単一キーのインデックスでは影響ありませんが、複合キーで複数のインデックスフィールドをソートする際に違いがあります。

インデックスに関する詳しい情報は[indexes page](http://docs.mongodb.org/manual/indexes/)にあります。

## Explain ##
 インデックスを使用しているかに関わらず、カーソルに対し`explain`メソッドを使うことが出来ます:

~~~ {.javascript}
db.unicorns.find().explain()
~~~

出力は`BasicCursor`が利用され(インデックスを使用していない事を意味します)、あの12個のオブジェクトをスキャンしてどれくらいの時間がかかったのかなど、その他の便利な情報も教えてくれます。

もしインデックスを利用するように変更した場合`BtreeCursor`が利用されていることを確認できます。この場合、インデックスはうまく利用できているでしょう:

~~~ {.javascript}
db.unicorns.find({name: 'Pilot'}).explain()
~~~

## レプリケーション ##

MongoDBのレプリケーションはリレーショナルデータベースとよく似た仕組みで動作します。
理想的に、本番環境には同じデータを持つ3台以上のレプリカセットを配備してください。
単一のプライマリサーバーに対し書き込みが行われると、すべてのセカンダリサーバへ非同期に複製されます。
あなたはセカンダリサーバに対して読み込みリクエストを許可するかを制御できます。これは古いデータを読み込むリスクを低減させるのに役立ちます。
マスターが落ちた場合、セカンダリサーバの1つが新しいプライマリサーバに昇格します。
MongoDBのレプリケーションもこの本の主題の範囲外です。

## シャーディング ##

MongoDBは自動シャーディングをサポートしています。シャーディングはデータを複数のサーバーやクラスターに分割してスケーラビリティを高める手法です。単純な実装ではデータの名前がA〜Mで始まるものをサーバー1に、残りをサーバー2に格納するでしょう。有り難いことに、MongoDBのシャーディング能力はその単純なアルゴリズムを上回ります。シャーディングの話題はこの本では取り上げませんが、単一レプリカセットのデータが限界まで増えた時、あなたはシャーディングの存在を思い出して利用することを検討してください。

レプリケーションは時間の掛かる参照リクエストをセカンダリサーバに分散することでパフォーマンスの向上にも役立ちますが、主要な目的は信頼性の向上です。
シャーディングはMongoDBクラスタのスケーラビリティを向上させる事が主要な目的です。
レプリケーションとシャーディングを組み合わせることはスケーラビリティと高可用性を向上させるための常套手段です。

## 統計 ##
あなたは`db.stats()`とタイプすることでデータベースの統計を取得できます。データベースのサイズは最もよく扱う情報です。`db.unicorns.stats()`とタイプすることで`unicorns`というコレクションの統計を取得することも出来ます。同様にこのコレクションのサイズに関する情報も有用です。

## Webインターフェース ##
MongoDBを起動すると、Webベースの管理ツールに関する情報が含まれています(`mongod`を起動した時点までターミナルウィンドウをスクロールすればその様子を確認できるでしょう)。あなたはブラウザで <http://localhost:28017/> を開いてアクセス出来ます。設定ファイルに`rest=true`を追加して`mongod`プロセスを再起動すると、さらにこれを有効に活用出来るでしょう。このWebインターフェースはサーバの現在の状態についての洞察を与えてくれます。

## プロファイラ ##
以下を実行してMongoDBプロファイラを有効にします:

~~~ {.javascript}
db.setProfilingLevel(2);
~~~

有効にした後に、以下のコマンドを実行します:

~~~ {.javascript}
db.unicorns.find({weight: {$gt: 600}});
~~~

そして、プロファイラを観察して下さい:

~~~ {.javascript}
db.system.profile.find()
~~~

この出力は何がいつどれ程のドキュメントを走査し、どれ程のデータが返却されたかを教えてくれます。

再度、`setProfilingLevel`の引数を`0`に変えて呼び出すとプロファイラが無効化されます。
最初の引数に`1`を指定すると100ミリ秒以上掛かるクエリーをプロファイリングします。
100ミリ秒は既定のしきい値です。2番目の引数に最小のしきい値を指定できます。

~~~ {.javascript}
// 1秒以上のクエリーをプロファイルする
db.setProfilingLevel(1, 1000);
~~~

## バックアップとリストア ##
MongoDBには`bin`の中に`mongodump`という実行ファイルが付属しています。単純に`mongodump`を実行すると、ローカルホストに接続して全てのデータベースを`dump`サブフォルダ以下にバックアップします。`mongodump --help`とタイプすると追加のオプションを確認できます。指定したデータベースをバックアップする`--db DBNAME`と、指定したコレクションをバックアップする`--collection COLLECTIONNAME`は共通です。次に、同じ`bin`フォルダにある`mongorestore`実行ファイルを使うことで、以前のバックアップをリストアできます。同じように、`--db`と`--collection`はオプションはリストアするデータベースとコレクションを指定します。
`mongodump`と`mongorestore`はBSONというMongoDBの独自フォーマットを操作します。

例えば、`learn`データベースを`backup`フォルダにバックアップするには以下を実行します(これは実行ファイルですのでmongoシェルではなく、ターミナルウィンドウでコマンドを実行します):

~~~ {.bash}
mongodump --db learn --out backup
~~~

`unicorns`コレクションのみをリストアするにはこの様に実行します:

~~~ {.bash}
mongorestore --db learn --collection unicorns backup/learn/unicorns.bson
~~~

`mongoexport`と`mongoimport`という２つの実行ファイルはJSONまたはCSV形式でエクスポートとインポートできることを指摘しておきます。例えばJSON形式で出力するには以下のようにします:

~~~ {.bash}
mongoexport --db learn --collection unicorns
~~~

そして、CSV形式での出力はこうします:

~~~ {.bash}
mongoexport --db learn --collection unicorns \
  --csv --fields name,weight,vampires
~~~

`mongoexport`と`mongoimport`はデータを完全に表現できないことに注意して下さい。`mongodump`と`mongorestore`のみを実際のバックアップでは利用すべきです。
詳細はMongoDBマニュアルの[バックアップの選択肢](http://docs.mongodb.org/manual/core/backups/)を読んでください。

## 章のまとめ ##
この章では、MongoDBで利用する様々なコマンドやツールやパフォーマンスの詳細を見てきました。全てに触れることは出来ませんでしたが一般的なものをいくつか紹介しました。MongoDBのインデックス化がリレーショナルデータベースのインデックス化とよく似ているのと同様に、ツールの多くも同じです。しかしMongoDBの方がわかり易くて単純に利用できるものが多いでしょう。

# まとめ # {-}
実際のプロジェクトでMongoDBを使い始める為には十分な情報を持つべきです。
ここで紹介してきた事の他にも、MongoDBの情報はまだまだあります。しかし、あなたが次に優先すべき事は、これまでに学んできた事を組み合わせて、これから利用するドライバに慣れる事です。
[MongoDBのウェブサイト](http://www.mongodb.org/)には数多くの役立つ情報があります。
公式な[MongoDBユーザーグループ](http://groups.google.com/group/mongodb-user)は質問を尋ねるには最適な場所です。

NoSQLは必要性によってのみ生み出されただけではなく、新しいアプローチへの興味深い試みでもあります。
有難いことにこれらの分野は常に進展しており、私たちが時々失敗し、挑戦し続けなければ成功はありえません。
思うにこれは、私たちがプロとして活躍するための賢明な方法となるでしょう。

<!--

git diff 5c9cc6ca2df7569860c25502710f861105e00bee^..master --word-diff
次 ## Chapter 3 - Mastering Find

-->
