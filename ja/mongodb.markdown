% MongoDBの薄い本
% Karl Seguin 著 / Tsukasa Hamano 訳

## この本について ##

### ライセンス ###
MongoDBの薄い本はAttribution-NonCommercial 3.0 Unportedに基づいてライセンスされています。*あなたはこの本の為にお金を支払う必要はありません。*

この本を複製、改変、展示することは基本的に自由です。しかし、この本は常に私(カール・セガン)に帰属するように求めます。そして私はこれを商用目的で使用する事はありません。

以下にライセンスの全文があります:

<http://creativecommons.org/licenses/by-nc/3.0/legalcode>

### 著者について ###
カール・セガンは幅広い経験と技術を持った開発者です。 彼は.Netのエキスパートであると同時にRubyの開発者です。彼はOSSプロジェクトのセミアクティブな貢献者であり、テクニカルライターや時々講演を行っています。MongoDBに関して、彼はC#のMongoDBライブラリNoRMの主要な貢献者であり、インタラクティブ・チュートリアル[mongly](http://mongly.com)や[Mongo Web Admin](https://github.com/karlseguin/Mongo-Web-Admin)を書きました。彼のカジュアルなゲーム開発者の為のサービス、[mogade.com](http://mogade.com/)はMongoDBで稼動しています。

