---
title: "Apex入門1"
date: 2021-01-11T22:02:19+09:00
---

### はじめに
この記事は、宮本が24歳の夏を共に過ごした、Salesforce内部で使用される「Apex」言語についてなるたけわかりやすく説明しようと試みたものです。
気が向いた時に加筆・修正をしていこうと思います。
対象は「Apex? ApexLegendsのことね。なるほどなるほど。レイスたんちゅっちゅ」みたいな人を対象にしています。コーダ向けではありません。

### Apexとは？
まずApexとは何かを知りたい場合は、以下のURLを見てください。
https://developer.salesforce.com/docs/atlas.ja-jp.apexcode.meta/apexcode/apex_intro_what_is_apex.htm

Salesforce社の日本語ドキュメントは、機械翻訳なのか何か分かりませんが非常に癖があるように私は感じます。

### とりあえずHello World
百聞は一見にしかず、まずはApexを書いてみましょう。
そのために、まず個人で使えるSalesforce環境を手に入れる必要があります。
https://developer.salesforce.com/jpblogs/2016/04/developer-edition-signup/

この環境は一生を寄り添う伴侶とまではいきませんが、少なくともこの目まぐるしく変わっていく世の中を共に歩いていくパートナーと言えるでしょう。それくらい大事なのです。

環境を手に入れたら早速コードを書いてみましょう。右上にある歯車マークのボタンを押すと「開発者コンソール」がしれっと居るので、押してみましょう。

![開発者コンソールを開く](apex01-1.png)


### Apex

Apexを用いてコードを書く際は、「ガバナ制限」を特に考慮する必要があります。
この「ガバナ制限」は、簡単に言うと「他の人も使っている環境でコードを動かすからあんまりピーキーなことすんなボケ」制限です。

Apexを使用する際、結構な頻度でオブジェクト（Oracleでいうテーブル）に対しての操作も行われる印象があります。つまり結構な頻度でガバナ制限と向き合うことが


このガバナ制限を考慮せずに書いたコードは、大半の確立で落ちるか上手く動きません。




- ガバナ制限
- sObjectの取り扱い
- sObjectとコレクション
- テストクラス