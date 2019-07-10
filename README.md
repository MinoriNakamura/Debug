# Visual Studioを用いたデバック方法について
ここでは、私たちが使っているVisual Studio(以下VS)を使ったデバッグ方法について書いていく。

### ブレークポイント
ブレークポイントは、VSでデバッグすることにおいて**最も重要な機能**である。
ブレークポイント、これだけは覚えていてほしい。
プログラムを普通に実行した場合、エラーや不正な結果はコードが実行された後でしか表示されない。 
プログラムが理由を示すことなく予期せず終了する可能性もある。
そんな時に**便利なのがブレイクポイント**だ。
ブレークポイントはプログラムの実行中に発生するすべてのことをデバッガーが能動的に監視し、 
いつでも**プログラムを一時停止**して状態を調べた後、コードを 1 行ずつステップ実行して発生するすべてのことを詳しく確認することができる。

要約すると、ブレークポイントは   
メモリの中と変数の中身を　**見れる　書き替えられる**機能である。

#### 使用方法
実行可能なプログラムをVSで開く →　一時停止したい箇所の**行数の左端をクリック**する　→　**F5**実行を押す   
この**3 STEP**で簡単にブレークポイントを使うことができる。
他にも、**ブレークポイントを貼りたい行にマウスオーバーし、F9を押す**ことでも可能である。

