% MongoDBの薄い本
% Karl Seguin 著 / Tsukasa Hamano 訳

## この本について ##

### ライセンス ###
MongoDBの薄い本はAttribution-NonCommercial 3.0 Unportedに基づいてライセンスされています。*あなたはこの本の為にお金を支払う必要はありません。*

この本を複製、改変、展示する事は基本的に自由です。しかし、この本は常に私(カール・セガン)に帰属するように求めます。そして私はこれを商用目的で使用する事はありません。

以下にライセンスの全文があります:

<http://creativecommons.org/licenses/by-nc/3.0/legalcode>

### 著者について ###
カール・セガンは幅広い経験と技術を持った開発者です。 彼は.Netのエキスパートであると同時にRubyの開発者です。彼はOSSプロジェクトのセミアクティブな貢献者であり、テクニカルライターや時々講演を行っています。MongoDBに関して、彼はC#のMongoDBライブラリNoRMの主要な貢献者であり、インタラクティブ・チュートリアル[mongly](http://mongly.com)や[Mongo Web Admin](https://github.com/karlseguin/Mongo-Web-Admin)を書きました。彼のカジュアルなゲーム開発者の為のサービス、[mogade.com](http://mogade.com/)はMongoDBで稼動しています。

カールは過去に[Redisの薄い本](http://openmymind.net/2012/1/23/The-Little-Redis-Book/)も書いています。

彼のブログは<http://openmymind.net>、つぶやきは[@karlseguin](http://twitter.com/karlseguin)で見つかります。

### 謝辞 ###
[Perry Neal](http://twitter.com/perryneal)が私に彼の目と意見と情熱を貸してくれた事に感謝します。ありがとう。

### 最新バージョン ###
この本の最新のソースはこちら:

<http://github.com/karlseguin/the-little-mongodb-book>

\clearpage

## 序章 ##
 > この章が短い事は私の誤りではありません、MongoDBを学ぶ事はとても簡単です。

しばしば、技術は激しい速度で変化していると言われます。それは新しい技術と技術手法が公開され続けているという点で真実ですが、私の見解ではプログラマによって利用される基礎的な技術の変化はかなり遅いと考えています。
One could spend years learning little yet remain relevant.
注目すべき所は確立した技術が置きかえられる速度です。気がつくと、長い歴史を持つ技術がまるで一晩で開発者の関心の転移に脅かされているようです。

既に確立されているリレーショナルデーターベースに反発して発展してきたNoSQLはこの様な急転換の典型的な事例です。5年後、またはNoSQLが十分普及したいつの日か、昔のWebはRDBMSで動いていたと言われる様になるかもしれません。

たとえこれらの技術が一晩で推移したとしても、実際的な実務でこれらが受け入れられるには何年もがかかります。初期の情熱は比較的小規模な会社や開発者によって突き動かされます。新しい技術は彼らのような人々の挑戦によってゆっくりと普及しソリューションや教育環境が洗練されていきます。念の為、NoSQLは昔ながらのストレージソリューションを置き換える手段ではないという事については大部分は真実です。しかしある特定の分野では従来のものに優る価値を必要とします。

何よりもまず初めに、NoSQLが何を意味しているのかを説明すべきでしょう。それは人によって異なる意味を持つ広義の用語です。私は個人的に、それをデータストレージの役割を果たすシステムという意味で使用しています。言い換えれば、(私にとっての)NoSQLはあなたが執着する単一のシステムに必ずしも責任を持つようなものではありません。歴史的に見て、リレーショナルデータベースベンダーはどんなサイズにも適応する万能なソリューションとしてソフトウェアを位置づけてきました。NoSQLスタックはMySQLといったリレーショナルデータベースの様に利用する事も出来るでしょうが、NoSQLは与えられた仕事を達成する為の最適なツールとしてより小さい単位の役割に向かう傾向があります。そして、Redisもまた参照性能というシステムの特定部位に執着し、同じようにHadoopもデータ処理に集中的です。簡単に言うと、NoSQLはオープンであり、既存のものの代替や付加的なパターンを意識し、データを管理する為のツールです。

あなたはMongoDBが多くの事に適応する事に驚くかもしれません。Mongoはドキュメント志向データベースとしてよりNoSQLソリューションに汎用化されています。それはリレーショナルデータベースの代替の様に見られるでしょうが、リレーショナルデータベースと比較すると、もっと専門化したNoSQLソリューションにおいて恩恵を得ることが出来ます。MongoDBには利点と欠点がありますのでそれには後ほどこの本の中で触れます。

もう気がついているかもしれませんが、私たちはMongoDBという用語と同じ意味でMongoと呼ぶことがあります。

## はじめよう ##
この本の大部分はMongoDBの機能面に注目します。その為に私たちはMongoDBシェルを利用します。MongoDBドライバを利用するようになるまで、MongoDBシェルは学習に役立つだけでなく、便利な管理ツールとなるでしょう。

MongoDBについてまず最初に知るべきことを取り上げます: それはドライバです。MongoDBは各種プログラミング言語向けに[数多くの公式ドライバ](http://www.mongodb.org/display/DOCS/Drivers)が用意されています。これらのドライバは恐らくあなたがすでに慣れ親しんでいる各種データーベースのドライバと似たようなものだと考えて良いでしょう。これらのドライバに加えて、開発コミュニティでは更にプログラミング言語/フレームワーク用のライブラリが開発されています。例えば、[NoRM](https://github.com/atheken/NoRM)はLINQを実装したC#のライブラリで、[MongoMapper](https://github.com/jnunemaker/mongomapper)はActiveRecordと親和性の高いRubyライブラリです。プログラムから直接MongoDBのコアドライバを利用するか、他の高級なライブラリを選択するかはあなた次第です。何故公式ドライバとコミュニティライブラリの両方が存在するのかについてMongoDBに不慣れな多くの人に混乱があるようなので説明しておきます。前者はMongoDBの中核的な通信と接続性に、後者はよりプログラミング言語や特定のフレームワークの実装に集中しています。

あなたがこれを読み終えると、あなたがMongoDBを楽しむようになり、I encourage you to play with MongoDB to replicate what I demonstrate as well as to explore questions that might come up on your own.
MongoDBの準備と実行は簡単です、今から数分の時間をかけてセットアップしてみましょう。

 1. [公式ダウンロードページ](http://www.mongodb.org/downloads)へ進み、一番上の行からOSを選択してバイナリを手に入れましょう(安定バージョンを推奨)。開発目的であれば32ビット64ビットのどちらを選んでも構いません。

 2. アーカイブを適当な場所に展開し、`bin`サブフォルダへ移動します。まだ何も実行しないこと、`mongod`がサーバープロセスであり、`mongo`がクライアントシェルであることは知っておいて下さい。その2つはこれから私たちが最も時間を費やす実行ファイルです。

 3. `bin`サブフォルダの中に`mongodb.config`という名前で新しいテキストファイルを作成します

 4. `mongodb.config`に以下の1行を追記します:

        dbpath=PATH_TO_WHERE_YOU_WANT_TO_STORE_YOUR_DATABASE_FILES

    例えば、Windowsでは`dbpath=c:\mongodb\data`を指定し、Linuxでは`dbpath=/etc/mongodb/data`と指定します。

 5. 指定した`dbpath`を作成する

 6. mongodを`--config /path/to/your/mongodb.config`パラメーターを付けて起動します。

Windowsユーザーの為の例を示すと、もしダウンロードファイルを`c:\mongodb\`に展開したのなら`c:\mongodb\bin\mongodb.config`に`dbpath=c:\mongodb\data\`を指定すると、`c:\mongodb\data\`が作成されます。次に、コマンドプロンプトから `c:\mongodb\bin\mongod --config c:\mongodb\bin\mongodb.config`を実行して`mongod`を起動します。

無駄を少なくする為に、ご自由に`bin`フォルダをパスに追加して下さい。MacOSXとLinuxユーザーはほとんど同じやり方に従うことが出来ます。あなたがすべきことはパスを変更することくらいです。

うまくいけば今あなたはMonogDBを実行しているでしょう。もしエラーが起こったらならメッセージを注意深く読んで下さい。サーバーは何がおかしいのかを丁寧に説明してくれます。

あなたは`mongo`(*d*は付かない)を起動し、実行中のサーバーのシェルに接続する事が出来ます。全てが動作しているか確認するために`db.version()`と入力してみて下さい、うまくいっていればインストールされているバージョンを確認することが出来るでしょう。

\clearpage

## 1章 - 基礎 ##
MongoDBの動作の基本的な機構を知ることからはじめましょう。当然これはMongoDBの核心を理解することです。しかしこれはMongoDBについての高レベルな質問答えを見つけ出す為にも役立ちます。

最初に、私たちは6つの概念を理解する必要があります。

1. MongoDBはあなたが既に慣れ親しんでいる`データベース`と同じ概念を持っています(あるいはOracleでいうところのスキーマ)。MongoDBインスタンスの中には0個以上のデータベースを持つことが出来、それぞれは高レベルコンテナの様に作用します。

2. データベースは0個以上の`コレクション`を持つことが出来ます。コレクションは従来の`テーブル`とほぼ共通しているので、2つが同じものだと思っても支障は無いでしょう。

3. コレクションは0個以上の`ドキュメント`を作成できます。先ほどと同様にドキュメントを`行`と思って構いません。

4. ドキュメントは1つ以上の`フィールド`を作成できます。あなたは恐らくこれを`列`に似ていると推測できるでしょう。

5. MongoDBでの`インデックス`機能はRDBMSのものとよく似ています。

6. `カーソル`はこれまでの5つの概念とは異なりますが、とても重要で見落とされがちですので詳しく説明する必要があると思います。カーソルについて理解べき重要な事は、カウントやスキップの様な操作は実際にデータを引き出すこと無くMongoDBにデータを問い合わせた際に返却されるカーソルに対して行われるいう事です。

要点をまとめると、MongoDBは`データベース`を作成し、その中には`コレクション`を含みます。`コレクション`は`ドキュメント`を作成します。それぞれの`ドキュメント`は`フィールド`を作成します。`コレクション`は`インデックス化`可能であり、これは参照やソートの性能を改善します。最後に、MongoDBからデータを取得する際、`カーソル`を経由して操作を行います。これは実際に実行する際に必要不可欠なものです。

なぜ新しい専門用語を利用するのか不思議に思うかもしれません(コレクションとテーブル、ドキュメントと行、フィールドと列)。物事を複雑にするだけでしょうか?これらの概念がリレーショナルデータベースの機能と良く似ているという点でその通りですが、これらは全く同じではありません。主要な違いは、リレーショナルデーターベースが`テーブル`のレベルに`列`を定義しているのに対し、ドキュメント志向データベースは`ドキュメント`のレベルに`フィールド`を定義している事です。`コレクション`の中の`ドキュメント`はそれ自身の独自の`フィールド`を持つことが出来ると言えます。という訳で、`コレクション`は`テーブル`に比べ、より使い易くいコンテナとなり、さらに`ドキュメント`は`行`に比べてより多くの情報を持つようになります。

これを理解することは重要ですが、もしこれをまだ完全に理解出来ていなくても心配することはありません。この本当の意味を確かめる為にはまだもう少し説明が必要でしょう。突き詰めていくとコレクションの中に何が入るかが厳密ではない事が要点です(スキーマレスの事)。フィールドは特定のドキュメントに対して追従します。先の章で利点と欠点に気がつくでしょう。

さあハンズオンをはじめましょう。まだ動かしていないのなら、どうぞ`mongod`サーバーとmongoシェルを起動して下さい。シェルはJavaScriptが動きます。`help`や`exit`の様な、幾つかのグローバルコマンドを実行することが出来ます。例えば、`db.help()`や`db.stats()`といったコマンドは、現在のデータベース`db`オブジェクトに対して実行します。`db.unicorns.help()`や`db.unicorns.count()`といったコマンドは、`db.COLLECTION_NAME`オブジェクトの様に、指定したそれぞれのコレクションに対して実行を行います。

どうぞ、`db.help()`と入力してみて下さい。`db`オブジェクトに対して実行可能なコマンド一覧を得ることが出来るでしょう。

余談ですが、あなたが丸カッコ`()`を含めずにメソッドを実行した場合、メソッドの実行ではなくメソッドの本体が表示されます。なぜならこれはJavaScriptシェルだからです。あなたが最初にこれをやった時、`function (...){`という応答が返ってきても驚かないように、この事に触れておきました。たとえば、丸カッコ無しで`db.help`と入力すると`help`メソッドの内部実装を見ることが出来ます。

私たちは最初にグローバルな`use`メソッドを利用してデータベースを切り替えます。どうぞ`use learn`と入力してみて下さい。そのデータベースが実際に存在していなくても構いません。最初のコレクションを`learn`に作成しましょう。今あなたはデータベースの中にいて、`db.getCollectionNames()`という様なデータベースコマンドを発行できます。これを実行すると、恐らく空の配列(`[ ]`)が返ってくるでしょう。コレクションはスキーマレスですので、それらを明確に作成する必要はありません。私たちは、単純にドキュメントをコレクションに作成する事が出来ます。それでは`insert`コマンドを使ってドキュメントにコレクションを挿入してみましょう。

	db.unicorns.insert({name: 'Aurora', gender: 'f', weight: 450})

上記のコマンドは一つの引数を受け取り`unicorns`コレクションに対して`insert`を行います。MongoDBの内部ではシリアライズされたJSONフォーマットを利用します。今、`db.getCollectionNames()`を実行すると、実際には2つのコレクション`unicorns`と`system.indexes`を確認できます。`system.indexes`はデータベースのインデックス情報が格納され、データベース毎にひとつ作成されます。

これで、`unicorns`に対し`find`コマンドを使用してドキュメントのリストを取得出来るようになりました。

	db.unicorns.find()

あなたが指定したデータには`_id`フィールドが追加されていることに注目して下さい。全てのドキュメントはユニークな`_id`フィールドを持たなければなりません。あなたは、MongoDBに生成させるかこのオブジェクトIDを自分自身で生成する事になります。先程`system.indexes`コレクションが作成された理由は、デフォルトで`_id`フィールドはインデックス化されているからであると説明できます。あなたは以下のようにして`system.indexes`を参照できます:

	db.system.indexes.find()

あなたはインデックスを含むフィールドに対して作成されたデータベースやコレクションのインデックス名を確認することが出来ます。

スキーマレスコレクションの話に戻りましょう。`unicorns`以下のような完全に異なるドキュメントを入れてみます:

	db.unicorns.insert({name: 'Leto', gender: 'm', home: 'Arrakeen', worm: false})

再度`find`を利用してドキュメントを表示してみて下さい。MongoDBの興味深い振る舞いについて前に少しだけ話しました、何故従来の技術うまく適応しなかったのかのかが解り始めてたのではないかと思います。

### セレクターの習得 ###
次の話題に進む前に、先程説明した6つの概念に加え、MongoDBの実用面でしっかりと理解すべきことがあります。それはクエリーセレクターです。MongoDBのクエリーセレクターはSQL構文の`where`節によく似ています。そういうわけで、これはドキュメントを見つけ出したり、数えたり、更新したり、削除したりする際に使用します。セレクターはJSONオブジェクトです。最も単純な`{}`は全てのドキュメントにマッチします(`null`も同じです)。もし女性ドキュメントを見つけたい場合、`{gender:'f'}`と指定します。

セレクターについて掘り下げていく前に、実演の為の幾つかのデータをセットアップしましょう。まず最初に、これまでに`unicorns`コレクションに入れたドキュメントを`db.unicorns.remove()`を実行して削除します(セレクターを指定していないので、全てのドキュメントが削除されます)。さて、以下を実行して実演に必要なデータを挿入しましょう(コピペ推奨):

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

データが入ったのでこれでセレクターを習得できます。`{field: value}`は`field`というフィールドが`value`と等しいドキュメントを検索します。`{field1: value1, field2: value2}`は`and`式で検索します。`$lt`、 `$lte`、 `$gt`、 `$gte`、 `$ne`はそれぞれ、未満、以下、より多い、以上、非等価、を意味する特別な演算子です。例えば、性別が男で体重が700ポンドより大きいユニコーンを探すにはこのようにします:

	db.unicorns.find({gender: 'm', weight: {$gt: 700}})
	//もしくは、(あまり良くないですが、デモの為に)
	db.unicorns.find({gender: {$ne: 'f'}, weight: {$gte: 701}})

`$exists`演算子はフィールドの存在や欠如のマッチに利用します。例えば:

	db.unicorns.find({vampires: {$exists: false}})

ひとつのドキュメントが返ってくるはずです。ANDではなくORを利用したい場合、`$or`演算子を利用して、ORをとりたい式を配列で指定します。

	db.unicorns.find({gender: 'f', $or: [{loves: 'apple'},
                                         {loves: 'orange'},
                                         {weight: {$lt: 500}}]})

上記は全ての女性のユニコーンの中から、りんごかオレンジが好き、もしくは体重が500ポンド未満の条件で検索します。

最後に示した例にはとても素敵なものがあります。すでに知っていると思いますが`loves`フィールドは配列です。MongoDBはファーストクラスオブジェクトとしての配列をサポートしています。これはとんでもなく便利な機能です。一度これを使ってしまうと、これ無しでは生活できなくなる恐れがあります。何よりも興味深いのは配列の値に基づいて簡単に選択できることです。`{loves: 'watermelon'}` は`loves`の値に`watermelon`を持つドキュメントを返します。

これまでに見てきた他に、演算子はまだまだあります。最も柔軟な`$where`は指定したJavaScriptをサーバー上で実行します。MongoDBのWebサイトの[Advanced Queries](http://www.mongodb.org/display/DOCS/Advanced+Queries#AdvancedQueries)の項に全てが記載されています。これまでに紹介してきたものはあなたが使い始めるのに必要な基本です。もっと使いこなせるようになるには多くの時間がかかるでしょう。

これまでセレクターは`find`コマンドで利用できることを見てきました。これらは以前ちょっとだけ利用した`remove`コマンドやまだ使っていない`count`コマンド、後で出てくる`update`コマンドでも利用できます。

`ObjectId`はMongoDBにが生成した`_id`フィールドを選択するために利用します:

	db.unicorns.find({_id: ObjectId("TheObjectId")})

### 章のまとめ ###
We haven't looked at the `update` command yet, or some of the fancier things we can do with `find`. However, we did get MongoDB up and running, looked briefly at the `insert` and `remove` commands (there isn't much more than what we've seen). We also introduced `find` and saw what MongoDB `selectors` were all about. We've had a good start and laid a solid foundation for things to come. Believe it or not, you actually know most of what there is to know about MongoDB - it really is meant to be quick to learn and easy to use. I strongly urge you to play with your local copy before moving on. Insert different documents, possibly in new collections, and get familiar with different selectors. Use `find`, `count` and `remove`. After a few tries on your own, things that might have seemed awkward at first will hopefully fall into place.

\clearpage

## 2章 - 更新 ##
In chapter 1 we introduced three of the four CRUD (create, read, update and delete) operations. This chapter is dedicated to the one we skipped over: `update`. `Update` has a few surprising behaviors, which is why we dedicate a chapter to it.

### Update: Replace Versus $set ###
In its simplest form, `update` takes 2 arguments: the selector (where) to use and what field to update with. If Roooooodles had gained a bit of weight, we could execute:

	db.unicorns.update({name: 'Roooooodles'}, {weight: 590})

(if you've played with your `unicorns` collection and it doesn't have the original data anymore, go ahead and `remove` all documents and re-insert from the code in chapter 1.)

If this was real code, you'd probably update your records by `_id`, but since I don't know what `_id` MongoDB generated for you, we'll stick to `names`.  Now, if we look at the updated record:

	db.unicorns.find({name: 'Roooooodles'})

You should discover `updates` first surprise. No document is found because the second parameter we supply is used to **replace** the original. In other words, the `update` found a document by `name` and replaced the entire document with the new document (the 2nd parameter). This is different than how SQL's `update` command works. In some situations, this is ideal and can be leveraged for some truly dynamic updates. However, when all you want to do is change the value of one, or a few fields, you are best to use MongoDB's `$set` modifier:

	db.unicorns.update({weight: 590}, {$set: {name: 'Roooooodles', dob: new Date(1979, 7, 18, 18, 44), loves: ['apple'], gender: 'm', vampires: 99}})

This'll reset the lost fields. It won't overwrite the new `weight` since we didn't specify it. Now if we execute:

	db.unicorns.find({name: 'Roooooodles'})

We get the expected result. Therefore, the correct way to have updated the weight in the first place is:

	db.unicorns.update({name: 'Roooooodles'}, {$set: {weight: 590}})

### Update Modifiers ###
In addition to `$set`, we can leverage other modifiers to do some nifty things. All of these update modifiers work on fields - so your entire document won't be wiped out. For example, the `$inc` modifier is used to increment a field by a certain positive or negative amount. For example, if Pilot was incorrectly awarded a couple vampire kills, we could correct the mistake by executing:

	db.unicorns.update({name: 'Pilot'}, {$inc: {vampires: -2}})

If Aurora suddenly developed a sweet tooth, we could add a value to her `loves` field via the `$push` modifier:

	db.unicorns.update({name: 'Aurora'}, {$push: {loves: 'sugar'}})

The [Updating](http://www.mongodb.org/display/DOCS/Updating) section of the MongoDB website has more information on the other available update modifiers.

### Upserts ###
One of `updates` more pleasant surprises is that it fully supports `upserts`. An `upsert` updates the document if found or inserts it if not. Upserts are handy to have in certain situations and, when you run into one, you'll know it. To enable upserting we set a third parameter to `true`.

A mundane example is a hit counter for a website. If we wanted to keep an aggregate count in real time, we'd have to see if the record already existed for the page, and based on that decide to run an update or insert. With the third parameter omitted (or set to false), executing the following won't do anything:

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}});
	db.hits.find();

However, if we enable upserts, the results are quite different:

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}}, true);
	db.hits.find();

Since no documents exists with a field `page` equal to `unicorns`, a new document is inserted. If we execute it a second time, the existing document is updated and `hits` is incremented to 2.

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}}, true);
	db.hits.find();

### Multiple Updates ###
The final surprise `update` has to offer is that, by default, it'll update a single document. So far, for the examples we've looked at, this might seem logical. However, if you executed something like:

	db.unicorns.update({}, {$set: {vaccinated: true }});
	db.unicorns.find({vaccinated: true});

You'd likely expect to find all of your precious unicorns to be vaccinated. To get the behavior you desire, a fourth parameter must be set to true:

	db.unicorns.update({}, {$set: {vaccinated: true }}, false, true);
	db.unicorns.find({vaccinated: true});

### In This Chapter ###
This chapter concluded our introduction to the basic CRUD operations available against a collection. We looked at `update` in detail and observed three interesting behaviors. First, unlike an SQL update, MongoDB's `update` replaces the actual document. Because of this the `$set` modifier is quite useful. Secondly, `update` supports an intuitive `upsert` which is particularly useful when paired with the `$inc` modifier. Finally, by default, `update` only updates the first found document.

Do remember that we are looking at MongoDB from the point of view of its shell. The driver and library you use could alter these default behaviors or expose a different API. For example, the Ruby driver merges the last two parameters into a single hash: `{:upsert => false, :multi => false}`. Similarly, the PHP driver, merges the last two parameters into an array: `array('upsert' => false, 'multiple' => false)`. 

\clearpage

## 3章 - 検索の習得 ##
Chapter 1 provided a superficial look at the `find` command. There's more to `find` than understanding `selectors` though. We already mentioned that the result from `find` is a `cursor`. We'll now look at exactly what this means in more detail.

### Field Selection ###
Before we jump into `cursors`, you should know that `find` takes a second optional parameter. This parameter is the list of fields we want to retrieve. For example, we can get all of the unicorns names by executing:

	db.unicorns.find(null, {name: 1});

By default, the `_id` field is always returned. We can explicitly exclude it by specifying `{name:1, _id: 0}`.

Aside from the `_id` field, you cannot mix and match inclusion and exclusion. If you think about it, that actually makes sense. You either want to select or exclude one or more fields explicitly.

### Ordering ###
A few times now I've mentioned that `find` returns a cursor whose execution is delayed until needed. However, what you've no doubt observed from the shell is that `find` executes immediately. This is a behavior of the shell only. We can observe the true behavior of `cursors` by looking at one of the methods we can chain to `find`. The first that we'll look at is `sort`. `sort` works a lot like the field selection from the previous section. We specify the fields we want to sort on, using 1 for ascending and -1 for descending. For example:

	//heaviest unicorns first
	db.unicorns.find().sort({weight: -1})

	//by vampire name then vampire kills:
	db.unicorns.find().sort({name: 1, vampires: -1})

Like with a relational database, MongoDB can use an index for sorting. We'll look at indexes in more detail later on. However, you should know that MongoDB limits the size of your sort without an index. That is, if you try to sort a large result set which can't use an index, you'll get an error. Some people see this as a limitation. In truth, I wish more databases had the capability to refuse to run unoptimized queries. (I won't turn every MongoDB drawback into a positive, but I've seen enough poorly optimized databases that I sincerely wish they had a strict-mode.)

### Paging ###
Paging results can be accomplished via the `limit` and `skip` cursor methods. To get the second and third heaviest unicorn, we could do:

	db.unicorns.find().sort({weight: -1}).limit(2).skip(1)

Using `limit` in conjunction with `sort`, is a good way to avoid running into problems when sorting on non-indexed fields.

### Count ###
The shell makes it possible to execute a `count` directly on a collection, such as:

	db.unicorns.count({vampires: {$gt: 50}})

In reality, `count` is actually a `cursor` method, the shell simply provides a shortcut. Drivers which don't provide such a shortcut need to be executed like this (which will also work in the shell):

	db.unicorns.find({vampires: {$gt: 50}}).count()

### In This Chapter ###
Using `find` and `cursors` is a straightforward proposition. There are a few additional commands that we'll either cover in later chapters or which only serve edge cases, but, by now, you should be getting pretty comfortable working in the mongo shell and understanding the fundamentals of MongoDB.

\clearpage

## 4章 - データモデリング ##
Let's shift gears and have a more abstract conversation about MongoDB. Explaining a few new terms and some new syntax is a trivial task. Having a conversation about modeling with a new paradigm isn't as easy. The truth is that most of us are still finding out what works and what doesn't when it comes to modeling with these new technologies. It's a conversation we can start having, but ultimately you'll have to practice and learn on real code.

Compared to most NoSQL solutions, document-oriented databases are probably the least different, compared to relational databases, when it comes to modeling. The differences which exist are subtle but that doesn't mean they aren't important.

### No Joins ###
The first and most fundamental difference that you'll need to get comfortable with is MongoDB's lack of joins. I don't know the specific reason why some type of join syntax isn't supported in MongoDB, but I do know that joins are generally seen as non-scalable. That is, once you start to horizontally split your data, you end up performing your joins on the client (the application server) anyways. Regardless of the reasons, the fact remains that data *is* relational, and MongoDB doesn't support joins.

Without knowing anything else, to live in a join-less world, we have to do joins ourselves within our application's code. Essentially we need to issue a second query to `find` the relevant data. Setting our data up isn't any different than declaring a foreign key in a relational database. Let's give a little less focus to our beautiful `unicorns` and a bit more time to our `employees`. The first thing we'll do is create an employee (I'm providing an explicit `_id` so that we can build coherent examples)

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d730"), name: 'Leto'})

Now let's add a couple employees and set their manager as `Leto`:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d731"), name: 'Duncan', manager: ObjectId("4d85c7039ab0fd70a117d730")});
	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d732"), name: 'Moneo', manager: ObjectId("4d85c7039ab0fd70a117d730")});


(It's worth repeating that the `_id` can be any unique value. Since you'd likely use an `ObjectId` in real life, we'll use them here as well.)

Of course, to find all of Leto's employees, one simply executes:

	db.employees.find({manager: ObjectId("4d85c7039ab0fd70a117d730")})

There's nothing magical here. In the worst cases, most of the time, the lack of join will merely require an extra query (likely indexed).

#### Arrays and Embedded Documents ####
Just because MongoDB doesn't have joins doesn't mean it doesn't have a few tricks up its sleeve. Remember when we quickly saw that MongoDB supports arrays as first class objects of a document? It turns out that this is incredibly handy when dealing with many-to-one or many-to-many relationships. As a simple example, if an employee could have two managers, we could simply store these in an array:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d733"), name: 'Siona', manager: [ObjectId("4d85c7039ab0fd70a117d730"), ObjectId("4d85c7039ab0fd70a117d732")] })

Of particular interest is that, for some documents, `manager` can be a scalar value, while for others it can be an array. Our original `find` query will work for both:

	db.employees.find({manager: ObjectId("4d85c7039ab0fd70a117d730")})

You'll quickly find that arrays of values are much more convenient to deal with than many-to-many join-tables.

Besides arrays, MongoDB also supports embedded documents. Go ahead and try inserting a document with a nested document, such as:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d734"), name: 'Ghanima', family: {mother: 'Chani', father: 'Paul', brother: ObjectId("4d85c7039ab0fd70a117d730")}})

In case you are wondering, embedded documents can be queried using a dot-notation:

	db.employees.find({'family.mother': 'Chani'})

We'll briefly talk about where embedded documents fit and how you should use them.

#### DBRef ####
MongoDB supports something known as `DBRef` which is a convention many drivers support. When a driver encounters a `DBRef` it can automatically pull the referenced document. A `DBRef` includes the collection and id of the referenced document. It generally serves a pretty specific purpose: when documents from the same collection might reference documents from a different collection from each other. That is, the `DBRef` for document1 might point to a document in `managers` whereas the `DBRef` for document2 might point to a document in `employees`.


#### Denormalization ####
Yet another alternative to using joins is to denormalize your data. Historically, denormalization was reserved for performance-sensitive code, or when data should be snapshotted (like in an audit log). However, with the ever-growing popularity of NoSQL, many of which don't have joins, denormalization as part of normal modeling is becoming increasingly common. This doesn't mean you should duplicate every piece of information in every document. However, rather than letting fear of duplicate data drive your design decisions, consider modeling your data based on what information belongs to what document.

For example, say you are writing a forum application. The traditional way to associate a specific `user` with a `post` is via a `userid` column within `posts`. With such a model, you can't display `posts` without retrieving (joining to) `users`. A possible alternative is simply to store the `name` as well as the `userid` with each `post`. You could even do so with an embedded document, like `user: {id: ObjectId('Something'), name: 'Leto'}`. Yes, if you let users change their name, you'll have to update each document (which is 1 extra query).

Adjusting to this kind of approach won't come easy to some. In a lot of cases it won't even make sense to do this. Don't be afraid to experiment with this approach though. It's not only suitable in some circumstances, but it can also be the right way to do it.

#### Which Should You Choose? ####
Arrays of ids are always a useful strategy when dealing with one-to-many or many-to-many scenarios. It's probably safe to say that `DBRef` aren't used very often, though you can certainly experiment and play with them. That generally leaves new developers unsure about using embedded documents versus doing manual referencing.

First, you should know that an individual document is currently limited to 4 megabytes in size. Knowing that documents have a size limit, though quite generous, gives you some idea of how they are intended to be used. At this point, it seems like most developers lean heavily on manual references for most of their relationships. Embedded documents are frequently leveraged, but mostly for small pieces of data which we want to always pull with the parent document. A real world example I've used is to store an `accounts` document with each user, something like:

	db.users.insert({name: 'leto', email: 'leto@dune.gov', account: {allowed_gholas: 5, spice_ration: 10}})

That doesn't mean you should underestimate the power of embedded documents or write them off as something of minor utility. Having your data model map directly to your objects makes things a lot simpler and often does remove the need to join. This is especially true when you consider that MongoDB lets you query and index fields of an embedded document.

### Few or Many Collections ###
Given that collections don't enforce any schema, it's entirely possible to build a system using a single collection with a mismatch of documents.  From what I've seen, most MongoDB systems are laid out similarly to what you'd find in a relational system. In other words, if it would be a table in a relational database, it'll likely be a collection in MongoDB (many-to-many join tables being an important exception).

The conversation gets even more interesting when you consider embedded documents. The example that frequently comes up is a blog. Should you have a `posts` collection and a `comments` collection, or should each `post` have an array of `comments` embedded within it. Setting aside the 4MB limit for the time being (all of Hamlet is less than 200KB, just how popular is your blog?), most developers still prefer to separate things out. It's simply cleaner and more explicit.

There's no hard rule (well, aside from 4MB). Play with different approaches and you'll get a sense of what does and does not feel right.

### In This Chapter ###
Our goal in this chapter was to provide some helpful guidelines for modeling your data in MongoDB. A starting point if you will. Modeling in a document-oriented system is different, but not too different than a relational world. You have a bit more flexibility and one constraint, but for a new system, things tend to fit quite nicely. The only way you can go wrong is by not trying.

\clearpage

## 5章 - When To Use MongoDB ##
By now you should have a good enough understanding of MongoDB to have a feel for where and how it might fit into your existing system. There are enough new and competing storage technologies that it's easy to get overwhelmed by all of the choices.

For me, the most important lesson, which has nothing to do with MongoDB, is that you no longer have to rely on a single solution for dealing with your data. No doubt, a single solution has obvious advantages and for a lot projects, possibly even most, a single solution is the sensible approach. The idea isn't that you must use different technologies, but rather that you can. Only you know whether the benefits of introducing a new solution outweigh the costs.

With that said, I'm hopeful that what you've seen so far has made you see MongoDB as a general solution. It's been mentioned a couple times that document-oriented databases share a lot in common with relational databases. Therefore, rather than tiptoeing around it, let's simply state that MongoDB should be seen as a direct alternative to relational databases. Where one might see Lucene as enhancing a relational database with full text indexing, or Redis as a persistent key-value store, MongoDB is a central repository for your data.

Notice that I didn't call MongoDB a *replacement* for relational databases, but rather an *alternative*. It's a tool that can do what a lot of other tools can do. Some of it MongoDB does better, some of it MongoDB does worse. Let's dissect things a little further.

### Schema-less ###
An oft-touted benefit of document-oriented database is that they are schema-less. This makes them much more flexible than traditional database tables. I agree that schema-less is a nice feature, but not for the main reason most people mention.

People talk about schema-less as though you'll suddenly start storing a crazy mismatch of data. There are domains and data sets which can really be a pain to model using relational databases, but I see those as edge cases. Schema-less is cool, but most of your data is going to be highly structured. It's true that having an occasional mismatch can be handy, especially when you introduce new features, but in reality it's nothing a nullable column probably wouldn't solve just as well.

For me, the real benefit of schema-less design is the lack of setup and the reduced friction with OOP. This is particularly true when you're working with a static language. I've worked with MongoDB in both C# and Ruby, and the difference is striking. Ruby's dynamism and its popular ActiveRecord implementations already reduce much of the object-relational impedance mismatch. That isn't to say MongoDB isn't a good match for Ruby, it really is. Rather, I think most Ruby developers would see MongoDB as an incremental improvement, whereas C# or Java developers would see a fundamental shift in how they interact with their data.

Think about it from the perspective of a driver developer. You want to save an object? Serialize it to JSON (technically BSON, but close enough) and send it to MongoDB. There is no property mapping or type mapping. This straightforwardness definitely flows to you, the end developer.

### Writes ###
One area where MongoDB can fit a specialized role is in logging. There are two aspects of MongoDB which make writes quite fast. First, you can send a write command and have it return immediately without waiting for it to actually write. Secondly, with the introduction of journaling in 1.8, and enhancements made in 2.0, you can control the write behavior with respect to data durability. These settings, in addition to specifying how many servers should get your data before being considered successful, are configurable per-write, giving you a great level of control over write performance and data durability.

In addition to these performance factors, log data is one of those data sets which can often take advantage of schema-less collections. Finally, MongoDB has something called a [capped collection](http://www.mongodb.org/display/DOCS/Capped+Collections). So far, all of the implicitly created collections we've created are just normal collections. We can create a capped collection by using the `db.createCollection` command and flagging it as capped:

	//limit our capped collection to 1 megabyte
	db.createCollection('logs', {capped: true, size: 1048576})

When our capped collection reaches its 1MB limit, old documents are automatically purged. A limit on the number of documents, rather than the size, can be set using `max`. Capped collections have some interesting properties. For example, you can update a document but it can't grow in size. Also, the insertion order is preserved, so you don't need to add an extra index to get proper time-based sorting.

This is a good place to point out that if you want to know whether your write encountered any errors (as opposed to the default fire-and-forget), you simply issue a follow-up command: `db.getLastError()`. Most drivers encapsulate this as a *safe write*, say by specifying `{:safe => true}` as a second parameter to `insert`.

### Durability ###
Prior to version 1.8, MongoDB didn't have single-server durability. That is, a server crash would likely result in lost data. The solution had always been to run MongoDB in a multi-server setup (MongoDB supports replication). One of the major features added to 1.8 was journaling. To enable it add a new line with `journal=true` to the `mongodb.config` file we created when we first setup MongoDB (and restart your server if you want it enabled right away). You probably want journaling enabled (it'll be a default in a future release). Although, in some circumstances the extra throughput you get from disabling journaling might be a risk you are willing to take. (It's worth pointing out that some types of applications can easily afford to lose data).

Durability is only mentioned here because a lot has been made around MongoDB's lack of single-server durability. This'll likely show up in Google searches for some time to come. Information you find about this missing feature is simply out of date.

### Full Text Search ###
True full text search capability is something that'll hopefully come to MongoDB in a future release. With its support for arrays, basic full text search is pretty easy to implement. For something more powerful, you'll need to rely on a solution such as Lucene/Solr. Of course, this is also true of many relational databases.

### Transactions ###
MongoDB doesn't have transactions. It has two alternatives, one which is great but with limited use, and the other that is a cumbersome but flexible.

The first is its many atomic operations. These are great, so long as they actually address your problem. We already saw some of the simpler ones, like `$inc` and `$set`. There are also commands like `findAndModify` which can update or delete a document and return it atomically.

The second, when atomic operations aren't enough, is to fall back to a two-phase commit. A two-phase commit is to transactions what manual dereferencing is to joins. It's a storage-agnostic solution that you do in code.  Two-phase commits are actually quite popular in the relational world as a way to implement transactions across multiple databases. The MongoDB website [has an example](http://www.mongodb.org/display/DOCS/two-phase+commit) illustrating the most common scenario (a transfer of funds). The general idea is that you store the state of the transaction within the actual document being updated and go through the init-pending-commit/rollback steps manually.

MongoDB's support for nested documents and schema-less design makes two-phase commits slightly less painful, but it still isn't a great process, especially when you are just getting started with it.

### Data Processing ###
MongoDB relies on MapReduce for most data processing jobs. It has some [basic aggregation](http://www.mongodb.org/display/DOCS/Aggregation) capabilities, but for anything serious, you'll want to use MapReduce. In the next chapter we'll look at MapReduce in detail. For now you can think of it as a very powerful and different way to `group by` (which is an understatement). One of MapReduce's strengths is that it can be parallelized for working with large sets of data. However, MongoDB's implementation relies on JavaScript which is single-threaded. The point? For processing of large data, you'll likely need to rely on something else, such as Hadoop. Thankfully, since the two systems really do complement each other, there's a [MongoDB adapter for Hadoop](https://github.com/mongodb/mongo-hadoop).

Of course, parallelizing data processing isn't something relational databases excel at either. There are plans for future versions of MongoDB to be better at handling very large sets of data.

### Geospatial ###
A particularly powerful feature of MongoDB is its support for geospatial indexes. This allows you to store x and y coordinates within documents and then find documents that are `$near` a set of coordinates or `$within` a box or circle. This is a feature best explained via some visual aids, so I invite you to try the [5 minute geospatial interactive tutorial](http://tutorial.mongly.com/geo/index), if you want to learn more.

### Tools and Maturity ###
You probably already know the answer to this, but MongoDB is obviously younger than most relational database systems. This is absolutely something you should consider. How much a factor it plays depends on what you are doing and how you are doing it. Nevertheless, an honest assessment simply can't ignore the fact that MongoDB is younger and the available tooling around isn't great (although the tooling around a lot of very mature relational databases is pretty horrible too!). As an example, the lack of support for base-10 floating point numbers will obviously be a concern (though not necessarily a show-stopper) for systems dealing with money.

On the positive side, drivers exist for a great many languages, the protocol is modern and simple, and development is happening at blinding speeds. MongoDB is in production at enough companies that concerns about maturity, while valid, are quickly becoming a thing of the past.

### In This Chapter ###
The message from this chapter is that MongoDB, in most cases, can replace a relational database. It's much simpler and straightforward; it's faster and generally imposes fewer restrictions on application developers. The lack of transactions can be a legitimate and serious concern. However, when people ask *where does MongoDB sit with respect to the new data storage landscape?* the answer is simple: **right in the middle**.

\clearpage

## 6章 - MapReduce ##
MapReduce is an approach to data processing which has two significant benefits over more traditional solutions. The first, and main, reason it was developed is performance. In theory, MapReduce can be parallelized, allowing very large sets of data to be processed across many cores/CPUs/machines. As we just mentioned, this isn't something MongoDB is currently able to take advantage of. The second benefit of MapReduce is that you get to write real code to do your processing. Compared to what you'd be able to do with SQL, MapReduce code is infinitely richer and lets you push the envelope further before you need to use a more specialized solution.

MapReduce is a pattern that has grown in popularity, and you can make use of it almost anywhere; C#, Ruby, Java, Python and so on all have implementations. I want to warn you that at first this'll seem very different and complicated. Don't get frustrated, take your time and play with it yourself. This is worth understanding whether you are using MongoDB or not.

### A Mix of Theory and Practice ###
MapReduce is a two-step process. First you map and then you reduce. The mapping step transforms the inputted documents and emits a key=>value pair (the key and/or value can be complex). The reduce gets a key and the array of values emitted for that key and produces the final result. We'll look at each step, and the output of each step.

The example that we'll be using is to generate a report of the number of hits, per day, we get on a resource (say a webpage). This is the *hello world* of MapReduce. For our purposes, we'll rely on a `hits` collection with two fields: `resource` and `date`. Our desired output is a breakdown by `resource`, `year`, `month`, `day` and `count`.

Given the following data in `hits`:

	resource     date
	index        Jan 20 2010 4:30
	index        Jan 20 2010 5:30
	about        Jan 20 2010 6:00
	index        Jan 20 2010 7:00
	about        Jan 21 2010 8:00
	about        Jan 21 2010 8:30
	index        Jan 21 2010 8:30
	about        Jan 21 2010 9:00
	index        Jan 21 2010 9:30
	index        Jan 22 2010 5:00

We'd expect the following output:

	resource  year   month   day   count
	index     2010   1       20    3
	about     2010   1       20    1
	about     2010   1       21    3
	index     2010   1       21    2
	index     2010   1       22    1

(The nice thing about this type of approach to analytics is that by storing the output, reports are fast to generate and data growth is controlled (per resource that we track, we'll add at most 1 document per day.)

For the time being, focus on understanding the concept. At the end of this chapter, sample data and code will be given for you to try on your own.

The first thing to do is look at the map function. The goal of map is to make it emit a value which can be reduced. It's possible for map to emit 0 or more times. In our case, it'll always emit once (which is common). Imagine map as looping through each document in hits. For each document we want to emit a key with resource, year, month and day, and a simple value of 1:

	function() {
		var key = {
		    resource: this.resource,
		    year: this.date.getFullYear(),
		    month: this.date.getMonth(),
		    day: this.date.getDate()
		};
		emit(key, {count: 1});
	}

`this` refers to the current document being inspected. Hopefully what'll help make this clear for you is to see what the output of the mapping step is. Using our above data, the complete output would be:

	{resource: 'index', year: 2010, month: 0, day: 20} => [{count: 1}, {count: 1}, {count:1}]
	{resource: 'about', year: 2010, month: 0, day: 20} => [{count: 1}]
	{resource: 'about', year: 2010, month: 0, day: 21} => [{count: 1}, {count: 1}, {count:1}]
	{resource: 'index', year: 2010, month: 0, day: 21} => [{count: 1}, {count: 1}]
	{resource: 'index', year: 2010, month: 0, day: 22} => [{count: 1}]

Understanding this intermediary step is the key to understanding MapReduce. The values from emit are grouped together, as arrays, by key. .NET and Java developers can think of it as being of type `IDictionary<object, IList<object>>` (.NET) or `HashMap<Object, ArrayList>` (Java).

Let's change our map function in some contrived way:

	function() {
		var key = {resource: this.resource, year: this.date.getFullYear(), month: this.date.getMonth(), day: this.date.getDate()};
		if (this.resource == 'index' && this.date.getHours() == 4) {
			emit(key, {count: 5});
		} else {
			emit(key, {count: 1});
		}
	}

The first intermediary output would change to:

	{resource: 'index', year: 2010, month: 0, day: 20} => [{count: 5}, {count: 1}, {count:1}]

Notice how each emit generates a new value which is grouped by our key.

The reduce function takes each of these intermediary results and outputs a final result. Here's what ours looks like:

	function(key, values) {
		var sum = 0;
		values.forEach(function(value) {
			sum += value['count'];
		});
		return {count: sum};
	};

Which would output:

	{resource: 'index', year: 2010, month: 0, day: 20} => {count: 3}
	{resource: 'about', year: 2010, month: 0, day: 20} => {count: 1}
	{resource: 'about', year: 2010, month: 0, day: 21} => {count: 3}
	{resource: 'index', year: 2010, month: 0, day: 21} => {count: 2}
	{resource: 'index', year: 2010, month: 0, day: 22} => {count: 1}

Technically, the output in MongoDB is:

	_id: {resource: 'home', year: 2010, month: 0, day: 20}, value: {count: 3}

Hopefully you've noticed that this is the final result we were after.

If you've really been paying attention, you might be asking yourself *why didn't we simply use `sum = values.length`?* This would seem like an efficient approach when you are essentially summing an array of 1s. The fact is that reduce isn't always called with a full and perfect set of intermediate data. For example, instead of being called with:

	{resource: 'home', year: 2010, month: 0, day: 20} => [{count: 1}, {count: 1}, {count:1}]

Reduce could be called with:

	{resource: 'home', year: 2010, month: 0, day: 20} => [{count: 1}, {count: 1}]
	{resource: 'home', year: 2010, month: 0, day: 20} => [{count: 2}, {count: 1}]

The final output is the same (3), the path taken is simply different. As such, reduce must always be idempotent. That is, calling reduce multiple times should generate the same result as calling it once.

We aren't going to cover it here but it's common to chain reduce methods when performing more complex analysis.

### Pure Practical ###
With MongoDB we use the `mapReduce` command on a collection. `mapReduce` takes a map function, a reduce function and an output directive. In our shell we can create and pass a JavaScript function. From most libraries you supply a string of your functions (which is a bit ugly). First though, let's create our simple data set:

	db.hits.insert({resource: 'index', date: new Date(2010, 0, 20, 4, 30)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 20, 5, 30)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 20, 6, 0)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 20, 7, 0)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 21, 8, 0)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 21, 8, 30)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 21, 8, 30)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 21, 9, 0)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 21, 9, 30)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 22, 5, 0)});

Now we can create our map and reduce functions (the MongoDB shell accepts multi-line statements, you'll see *...* after hitting enter to indicate more text is expected):

	var map = function() {
		var key = {resource: this.resource, year: this.date.getFullYear(), month: this.date.getMonth(), day: this.date.getDate()};
		emit(key, {count: 1});
	};

	var reduce = function(key, values) {
		var sum = 0;
		values.forEach(function(value) {
			sum += value['count'];
		});
		return {count: sum};
	};

Which we can use the `mapReduce` command against our `hits` collection by doing:

	db.hits.mapReduce(map, reduce, {out: {inline:1}})

If you run the above, you should see the desired output. Setting `out` to `inline` means that the output from `mapReduce` is immediately streamed back to us. This is currently limited for results that are 16 megabytes or less. We could instead specify `{out: 'hit_stats'}` and have the results stored in the `hit_stats` collections:

	db.hits.mapReduce(map, reduce, {out: 'hit_stats'});
	db.hit_stats.find();

When you do this, any existing data in `hit_stats` is lost. If we did `{out: {merge: 'hit_stats'}}` existing keys would be replaced with the new values and new keys would be inserted as new documents. Finally, we can `out` using a `reduce` function to handle more advanced cases (such an doing an upsert).

The third parameter takes additional options, for example we could filter, sort and limit the documents that we want analyzed. We can also supply a `finalize` method to be applied to the results after the `reduce` step.

### In This Chapter ###
This is the first chapter where we covered something truly different. If it made you uncomfortable, remember that you can always use MongoDB's other [aggregation capabilities](http://www.mongodb.org/display/DOCS/Aggregation) for simpler scenarios. Ultimately though, MapReduce is one of MongoDB's most compelling features. The key to really understanding how to write your map and reduce functions is to visualize and understand the way your intermediary data will look coming out of `map` and heading into `reduce`.

\clearpage

## 7章 - パフォーマンスとツール ##
最後の章では、パフォーマンスに関する話題とMongoDB開発者に有効な幾つかのツールを見ていきます。どちらの話題にも深くは追求しませんがそれぞれの重要な側面を検討します。

### インデックス ###
まず最初に、特別な`system.indexes`コレクションの中に含まれるデータベースのインデックス情報を見て行きましょう。MongoDBのインデックスはリレーショナルデータベースのインデックスと同じように動作します。すなわち、これらはクエリーやソートのパフォーマンスを改善するのに役立ちます。インデックスは`ensureIndex`を呼んで作成されます:

	// where "name" is the fieldname
	db.unicorns.ensureIndex({name: 1});

そして、`dropIndex`を呼んで削除します:

	db.unicorns.dropIndex({name: 1});

2番目のパラメーターに`{unique: true}`に設定することでユニークインデックスを作成できます。

	db.unicorns.ensureIndex({name: 1}, {unique: true});

インデックスは埋めこまれたフィールドと配列フィールドに対して作成できます。
複合インデックスも作成できます:

	db.unicorns.ensureIndex({name: 1, vampires: -1});

インデックスの順序(1は昇順、-1は降順)は単一のキーインデックスでは問題となりませんが、複合キーでソートやレンジ条件を利用した際に影響があります。

インデックスに関する詳しい情報は[indexes page](http://www.mongodb.org/display/DOCS/Indexes)にあります。

### Explain ###
To see whether or not your queries are using an index, you can use the `explain` method on a cursor:

	db.unicorns.find().explain()

The output tells us that a `BasicCursor` was used (which means non-indexed), 12 objects were scanned, how long it took, what index, if any was used as well as a few other pieces of useful information.

If we change our query to use an index, we'll see that a `BtreeCursor` was used, as well as the index used to fulfill the request:

	db.unicorns.find({name: 'Pilot'}).explain()

### Fire And Forget Writes ###
We previously mentioned that, by default, writes in MongoDB are fire-and-forget. This can result in some nice performance gains at the risk of losing data during a crash. An interesting side effect of this type of write is that an error is not returned when an insert/update violates a unique constraint. In order to be notified about a failed write, one must call `db.getLastError()` after an insert. Many drivers abstract this detail away and provide a way to do a *safe* write - often via an extra parameter.

Unfortunately, the shell automatically does safe inserts, so we can't easily see this behavior in action.

### シャーディング ###
MongoDB supports auto-sharding. Sharding is an approach to scalability which separates your data across multiple servers. A naive implementation might put all of the data for users with a name that starts with A-M on server 1 and the rest on server 2. Thankfully, MongoDB's sharding capabilities far exceed such a simple algorithm. Sharding is a topic well beyond the scope of this book, but you should know that it exists and that you should consider it should your needs grow beyond a single server.

### レプリケーション ###
MongoDB replication works similarly to how relational database replication works. Writes are sent to a single server, the master, which then synchronizes itself to one or more other servers, the slaves. You can control whether reads can happen on slaves or not, which can help distribute your load at the risk of reading slightly stale data. If the master goes down, a slave can be promoted to act as the new master. Again, MongoDB replication is outside the scope of this book.

 While replication can improve performance (by distributing reads), its main purpose is to increase reliability. Combining replication with sharding is a common approach. For example, each shard could be made up of a master and a slave. (Technically you'll also need an arbiter to help break a tie should two slaves try to become masters. But an arbiter requires very few resources and can be used for multiple shards.)

### 統計 ###
あなたは`db.stats()`とタイプすることでデータベースの統計を取得できます。データベースのサイズは最もよく扱う情報です。`db.unicorns.stats()`とタイプすることで`unicorns`というコレクションの統計を取得することも出来ます。同様にこのコレクションのサイズに関する情報も有用です。

### Webインターフェース ###
MongoDBを起動すると、Webベースの管理ツールに関する情報が含まれています(`mongod`を起動した時点までターミナルウィンドウをスクロールすればその様子を確認できるでしょう)。あなたはブラウザで<http://localhost:28017/>を開いてアクセス出来ます。設定ファイルに`rest=true`を追加して`mongod`プロセスを再起動すると、さらにこれを有効に活用出来るでしょう。このWebインターフェースはサーバの現在の状態についての洞察を与えてくれます。

### プロファイラ ###
以下を実行をする事でMongoDBプロファイラを有効にできます:

	db.setProfilingLevel(2);

有効にした後に、以下のコマンドを実行します:

	db.unicorns.find({weight: {$gt: 600}});

そして、プロファイラを観察して下さい:

	db.system.profile.find()

この出力は何がいつどれ程のドキュメントを走査し、どれ程のデータが返却されたかを教えてくれます。

再度、引数を`0``に変えて`setProfileLevel`を呼ぶことでプロファイラを無効に出来ます。他のオプションは`1`を指定することで100ミリ秒以上のクエリーのみをプロファイリングします。もしくは2番目のパラメータに最小時間をミリ秒で指定することが出来ます。

	//profile anything that takes more than 1 second
	db.setProfilingLevel(1, 1000);

### バックアップとリストア ###
MongoDBには`bin`の中に`mongodump`という実行ファイルが付属しています。単純に`mongodump`を実行すると、ローカルホストに接続して全てのデータベースを`dump`サブフォルダ以下にバックアップします。`mongodump --help`とタイプすると追加のオプションを確認できます。指定したデータベースをバックアップする`--db DBNAME`と、指定したコレクションをバックアップする`--collection COLLECTIONAME`は共通です。次に、同じ`bin`フォルダにある`mongorestore`実行ファイルを使うことで、以前のバックアップをリストアできます。同じように、`--db`と`--collection`はオプションはリストアするデータベースとコレクションを指定します

例えば、`learn`データベースを`backup`フォルダにバックアップするには以下を実行します(これ実行ファイルですのでmongoシェルではなく、ターミナルウィンドウでコマンドを実行します):

	mongodump --db learn --out backup

`unicorns`コレクションのみをリストアするにはこの様に実行します:

	mongorestore --collection unicorns backup/learn/unicorns.bson

`mongoexport`と`mongoimport`という２つの実行ファイルはJSONまたはCSV形式でエクスポートとインポートできることを指摘しておきます。例えばJSON形式で出力するには以下のようにします:

	mongoexport --db learn -collection unicorns

そして、CSV形式での出力はこうします:

	mongoexport --db learn -collection unicorns --csv -fields name,weight,vampires

`mongoexport`と`mongoimport`は完全にあなたのデータを表現できない事に注意して下さい。`mongodump`と`mongorestore`のみを実際のバックアップでは利用すべきです。

### 章のまとめ ###
この章では、MongoDBで利用する様々なコマンドやツールやパフォーマンスの詳細を見てきました。全てに触れる事は出来ませんでしたが最も一般的なものを紹介しました。MongoDBのインデックス化がリレーショナルデータベースのインデックス化とよく似ているのと同様に、ツールの多くも同じです。しかしMongoDBの方がわかり易くて単純に利用できるものが多いでしょう。

\clearpage

## まとめ ##
実際のプロジェクトでMongoDBを使い始める為には十分な情報を持つべきです。ここで紹介してきた事の他にも、MongoDBの情報はまだまだあります。しかし、あなたが次に優先すべき事は、これまでに学んできた事を組み合わせて、利用予定のドライバに慣れる事です。[MongoDBのウェブサイト](http://www.mongodb.com/)には数多くの役立つ情報があります。公式な[MongoDBユーザーグループ](http://groups.google.com/group/mongodb-user)は質問を尋ねるには最適な場所です。

NoSQLは必然性によって生み出されただけではなく、新しいアプローチへの興味深い試みでもあります。この分野の認知と発展は私たちが時々失敗し、挑戦しなければ成功はありえません。私が思うに、これは私たちがプロとして活躍するための近道となるでしょう。

<!--
# translate status
commit 5e8d9bcac1f0566d853ea954a5165d5dd369a095
Author: Karl Seguin <karlseguin@gmail.com>
Date:   Wed Mar 28 16:51:08 2012 +0800

    added translation section

-->