カールは過去に[Redisの薄い本](http://openmymind.net/2012/1/23/The-Little-Redis-Book/)も書いています。

彼のブログは<http://openmymind.net>、つぶやきは[@karlseguin](http://twitter.com/karlseguin)で見つかります。

### 謝辞 ###
[Perry Neal](http://twitter.com/perryneal)が私に彼の目と意見と情熱を貸してくれたことに感謝します。ありがとう。

### 最新バージョン ###
この本の最新のソースはこちら:

<http://github.com/karlseguin/the-little-mongodb-book>

\clearpage

## 序章 ##
 > この章が短いことは私の誤りではありません、MongoDBを学ぶ事はとても簡単です。

しばしば、技術は激しい速度で変化していると言われます。それは新しい技術と技術手法が公開され続けているという点で真実ですが、私の見解ではプログラマによって利用される基礎的な技術の変化はかなり遅いと考えています。しかし、誰しもが過去のものになろうとする技術に学習コストを費やしたいとは思わないでしょう。注目すべき点は確立した技術が置きかえられる速度です。気がつくと、長い歴史を持つ技術がまるで一晩で開発者の関心の転移に脅かされているようです。

既に確立されているリレーショナルデーターベースに反発して発展してきたNoSQLはこの様な急転換の典型的な事例です。5年後、またはNoSQLが十分普及したいつの日か、昔のWebはRDBMSで動いていたと言われる様になるかもしれません。

たとえこれらの技術が一晩で推移したとしても、実際的な実務でこれらが受け入れられるには何年もがかかります。初期の情熱は比較的小規模な会社や開発者によって突き動かされます。新しい技術は彼らのような人々の挑戦によってゆっくりと普及しソリューションや教育環境が洗練されていきます。念の為、NoSQLは昔ながらのストレージソリューションを置き換える手段ではないという事については大部分は真実です。しかしある特定の分野では従来のものに優る価値を必要とします。

何よりもまず初めに、NoSQLが何を意味しているのかを説明すべきでしょう。それは人によって異なる意味を持つ広義の用語です。私は個人的に、それをデータストレージの役割を果たすシステムという意味で使用しています。言い換えれば、(私にとっての)NoSQLはあなたが執着する単一のシステムに必ずしも責任を持つようなものではありません。歴史的に見て、リレーショナルデータベースベンダーはどんなサイズにも適応する万能なソリューションとしてソフトウェアを位置づけてきました。NoSQLスタックはMySQLといったリレーショナルデータベースの様に利用する事も出来るでしょうが、NoSQLは与えられた仕事を達成する為の最適なツールとしてより小さい単位の役割に向かう傾向があります。そして、Redisもまた参照性能というシステムの特定部位に執着し、同じようにHadoopもデータ処理に集中的です。簡単に言うと、NoSQLはオープンであり、既存のものの代替や付加的なパターンを意識し、データを管理する為のツールです。

あなたはMongoDBが多くの事に適応する事に驚くかもしれません。Mongoはドキュメント志向データベースとしてよりNoSQLソリューションに汎用化されています。それはリレーショナルデータベースの代替の様に見られるでしょうが、リレーショナルデータベースと比較すると、もっと専門化したNoSQLソリューションにおいて恩恵を得ることが出来ます。MongoDBには利点と欠点がありますのでそれには後ほどこの本の中で触れます。

もう気がついているかもしれませんが、私たちはMongoDBという用語と同じ意味でMongoと呼ぶことがあります。

## はじめよう ##
この本の大部分はMongoDBの機能面に注目します。その為に私たちはMongoDBシェルを利用します。MongoDBドライバを利用するようになるまで、MongoDBシェルは学習に役立つだけでなく、便利な管理ツールとなるでしょう。

MongoDBについてまず最初に知るべきことを取り上げます: それはドライバです。MongoDBは各種プログラミング言語向けに[数多くの公式ドライバ](http://www.mongodb.org/display/DOCS/Drivers)が用意されています。これらのドライバは恐らくあなたがすでに慣れ親しんでいる各種データーベースのドライバと似たようなものだと考えて良いでしょう。これらのドライバに加えて、開発コミュニティでは更にプログラミング言語/フレームワーク用のライブラリが開発されています。例えば、[NoRM](https://github.com/atheken/NoRM)はLINQを実装したC#のライブラリで、[MongoMapper](https://github.com/jnunemaker/mongomapper)はActiveRecordと親和性の高いRubyライブラリです。プログラムから直接MongoDBのコアドライバを利用するか、他の高級なライブラリを選択するかはあなた次第です。何故公式ドライバとコミュニティライブラリの両方が存在するのかについてMongoDBに不慣れな多くの人に混乱があるようなので説明しておきます。前者はMongoDBの中核的な通信と接続性に、後者はよりプログラミング言語や特定のフレームワークの実装に集中しています。

これを読みながらあなたが実際に演習を反復し、自分自身で疑問を解決していく事を奨励します。MongoDBの準備と実行は簡単です、今から数分の時間をかけてセットアップしてみましょう。

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

セレクターについて掘り下げていく前に、演習の為の幾つかのデータをセットアップしましょう。まず最初に、これまでに`unicorns`コレクションに入れたドキュメントを`db.unicorns.remove()`を実行して削除します(セレクターを指定していないので、全てのドキュメントが削除されます)。さて、以下を実行して演習に必要なデータを挿入しましょう(コピペ推奨):

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
私たちはまだ`update`コマンドや、`find`で出来る幾つかの手の込んだ事は見ていません。しかし、私たちは簡単に`insert`コマンドと`remove`コマンドを確認しました(これまで見てきた以上のものはそれほど多くありません)。私たちは`find`の紹介とMongoDBの`selectors`というものも見てきました。私たちは順調なスタートと、来たるべき時の為の盤石な基礎を築く事が出来ました。信じようと信じまいと、あなたは実際にMongoDBについての殆どの事を知っています(素早く学習し、簡単に使えるようになるという意味でです)。次に移る前に、演習のデータをローカルコピーすることを強く推奨します。恐らく、新しいコレクションで違うドキュメントを挿入したり、セレクターと似たようなものを使います。`find`や`count`や`remove`も使います。いろいろ試しているうちに、なにかマズイ事が起こった場合に最初の状態に戻れるようにしておいた方が良いでしょう。

\clearpage

## 2章 - 更新(Update) ##
1章ではCRUD(作成、読み込み、更新、削除)の4つのうちの3つの操作を紹介しました。この章では、省略していた`update`に専念します。その理由は、`update`には幾つかの意外な振る舞いを持っているからです。

### 置換(Replace) と $set ###
最も単純な形式では、`update`は2つの引数をとります: セレクター(where条件)とアップデートするフィールドです。もしRoooooodlesの体重を少し増やしたい場合、これを実行します:

	db.unicorns.update({name: 'Roooooodles'}, {weight: 590})

(もし前回の演習で作成した`unicorns`コレクションを残していない場合、1章に戻って、全てのドキュメントを`remove`し、挿入し直して下さい。)

現実のコードでは、`_id`にを指定してレコードを更新するでしょうが、MongoDBが生成した`_id`はまだ知らないとして、`names`を指定します。アップデートされたレコードを確認する場合、以下のようにします:

	db.unicorns.find({name: 'Roooooodles'})

まずあなたは驚いてしまうでしょう。2番目に指定したパラメータは元のデータを**置き換える**為に使われてしまい、ドキュメントは見つかりません。言い換えると、`update`はドキュメントを`name`で検索し、ドキュメント全体を2番目のパラメータで置き換えます。これはSQLの`update`文と異なる動作です。忠実に動的な更新を行う目的の幾つかの状況では、これは理想的な動作です。しかし、ひとつか複数のフィールドの値を変更したい場合は、MongoDBの`$set`修飾子を利用するのが最適でしょう:

	db.unicorns.update({weight: 590}, {$set: {name: 'Roooooodles', dob: new Date(1979, 7, 18, 18, 44), loves: ['apple'], gender: 'm', vampires: 99}})

これで、失われたフィールドをリセットします。`weight`を指定しなければ上書きできません。以下を実行します:

	db.unicorns.find({name: 'Roooooodles'})

期待する結果が得られました。従って、最初に行いたかった体重を変更する正しい方法は以下の通りです:

	db.unicorns.update({name: 'Roooooodles'}, {$set: {weight: 590}})

### 更新修飾子(Modifier) ###
`$set`に加えて、その他の修飾子を利用するともっと粋なことが出来ます。これらの更新修飾子は、フィールドに対して作用します。なのでドキュメント全体が消えてしまうことはありません。例えば、`$inc`修飾子はフィールドの値を増やしたり、負の値で減らす事が出来ます。もしPilotが`vampire`を倒した数が間違っていて2つ多かった場合、以下のようにして間違いを修正します:

	db.unicorns.update({name: 'Pilot'}, {$inc: {vampires: -2}})

もしAuroraが突然甘党になったら、`$push`修飾子を使って、`loves`フィールドに値を追加することが出来ます:

	db.unicorns.update({name: 'Aurora'}, {$push: {loves: 'sugar'}})

その他の有効な更新修飾子はMongoDB Webサイトの[Updating](http://api.mongodb.org/wiki/current/Updating.html)に情報があります。

### Upserts ###
`update`にはもっと驚く愉快なものがあります。その一つは`upserts`を完全にサポートしている事です。`upsert`はドキュメントが見つかった場合に更新を行い、無ければ挿入を行います。`upsert`は見ればすぐ解るし、よくあるシチュエーションで重宝します。`upsert`呼ぶ際に3番目の引数を'true'に設定する事が出来ます。

一般的な例はWebサイトのカウンターです。複数のページのカウンターをリアルタイムに動作させたい場合、ページのレコードが既に存在しているか確認し、更新を行うか挿入を行うか決めなければなりません。3番目の引数を省略(もしくはfalseに設定)して実行すると、以下のようにうまくいきません:

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}});
	db.hits.find();

しかし、`upserts`を有効にすると違った結果になります。

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}}, true);
	db.hits.find();

