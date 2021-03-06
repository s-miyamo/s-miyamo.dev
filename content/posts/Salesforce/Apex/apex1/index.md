---
title: "Apex入門1"
date: 2021-01-11T22:02:19+09:00
---

## はじめに
この記事は、宮本が24歳の夏を共に過ごした、Salesforce内部で使用される「Apex」言語についてなるたけわかりやすく説明しようと試みたものです。
気が向いた時に加筆・修正をしていこうと思います。
対象は「Apex? ApexLegendsのことね。なるほどなるほど。」みたいな人を対象にしています。コーダ向けではありません。

## Apexとは？
まずApexとは何かを知りたい場合は、以下のURLを見てください。
https://developer.salesforce.com/docs/atlas.ja-jp.apexcode.meta/apexcode/apex_intro_what_is_apex.htm

Salesforce社の日本語ドキュメントは、機械翻訳なのか何か分かりませんが非常に癖があるように私は感じます。

## とりあえずHello World
百聞は一見にしかず、まずはApexを書いてみましょう。
そのために、まず個人で使えるSalesforce環境を手に入れる必要があります。
https://developer.salesforce.com/jpblogs/2016/04/developer-edition-signup/

この環境は一生を寄り添う伴侶とまではいきませんが、少なくともこの目まぐるしく変わっていく世の中を共に歩いていくパートナーと言えるでしょう。それくらい大事なのです。

環境を手に入れたら早速コードを書いてみましょう。右上にある歯車マークのボタンを押すと「開発者コンソール」がしれっと居るので、押してみましょう。

開くと以下のようなウィンドウが出てきます。おめでとうございます！これでApexを書く準備が整いました。環境を手に入れたあなたは鬼に金棒、どんな世界へも羽ばたいていけることでしょう。

![開発者コンソールを開く](apex1-02.png)

次に画面上部のDebug > Open Execute Anonymous Windowの順にボタンを押下します。
この「Anonymous Window」はApexコードを簡単に実行できる優れものです。これは非常に便利なので使えるようになりましょう。
なお、Ctrl+Eでも起動します。便利だね。
![apex1-06_anonymous](apex1-06_anonymous.png)

「Enter Apex Code」のウィンドウが出てくるので、以下のコードを入力し「Execute」ボタンを押下しましょう。
{{< highlight java "linenos=table" >}}
System.debug('Hello World');
{{< /highlight >}}

「Execute」ボタンを押下しても何も反応がありませんが、ご安心ください。
画面下部の「Logs」タブに何やらログが吐き出されているみたいなので開いて確認してみましょう。
ログをダブルクリックすると詳細が表示されます。
![apex1-07_logs](apex1-07_logs.png)

開いてみると難しそうなログがたくさん出力されています。
![apex1-08_logs2](apex1-08_logs2.png)

これでは分からないので、ログ出力エリアの下部にある「Debug Only」にチェックを入れてみましょう。
![apex1-09](apex1-09.png)

おお！「Hello World」と出力されているではありませんか！
ここまでできたあなたは最高です。これは小さなことに見えますが、あなたにとっては偉大な一歩です。

とはいえ、やはり文字を出力するだけでは味気ないのも事実です。
それならSalesforceっぽいことをしてみましょう。

## 顧客を作る
Apexは本来VisualForceのコントローラ（いずれ説明します）やバッチ処理を行うために使用しますが、
簡単なテストデータを作ったり、sandbox内のデータを更新したりする際にも活用できます。
例として、顧客（Account)を作成してみましょう。

先ほどの手順と同様に、Anonymous Windowを開いて以下のコードを入力し実行してみましょう。
{{< highlight java "linenos=table" >}}
Account acc = new Account();
acc.Name = 'フグ田 マスオ';
insert acc;
{{< /highlight >}}

実行を押下したら、Salesforceの画面に戻り、「取引先」タブを押下します。
リストビューを「すべての取引先」にして先ほど登録した「フグ田 マスオ」がいることを確認します。
![apex1-10](apex1-10.png)

![apex1-11](apex1-11.png)

見事に顧客を作ることができました！素晴らしいですね。
この3行だけで顧客を作成することができます。しかしこんな簡単なコードですが大事なことが詰まっています。

{{< highlight java "linenos=table" >}}
Account acc = new Account();
{{< /highlight >}}

上記は何をしているかというと、Account型のsObject変数「acc」を宣言して、新規作成したsObjectインスタンスを割り当てています。
いきなり訳の分からないワードが出てきました。のんびり、定年後の温泉休暇くらいのんびりやっていきましょう。