#### ブレークポイントって何がうれしいの？
上で書いた使用方法では、使い方は分かっても**何がうれしいか**わからないと思う。
なので、これから実際にブレークポイントを使って説明していこうと思う。   
まず私は
2^0～2 3 4 5^と順番に計算していき、その結果が100以下まで表示するプログラムを作った。
では使用方法にのっとってブレークポイントを貼ってみよう。
![bp](https://user-images.githubusercontent.com/51075129/60633567-32e0bf80-9e46-11e9-832f-68a7784c41f0.png)
貼ってみた。行数の左側に赤い丸がついていれば完璧である。   
では、実行してみよう。
![bp1](https://user-images.githubusercontent.com/51075129/60633750-0aa59080-9e47-11e9-8780-751b13a50fd3.gif)
VSの枠がオレンジ色になれば成功である。
いま処理はブレークポイントを貼った位置で処理が一時停止している。
では今の**a**の値は何だろう。  
 
ここを見てみてみよう。
![bp5](https://user-images.githubusercontent.com/51075129/60776385-ca0b8700-a166-11e9-9993-c29c5ad68d70.gif)
マウスカーソルが荒ぶっている左下の部分だ。
今**a**にはゴミが入っていることがわかる。

では下へ進めてみよう。実は赤い画面の時にF11を押すことで下へブレークポイントが進む。
![bp3](https://user-images.githubusercontent.com/51075129/60634627-88b76680-9e4a-11e9-8bf9-e8a6177f5f0e.gif)
F11を押して進めてみた。
矢印が残っていたら成功である。   
さて、**a**の値は何になっていただろうか。
1になっていることがわかるだろうか。   
ではどんどん進めていこうと思う。
![bp4](https://user-images.githubusercontent.com/51075129/60635065-3f681680-9e4c-11e9-86cf-08ee88e4ee75.gif)
2になった。しっかり**a+=a**の処理を通過したことにより**a**の値が2になったことがわかる。
その調子でどんどん進めていって欲しい。   
もうブレークポイント要らない！！！ってときは**画面上の赤い四角ボタン**を押せば強制終了となる。

この機能説明は初歩的なことしか書いていないため、これから活用してほしい。

### step in/over/out
この3つの機能は上で書いた実行中断時(ブレークポイント)に一緒に使うものだ。
- **step in**   
step inは最もステップ単位が小さいデバッグ方法だ。
基本的に1行単位で実行される。
このステップ実行をすると、関数の内部にもどんどん入ることができる。
**つまり先ほどでてきたF11である。**

- **step over**   
step overは同じく1行単位で実行されるのですが、関数があった場合その関数を実行して次の行に移行する。
関数の内部に入らずそれを飛ばすため「オーバー」である。
**F10で使うことができる。**

- **step out**   
step outは上2つよりもちょっとだけマイナーな感じがしますが、これは今実行している関数の外（呼び出し元）に出るまでプログラムを進めるステップ実行だ。
今の関数の動作チェックができたので呼び出し元に戻りたい事はまあある。
そういう時に使えるものだ。
**Shift + F11で使うことができる**

### ローカル変数、自動変数、ウォッチ　ウィンドウ

これらのウィンドウは実行中断時(ブレークポイント使用時)に下に表示されている変数名とその値を表示してくれるウィンドウだ。
察しのいい人なら気づくだろう。そう、上で書いた使用方法ででてきたものだ。
- ウォッチ
ウォッチは、自分が見たい変数を指定することができる。

- 自動変数
自動変数は、停止した行とその前の行で使用されている変数が表示される。

- ローカル変数
ローカルは、停止したスコープの中のローカル変数が表示される。

この3つは実行時に、左下のタブで変更することができる。
![2019-07-04 (2)_LI](https://user-images.githubusercontent.com/51075129/60637099-0cc21c00-9e54-11e9-9c6c-2ef359e72adf.jpg)

### データブレイクポイント
データ ブレークポイントは、特定の変数の値が変更されたときに実行を中断するものだ。

#### データブレイクポイントを設定する
実際にデータブレイクポイントを設定してみようと思う。
1. まず自分の調べたい変数が初期化された行にブレークポイントを貼る。
2. 実行する
3. 上のタブの[**デバッグ**]→[**ブレークポイントの作成**]→[**データブレイクポイント**]の順番に選択していき、条件を記入する。

では、その条件の具体例を紹介しようと思う。
![bp6](https://user-images.githubusercontent.com/51075129/60778563-6ab37400-a172-11e9-8ab4-c37a1759e4f8.gif)
どうだろうか、私は**a**という値が変更されたら実行を中断するように設定した。

#### データブレークポイントの何がうれしいか
実際にデータブレイクポイントを使うことによって、その変数の値がいつ変更されたかが一目で判明するため、
予期せぬバグに対応することができる。

### メモリウィンドウ
メモリウィンドウとは、デバック中に表示することができるウィンドウであり、
そこには確保しているメモリ領域が表示される。

#### メモリウィンドウを表示させて使用する
これからメモリウィンドウの主な使い方を説明しようと思う。
1. 自分の調べたい変数が初期化された行にブレークポイントを貼る。
2. 実行する
3. 上のタブの[**デバッグ**]→[**ウィンドウ**]→[**メモリ**]の順に選択していく。
4. 表示されたウィンドウの上のアドレスに自分の調べたい変数のアドレスを記入する。
それによって表示されたアドレスの複雑な数字がメモリの**先頭アドレス**である。

また、実際にやってみた。
![bp7](https://user-images.githubusercontent.com/51075129/60779629-6a1cdc80-a176-11e9-8399-7b68c493902f.gif)
わたしは**a**のメモリの中身を調べたかったため、**&a**を記入した。
f10を押して進めていくと**&aのメモリの中が変更**されていることがわかる。
　
#### メモリウィンドウの何がうれしいか
メモリの中や、先頭アドレスを知ることで、その変数のメモリがいつ変更されたかが一目で判明するため、
予期せぬバグに対応することができる。
配列、二次元配列を使うとその嬉しさがわかると思う。

### コールスタック
コールスタックは、実行中の[サブルーチン](https://ja.wikipedia.org/wiki/%E3%82%B5%E3%83%96%E3%83%AB%E3%83%BC%E3%83%81%E3%83%B3)に関する情報を格納するスタックである。 
実行中のサブルーチンとは、呼び出されたが処理を完了していないサブルーチンを意味する。
要するに、呼び出し履歴のことである。

#### コールスタックを表示させる
これから、コールスタックの表示方法を説明しようと思う。
1. ブレークポイントを貼り、実行する
2. [**デバッグ**]→[**ウィンドウ**]→[**呼び出し履歴**]
この 2 STEP で表示することができる。

#### コールスタックの何がうれしいか
DirectXなどの関数がたくさんある場合はものすごく便利である。
F11で関数の中に入ると関数の中身を全て見に行ってくれる。

関数がたくさん出てくるプログラムでコールスタックを表示してみた。
![bp8](https://user-images.githubusercontent.com/51075129/60870195-5901c780-a26b-11e9-9577-d842cff982b0.gif)
見てわかるように、すべての関数の中身を見に行き、ウィンドウに行数も表示してくれる。
長いコードを追いかけるために使うと便利ではないかと思う。

### イミディエイトウィンドウ
イミディエイトウィンドウは、実行中にイミディエイトウィンドウを表示させ、そこに
コードを打つと、評価してくれて、その結果を確認することができる機能である。   
イミディエイト→immediate(直接、早速)

#### イミディエイトウィンドウを表示させて使用する
これからイミディエイトウィンドウの主な使い方を説明しようと思う。
1. 任意の場所にブレークポイントを貼り、実行する
2. [**デバッグ**]→[**ウィンドウ**]→[**インディエイトウィンドウ**]で表示されたウィンドウに評価して欲しい関数や値を評価する。

では、イミディエイトウィンドウにどのようなことを書けばいいのかを紹介します。 
  
|タスク|ソリューション|例|   
|----|----|----|   
|式を評価する|先頭に(?)を付ける|?a+b|   
|コマンドを実行する|先頭に(>)を付けてコマンドを入力する|>alias|   
|コマンドウィンドウに切り替える|先頭に(>)をつけてcmdと入力する|>cmd|  
|イミディエイトウィンドウに戻る|immedと入力する|immed|  

このようにイミディエイトウィンドウの機能はそこそこ豊富である。
今のバージョンでは、(?)を付けなくても変数の中の値を表示してくれる。
しかし、もし(?)を入力しなかったときにエラーが出た場合は(?)を先頭につけて入力してみてほしい。

最後に   
わたしは、このレポートを通してデバックの機能の豊富さを感じた。
授業で、イミディエイトウィンドウや、データブレイクポイントなどの機能を教えてもらったときは、基本の機能しか知らなかったが、
このレポートを書くために調べることで、コマンドなどの機能を知ることができた。
知らないことや、調べた内容と自分の解釈が矛盾していた時に先生に聞くことで、もっとさらに奥底まで知ることができた。