`page`というフィールドの値が`unicorns`のドキュメントが存在していなければ、新しいドキュメントが挿入されます。2回目を実行すると既存のドキュメントが更新され、`hits`は2に増えます。

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}}, true);
	db.hits.find();

### 複数同時更新 ###
最後の驚きは、`update`はデフォルトで一つのドキュメントに対してのみ更新を行う事です。これまでの様に、まず例を見て行きましょう。以下のように実行します:

	db.unicorns.update({}, {$set: {vaccinated: true }});
	db.unicorns.find({vaccinated: true});

恐らくあなたは全てのかわいいユニコーン達が予防接種を受けた(vaccinated)と期待するでしょう。あなたが望む様な振る舞いを行うには、4番目のパラメータをtrueに設定する必要があります:

	db.unicorns.update({}, {$set: {vaccinated: true }}, false, true);
	db.unicorns.find({vaccinated: true});

### 章のまとめ ###
この章では、コレクションに対して有効なCRUD操作を紹介しました。私たちは`update`の詳細を確認し、3つの興味深い振る舞いを観察しました。まず、MongoDBの`update`はSQLの`update`と異なり、ドキュメント全体を置き換えます。そんな訳で`$set`修飾子はとても便利です。次に、`update`は直感的な`upsert`をサポートしています。これは`$inc`修飾子と一緒に使うと非常に便利です。最後に、デフォルトで`update`は最初にみつけたドキュメントしか更新しません。

私たちはシェルの視点からMongoDBを見てきた事を思い出して下さい。ドライバやライブラリの場合でも、デフォルトの振る舞いを切り替えて使用したり、異なるAPIに触れる事になります。

例えば、Rubyのドライバでは最後2つのパラメータを一つのハッシュにまとめています:

    {:upsert => false, :multi => false}

同様に、PHPのドライバも最後2つのパラメータを配列にまとめています。

    array('upsert' => false, 'multiple' => false)

\clearpage

## 3章 - 検索(Find)の習得 ##
1章では、`find`コマンドについて簡単に説明しました。ここでは`find`やセレクターについての理解を深めていきます。`find`が`カーソル`を返却することについては既に述べましたので、もっと正確な意味を見ていきましょう。

### フィールド選択 ###
`カーソル`ついて学ぶ前に、`find`に任意で設定出来る2番目のパラメータについて知る必要があります。このパラメーターは取得したいフィールドのリストです。例えば、以下の様に実行して、全てのユニコーンの名前を取得出来ます。

	db.unicorns.find(null, {name: 1});

デフォルトで、`_id`フィールドは常に返却されます。明示的に`{name:1, _id: 0}`を指定する事でそれを除外する事が出来ます。

`_id`に関する余談ですが、包含条件と排他条件を混ぜることが出来るのかどうか、気になるかもしれません。あなたはフィールドを含めるか除くかのどちらかを選択することが出来ます。