## sObjectの取り扱い

上記ではAccount型のsObject型変数を定義していますが、カスタムオブジェクトを使用することも可能です。
Custom型のsObject型変数を定義する場合は以下になります。

{{< highlight java "linenos=table" >}}
CustomObj__c cstm = new CustomObj__c();
{{< /highlight >}}

リストやマップといったコレクションにsObjectを格納することも可能です。
これは特に大事なことです。まずApexで大事なことはリストやマップにsObjectを格納できることを知っていることです。
次に大事なことは、リストやマップにsObjectを格納できることを知っていることです。
それくらい大事なことです。

{{< highlight java "linenos=table" >}}
List<Account> accList = new List<Account>();
{{< /highlight >}}

なぜここまで口酸っぱく言うのか、それはSOQLクエリの結果を格納したり一括処理の実行で多用するからです。
むしろこれを知らないと始まりません。ポケモンでマサラタウンから出ることが一生できないのと同じくらい始まりません。

SOQLの結果を直接格納することも可能です。
{{< highlight java "linenos=table" >}}
List<Account> accList = [SELECT id, Name FROM Account limit 100];
{{< /highlight >}}

以下のような使い方もできます。
{{< highlight java "linenos=table" >}}
List<Account> accList = new List<Account>();
Account acc1 = new Account(Name='Miyamoto');
Account acc2 = new Account(Name='Yamashita');
Account acc3 = new Account(Name='Takeuchi');

accList.add(acc1);
accList.add(acc2);
accList.add(acc3);

{{< /highlight >}}

上のような書き方が出来るならfor文もいけます。
{{< highlight java "linenos=table" >}}
List<Account> accList = new List<Account>();

for(Integer i = 0; i < 3; i++){
    Account acc = new Account();
    acc.Name = 'account' + i;
    accList.add(acc);
}

{{< /highlight >}}

sObjectの変数はそのままINSERTやUPDATEといったDML操作に渡すことができます。
{{< highlight java "linenos=table" >}}
Account acc = new Account();
acc.Name = 'sano';
insert acc;
{{< /highlight >}}

{{< highlight java "linenos=table" >}}
List<Account> accList = new List<Account>();

for(Integer i = 0; i < 3; i++){
    Account acc = new Account();
    acc.Name = 'account' + i;
    accList.add(acc);
}

insert acc;

{{< /highlight >}}

{{< highlight java "linenos=table" >}}
List<Account> accList = [SELECT id, Name FROM Account limit 100];
accList[0].Name = '変更する';
update accList
{{< /highlight >}}

{{< highlight java "linenos=table" >}}
List<Account> accList = [SELECT id, Name FROM Account limit 100];

for(Account acc : accList){
    acc.Name = '名前を変えちゃえ';
}
update accList;

{{< /highlight >}}

マップも使用できます。※超便利
{{< highlight java "linenos=table" >}}
Map<Id, Account> accMap = new Map<Id, Account>([SELECT id, Name FROM Account limit 100]);

for(Id key : accMap.keySet() ){
    Account acc = accMap.get(key);
    System.debug(acc);
}
{{< /highlight >}}

## ガバナ制限

Apexを用いてコードを書く際は、「ガバナ制限」を特に考慮する必要があります。
この「ガバナ制限」は、簡単に言うと「他の人も使っている環境でコードを動かすからあんまりピーキーなことすんなボケ」制限です。

Apexを使用する際、結構な頻度でオブジェクト（Oracleでいうテーブル）に対しての操作も行われる印象があります。つまり結構な頻度でガバナ制限と向き合うことになります。
このガバナ制限を考慮せずに書いたコードは、大半の確立で落ちるか上手く動きません。

https://developer.salesforce.com/docs/atlas.ja-jp.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_apexgov.htm

以下の記事のほうが僕よりわかりやすく、詳しく書いてあります。
気が向いたら宮本なりに書きますが、先ずは以下を参考いただいて...

https://qiita.com/comefigo/items/48f05d8fe4a3959911f4

## テストクラス

## Apexバッチ

この勢いのままコードを書いてみましょう。男と女のラブゲームと同じように、勢いが大事な時もあります。知りませんが。
File > New > Apex Classとボタンを押下すると「New Apex class」のウィンドウが出てきます。
![apex1-03](apex1-03.png)

「Please enter a name for your new Apex class」に「Batch_test」と入力し「OK」ボタンを押下します。
![apex1-03](apex1-04.png)

開くと以下の画像のような状態になっていると思います。
ここからコードを修正していきましょう。