### 順序 ###
これまでに何度か、`find`が必要な時に遅延して実行されるカーソルを返却する事に言及しました。しかし、まだあなたはこれをシェルから直接'find'を実行して自分の目で観測していません。この振る舞いはシェルのみとなります。カーソルの本当の振る舞いは`find`に一つのメソッドを連結することで観測することが出来ます。昇順でソートを行いたい場合はフィールドと1を指定し、降順で行いたい場合は-1を指定します。例えば:

	//最も重い最初のユニコーン
	db.unicorns.find().sort({weight: -1})

	//by vampire name then vampire kills:
	db.unicorns.find().sort({name: 1, vampires: -1})

リレーショナルデータベースの様に、MongoDBもソートの為にインデックスを利用出来ます。インデックスの詳細は後で詳しく見ていきますが、MongoDBにはインデックスを使用しない場合にソートのサイズ制限があることを知っておく必要があります。すなわち、もし巨大な結果に対してソートを行おうとするとエラーが返ってきます。実際の話、その他のデータベースでにも、最適化されていないクエリーを拒否する機能があった方が良いと考えています。(私はこの動作をMongoDBの欠点とは考えていませんし、データベースの最適化が下手な人達にこの機能を使って欲しいと強く願っています。)

### ページング ###
ページングの結果はcursorの`limit`メソッドや`skip`メソッドを利用して遂行できます。2番目と3番目に重いユニコーンを得るにはこうやります:

	db.unicorns.find().sort({weight: -1}).limit(2).skip(1)

`limit`と`sort`を組み合わせると、インデックス化されていないフィールドでソートする場合の問題を避けるのに役立ちます。

### カウント ###
シェルではcollectionに対して直接`count`を呼び出す事が出来ます。例えば:

	db.unicorns.count({vampires: {$gt: 50}})

実際には`count`は`cursor`のメソッドであり、シェルは単純なショートカットを提供しているだけです。この様なショートカットを提供しないドライバでは以下の様に実行する必要があります(これはシェルでも動きます):

	db.unicorns.find({vampires: {$gt: 50}}).count()

### 章のまとめ ###
`find`や`cursors`の率直な使われ方を見てきました。これらの他に、あとの章で触れるコマンドや特別な状況で使われるコマンドが存在しますが、あなたは既にMongoDBの基礎を理解し、mongoシェルを安心して触れるようになったでしょう。

\clearpage

## 4章 - データモデリング ##
さて、MongoDBのもっと抽象的な話題に移っていきましょう。幾つかの新しい用語や、些細な機能の新しい文法について説明していきます。新しいパラダイムであるモデリングについての話題は簡単ではありません。モデリングに関する新しい技術について、大抵の人々はまだ何が役に立ち、役に立たないのかをよく知りません。まずは講話から始めますが、最終的には実際のコードで学び、実践を行っていきます。

モデリングに関して言えば、ドキュメント指向データベースである多くのNoSQLソリューションとリレーショナルデータベースを比較して大した違いは在りません。しかし違いが少ないからといってそれらが重要で無い訳ではありません。

### Joinは在りません ###
まず最初に、最も根本的な違いであるMongoDBにJoinが存在しない事に対して安心する必要があるでしょう。MongoDBが何故joinの文法をサポートしていないのか、特別な理由を私は知りませんが、Joinがスケーラブルでない事は一般的に知られています。すなわち、一度データの水平分割を行うと、最終的にクライアント(アプリケーションサーバー)側でJoinを行う事になります。理由はどうあれ、データはリレーショナルである事に変り在りませんが、MongoDBはJoinをサポートしていません。

とにかく、Join無しの世界で生活するためにはアプリケーションのコード内でJoinを行わなくてはなりません。それには基本的に2度目の`find`クエリーを発行してデータを取得する必要があります。これから準備するデータはリレーショナルデータベースの外部キーと違いはありません。しばらく素敵な`unicorns`コレクションから視点を外して、`employees`コレクションに注目してみましょう。まず最初に、社員を作成します。(分かり易く説明する為に、`_id`フィールドを明示的に指定しています)

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d730"), name: 'Leto'})

さて、`Leto`がマネージャーとなる様に設定した社員を何人か追加してみましょう:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d731"), name: 'Duncan',
                         manager: ObjectId("4d85c7039ab0fd70a117d730")});
	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d732"), name: 'Moneo',
                         manager: ObjectId("4d85c7039ab0fd70a117d730")});

(上記に倣って、`_id`はユニークになる必要があります。
ここで実際に指定した`ObjectId`を、以降も同じ様に使用する事になります。)

言うまでもなく、Letoの社員を検索するには単純に以下を実行します:

	db.employees.find({manager: ObjectId("4d85c7039ab0fd70a117d730")})

これは何の変哲もありません。
最悪の場合、joinの欠如はただ単に余分なクエリーが多くの時間を占めるかもしれません
(恐らくインデックス化されているでしょうが)。

#### 配列と埋め込みドキュメント ####
MongoDBがjoinを持たないと言うだけで、切り札が無いという意味ではありません。MongoDBのドキュメントがファーストクラスオブジェクトとしての配列をサポートしてい事を簡単に確認したのを思い出してください。これは、多対一、多対多の関係を表現する際にとても器用に役立つ事が分かります。簡単な例として、社員が複数のマネージャーを持つ場合、単純にこれらを配列で格納する事が出来ます:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d733"), name: 'Siona',
                         manager: [ObjectId("4d85c7039ab0fd70a117d730"),
                                   ObjectId("4d85c7039ab0fd70a117d732")]})

得に興味深い事は、ドキュメントはスカラ値であっても構わないし、配列であっても構わないという点です。最初の`find`クエリーはどちらであっても動作します:

	db.employees.find({manager: ObjectId("4d85c7039ab0fd70a117d730")})

これによって、多対多のjoinテーブルよりもっと便利に素早く配列の値を見つけることが出来ます。

配列に加えて、MongoDBは埋め込みドキュメントをサポートしています。次に進んで入れ子になったドキュメントを挿入してみてください:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d734"), name: 'Ghanima',
                         family: {mother: 'Chani',
                                  father: 'Paul',
                                  brother: ObjectId("4d85c7039ab0fd70a117d730")}})

驚くでしょうが、埋め込みドキュメントはクエリーにドット表記を使用できます:

	db.employees.find({'family.mother': 'Chani'})

後ほど、埋め込みドキュメントがどの様な場所に適合し、どの様に使用するかを簡単に説明します。

#### DBRef ####
MongoDBは`DBRef`と言われる習慣を多くのドライバーでサポートしています。ドライバが`DBRef`に遭遇すると、自動的に参照先のドキュメントを取得します。`DBRef`はコレクションやドキュメントの参照IDを含みます。これは一般的に特定の目的に対して提供される機能です。例えばドキュメントが同じコレクションのドキュメントから参照され、異なるコレクションからも同じドキュメントを参照するような場合です。つまり、ドキュメント1が`managers`のドキュメントを指し示す`DBRef`である一方、ドキュメント2が`employees`のドキュメントを指し示す事が出来ます。

#### 非正規化 ####
joinを使う事の代わりのもうひとつの代替は、データを非正規化する事です。従来、非正規化はパフォーマンス特化の為やデータの速記(ログの様な)の為に利用されてきました。ところが、NoSQLの人気が高まるにつれて、joinを行わないことや非正規化は次第に一般的なモデリング手法として認められるようになってきました。これは全てのドキュメントであらゆる情報が重複するという意味ではありません。けれども、その方がかえって重複を恐れずに、データがどの情報に基づいていて、どのドキュメントに属しているかをよく考えてモデリングし、設計を行う傾向があります。

例えば、掲示板のWEBアプリケーションを作っているとします。伝統的な方法では、`posts`テーブルにある`ユーザーID`によって`ユーザー`と`投稿`を紐付けます。この様なモデルでは`users`テーブルを検索(もしくはjoin)しなければ`投稿`を表示することが出来ません。埋め込みドキュメントがあればこういう事も出来るでしょう:

    `user: {id: ObjectId('Something'), name: 'Leto'}`

もちろんこうした場合、ユーザーが名前を変更すると全てのドキュメントを更新しなければなりません(一度のクエリーで済みます)。

この種の取り組みを調整する事はそれほど簡単ではありません。多くの場合、この様な調整は非常識で効果が無いかもしれません。しかし、この取り組みへの実験を恐れないでください。状況によっては適切ではありませんが、その取り組みが効果的で正しい対処になることもあるでしょう。

#### どちらを選ぶ? ####
1対多や多対多の関係のシナリオでIDを配列にする事は有用な戦略です。`DBRef`は実験的に利用することは出来ますがそれほど利用頻度は多くないと言っても間違いではないと思います。一般的な新しい開発者にとって、埋め込みドキュメントを利用するか、手動で参照を行うか悩んでしまう事がよくあります。

まず、個々のドキュメントのサイズは4MByteまでに制限されていることを知らなければなりません。ドキュメントのサイズに制限があるとわかった所で、気前よく替りにどの様にすれば良いかのアイディアを提供しましょう。現在の所、開発者が巨大なリレーションを行いたい場合、大抵は手動で参照しなければならない様に思われます。埋め込みドキュメントは頻繁に利用されますが、データの小片は親ドキュメントと同時に取得したい場合が殆どです。
実例として、`accounts`コレクションに以下のユーザーを格納してみます:

	db.users.insert({name: 'leto', email: 'leto@dune.gov', account: {allowed_gholas: 5, spice_ration: 10}})

これを単に手っ取り早く書き込むための只のユーティリティだと過小評価してはいけません。直接ドキュメントを持つ事は、データモデルをより単純にし、多くの場合Joinの必要性を無くします。これは、埋め込みドキュメントのインデックスフィールドや、クエリーを考慮すると、特にあてはまります。

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
MapReduceは、従来のソリューションを上回る2つの有用な利点を持ったデータ処理手法です。最初であり、かつ主要な目的はパフォーマンスを発達させる事です。理論上では、MapReduceは並行化によって、巨大なデータセットを多くのCPUやマシンで処理するする事が出来ます。最初に述べておくと、MongoDBは現在の所この利点はありません。MapReduceの2番目の利点は実際に書いたコードで処理することが出来るという事です。SQLと比べて何を行えるのか比較すると、MapReduceのコードは特別なソリューションを利用すること無く機能を拡張し、飛躍的に豊かな柔軟性を提供します。

MapReduceは注目を集めているパターンです、あなたは、C#, Ruby, Java, Pythonなど、ほとんど全ての実装でこれを利用することが出来ます。それらはまったく異なっていて複雑に見える事を警告しておきます。挫折せず時間をかけて学んで見てください。これはMongoDBの利用に関わらず理解しておく価値があります。

### 理論と実践 ###
MapReduceは2段階の処理に分かれています。最初にmapを行い、次にreduceを行います。mappingの段階で入力されたドキュメントを変換し、key=>valueのペアをemitします(キーと値は複合化可能です)。reduceの段階でemitされたキーと値の配列から処理を行った最終的な結果を集約します。それでは各段階での出力を見ていきましょう。

ここでは、(Webページの)リソースに対して日別のアクセス数のレポートを生成する例を使用します。これはMapReduceの*hello world*です。目的は、`hits`コレクションに2つのフィールド: `resource`と`date`を入力として利用し、求められる出力は`resource`、`year`、`month`、`day`、`count`に分割されている事です。

`hits`に以下のデータがあります:

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

以下の出力を期待しているとします:

	resource  year   month   day   count
	index     2010   1       20    3
	about     2010   1       20    1
	about     2010   1       21    3
	index     2010   1       21    2
	index     2010   1       22    1

この種のアクセス解析の良い所は、レポートを素早く生成して出力を保存し、増え続けるデータを抑制出来る事です。(1日毎に解析するページの数だけのドキュメントが追加されます。)

当面は、概念の理解に集中します。章の最後の方でサンプルデータとコードを利用して自分自身で試してみましょう。

まず初めに、以下のmap関数を見てください。mapの目的はreduce出来るような値を生成し、emitする事です。mapは0回以上emitする事が可能です。今回の場合、全て共通に一度だけemitを行います。このmap関数はhitsコレクションのドキュメント毎にループしていると想像して下さい。ドキュメント毎に、キーをresource, year, month, day指定し、値には単純に1を指定してemitします:

    function() {
        var key = {
            resource: this.resource,
            year: this.date.getFullYear(),
            month: this.date.getMonth(),
            day: this.date.getDate()
        };
        emit(key, {count: 1});
    }

`this`はループ中のドキュメントを参照します。恐らくは、map段階の後にどの様なデータが出力されるかを確認する事が、理解の助けになるでしょう。前記した入力データを利用すると、map完了後のデータは以下の様になります:

	{resource: 'index', year: 2010, month: 0, day: 20}
    => [{count: 1}, {count: 1}, {count:1}]
    
	{resource: 'about', year: 2010, month: 0, day: 20}
    => [{count: 1}]
    
	{resource: 'about', year: 2010, month: 0, day: 21}
    => [{count: 1}, {count: 1}, {count:1}]
    
	{resource: 'index', year: 2010, month: 0, day: 21}
    => [{count: 1}, {count: 1}]
    
	{resource: 'index', year: 2010, month: 0, day: 22}
    => [{count: 1}]

この中間段階を理解することが、MapReduceを理解する事の鍵です。emit後のキーに対応する値は、配列としてまとめられています。.NETやJava開発者は`IDictionary<object, IList<object>>`(.Net)や`HashMap<Object, ArrayList>`(Java)の様な物だと思って構いません。

それでは、map関数を不自然に変更してみましょう:

    function() {
        var key = {
            resource: this.resource,
            year: this.date.getFullYear(),
            month: this.date.getMonth(),
            day: this.date.getDate()
        };
        if (this.resource == 'index' && this.date.getHours() == 4) {
            emit(key, {count: 5});
        } else {
            emit(key, {count: 1});
        }
    }

中間段階の出力は以下の様に変わります:

	{resource: 'index', year: 2010, month: 0, day: 20}
    => [{count: 5}, {count: 1}, {count:1}]

キーに対応してemitで生成される値が、どの様にまとめられているかに注目して下さい。

reduce関数はこれらの中間結果を受け取り、最終的な結果として出力します。
以下を見て下さい:

	function(key, values) {
		var sum = 0;
		values.forEach(function(value) {
			sum += value['count'];
		});
		return {count: sum};
	};

以下の出力を得られます:

	{resource: 'index', year: 2010, month: 0, day: 20} => {count: 3}
	{resource: 'about', year: 2010, month: 0, day: 20} => {count: 1}
	{resource: 'about', year: 2010, month: 0, day: 21} => {count: 3}
	{resource: 'index', year: 2010, month: 0, day: 21} => {count: 2}
	{resource: 'index', year: 2010, month: 0, day: 22} => {count: 1}

正確には、MongoDBはこの様に出力します:

	_id: {resource: 'home', year: 2010, month: 0, day: 20}, value: {count: 3}

これが目的の結果である事に気が付きましたでしょうか。

注意深く見て来たのであれば、あなたはこんな疑問を持つかもしれません *なぜ単純に`sum = values.length`を利用しないのですか?*原則として`{count: 1}`しか合計しない場合、この方法は効果的の様に見えます。答えは、reduceは常に完全な中間データを渡されて呼び出されるとは限らないという事です。例えば、reduceは以下の様に呼ばれるかもしれないし:

	{resource: 'home', year: 2010, month: 0, day: 20}
    => [{count: 1}, {count: 1}, {count:1}]

以下の様に呼ばれるかもしれません:

	{resource: 'home', year: 2010, month: 0, day: 20}
    => [{count: 1}, {count: 1}]
    
	{resource: 'home', year: 2010, month: 0, day: 20}
    => [{count: 2}, {count: 1}]

最終的な出力は同じく(3)ですが単純に経緯が異なります。reduceは常に冪等であると言えます。つまり、reduceが何回呼ばれたとしても、1回呼ばれた場合と同じ結果にならなくてはなりません。

ここでは触れませんが、より複雑な解析を行う場合、reduceメソッドを連鎖する事は一般的です。

### ひたすら練習 ###
MongoDBでは、コレクションに対して`mapReduce`コマンドを呼び出してMapReduceを実行します。`mapReduce`には引数にmap関数とreduce関数、そして出力ディレクティブを引き渡します。mongodbのシェルではJavaScriptの関数を定義して解釈します。多くのライブラリでは関数を文字列で引き渡します(ちょっとカッコ悪いけど)。まずはこれらのデータを入力してみましょう:

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

続いてmapとreduce関数を定義します(MongoDBのシェルは複数行の命令文を解釈します。*...*は引き続きテキストが入力される事を期待しています):

	var map = function() {
		var key = {resource: this.resource,
                   year: this.date.getFullYear(),
                   month: this.date.getMonth(),
                   day: this.date.getDate()
                  };
		emit(key, {count: 1});
	};

	var reduce = function(key, values) {
		var sum = 0;
		values.forEach(function(value) {
			sum += value['count'];
		});
		return {count: sum};
	};

`hits`コレクションに対して、`mapReduce`コマンドをこの様に実行します:

	db.hits.mapReduce(map, reduce, {out: {inline:1}})

上記を実行すると、期待した出力が表示されます。`out: {inline:1}`を設定すると、`mapReduce`の処理結果が順次表示されます。この機能は現在の所結果のサイズが16MByte以下に制限されています。代わりに、`{out: 'hit_stats'}`と指定することで結果を`hit_stats`コレクションに格納することが出来ます:

	db.hits.mapReduce(map, reduce, {out: 'hit_stats'});
	db.hit_stats.find();

これを行うと、既存の`hit_stats`にある既存のデータは消えてしまいます。もし`{out: {merge: 'hit_stats'}}`を指定したのであれば、既存のキーは上書きされ、新しいキーは新しいドキュメントとして挿入されます。最後に、高度な使い方として、`reduce`関数で`out`を操作することが可能です(upsertの様な使い方が出来ます)

3番目の引数は追加のオプションを渡します。例えば、解析したいドキュメントを制限したり、フィルタやソートを行うことが出来ます。`finalize`メソッドを渡すと、`reduce`後の段階結果にこの関数を適用することもできます。

### 章のまとめ ###
これは、これまでに触れてきた内容とはまったく異なる最初の章でした。もし不安が残るようであれば、MongoDBのその他の[aggregation capabilities](http://www.mongodb.org/display/DOCS/Aggregation)を参照することが出来ます。最後になりますが、MapReduceはMongoDBの最も強力な機能のひとつです。正しく理解するための鍵は、あなたの書いたmapとreduce関数を思い浮かべ、`map`を出てから`reduce`に入る前の中間データを理解することです。

\clearpage

## 7章 - パフォーマンスとツール ##
最後の章では、パフォーマンスに関する話題とMongoDB開発者に有効な幾つかのツールを見ていきます。どちらの話題にも深くは追求しませんがそれぞれの重要な側面を検討します。

### インデックス ###
まず最初に、特別な`system.indexes`コレクションの中に含まれるデータベースのインデックス情報を見て行きましょう。MongoDBのインデックスはリレーショナルデータベースのインデックスと同じように動作します。すなわち、これらはクエリーやソートのパフォーマンスを改善するのに役立ちます。インデックスは`ensureIndex`を呼んで作成されます:

	// この "name" はフィールド名です
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
 インデックスを使用しているかに関わらず、カーソルに対し`explain`メソッドを使うことが出来ます:

	db.unicorns.find().explain()

出力は`BasicCursor`が利用され(インデックスを使用していない事を意味します)、12のオブジェクトをスキャンしてどれくらいの時間がかかったのかなど、その他の便利な情報も教えてくれます。

もしインデックスを利用するように変更した場合`BtreeCursor`が利用されていることを確認できます。この場合、インデックスはうまく利用できているでしょう:

	db.unicorns.find({name: 'Pilot'}).explain()

### 一方向通信書き込み ###
前述したように、MongoDBの書き込みはデフォルトでは一方向通信(fire-and-forget)です。これによってクラッシュするとデータを失うリスクと引き換えに素晴らしいパフォーマンスを得ることが出来ます。興味深い副作用として、挿入や更新などの書き込みでユニーク制約の違反が発生した場合でもエラーを返却しません。書きこみ失敗について知る為には挿入を行った後に`db.getLastError()`を呼ぶ必要があります。多くのドライバは*安全な*書き込みを行う方法を追加のパラメーターによって抽象化して提供しています。

あいにく、シェルは自動的に安全な挿入を行います。従って私たちはこの動作の振る舞いを簡単に確認することが出来ません。

### シャーディング ###
MongoDBは自動シャーディングをサポートしています。シャーディングはデータを複数のサーバーに分割してスケーラビリティを高める手法です。単純な実装ではデータの名前がA〜Mで始まるものをサーバー1に、残りをサーバー2に格納するでしょう。有り難いことに、MongoDBのシャーディング能力はその単純なアルゴリズムを上回ります。シャーディングの話題はこの本では取り上げませんが、単一サーバーのデータが限界まで増えた際に、あなたはシャーディングの存在と、それついてよく知っている必要があるでしょう。

### レプリケーション ###
MongoDBのレプリケーションの動きはリレーショナルデータベースのそれ動作とよく似ています。単一のマスターサーバーに対し書き込みが行われると、他のスレーブサーバに同期とします。あなたはスレーブに対して読み込みリクエストを発生させるかどうかを制御できます。これは古いデータを読み込むリスクを低減させるのに役立ちます。マスターが落ちた場合、スレーブが新しいマスターの役割に昇格することが出来ます。MongoDBのレプリケーションもまた、この本の主題から外れます。

レプリケーションの主要な目的は信頼性の向上ですが、読み込みリクエストを分散することでパフォーマンスを改善することも出来ます。レプリケーションとシャーディングを組み合わせることは一般的な方法です。例えば、それぞれのマスターとスレーブシャードを共有することが出来ます。(厳密には、調停者が2つのスレーブの均衡を破って、マスターになれる様に助ける必要があります。その為に調停者は若干のリソースと、複数のシャードを利用できる事を要求します。)

### 統計 ###
あなたは`db.stats()`とタイプすることでデータベースの統計を取得できます。データベースのサイズは最もよく扱う情報です。`db.unicorns.stats()`とタイプすることで`unicorns`というコレクションの統計を取得することも出来ます。同様にこのコレクションのサイズに関する情報も有用です。

### Webインターフェース ###
MongoDBを起動すると、Webベースの管理ツールに関する情報が含まれています(`mongod`を起動した時点までターミナルウィンドウをスクロールすればその様子を確認できるでしょう)。あなたはブラウザで<http://localhost:28017/>を開いてアクセス出来ます。設定ファイルに`rest=true`を追加して`mongod`プロセスを再起動すると、さらにこれを有効に活用出来るでしょう。このWebインターフェースはサーバの現在の状態についての洞察を与えてくれます。

### プロファイラ ###
以下を実行をすることでMongoDBプロファイラを有効にできます:

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

`mongoexport`と`mongoimport`は完全にあなたのデータを表現できないことに注意して下さい。`mongodump`と`mongorestore`のみを実際のバックアップでは利用すべきです。

### 章のまとめ ###
この章では、MongoDBで利用する様々なコマンドやツールやパフォーマンスの詳細を見てきました。全てに触れることは出来ませんでしたが最も一般的なものを紹介しました。MongoDBのインデックス化がリレーショナルデータベースのインデックス化とよく似ているのと同様に、ツールの多くも同じです。しかしMongoDBの方がわかり易くて単純に利用できるものが多いでしょう。

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
