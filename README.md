POSTCODE API
====

インド版仕様
----

### リクエスト

GitHub PagesでJSONファイルを配信するという仕組みです。下記のようなURLにアクセスしてJSONを取得してください。インドの郵便番号の頭3桁に拡張子（.json）をつけてください。

https://yuigahamak.github.io/postcode/v1/in/744.json

GitHub PagesはCORS対応（？）なのでJSでブラウザから取得可能。レスポンスヘッダに下記の指定がある！

    access-control-allow-origin: * 

### レスポンス

JSONで以下のように返ってきます。頭3桁が同じ郵便番号がまとめて返ってきます。

{
    744301: [
        {
            address3: Sawai,	
            state: Andaman & Nicobar Islands,
            state_code: 01,
            district: Nicobar,
            district_code: 638,
            address1: Carnicobar,
            address2: "",
            latitude: 7.5166
            longitude: 93.6031
            accuracy: 4
        },
    ],
    744302: [],
    744303: [],
    credits: [
        {
            name: geonames,
            url: https://www.geonames.org
        }
    ],
    update: 2019-03-01 00:00:00
}

同じ番号でいくつもデータがあるのは元データの仕様です。最初のひとつを使ってください。JSだと下記のような感じで。getJSONは適当に実装してください。

    getJSON("https://yuigahamak.github.io/postcode/v1/in/744.json", function(json) {
        var address = json["744301"][0];
    });

インドの住所の仕組みがいまいち理解できず…。州（state）、県（district）まであるのはわかった。その下のaddress1、address2はよくわからんので使わない方が良いと思います。address2はだいたい空です。state_code、district_codeも元データにあるので入れましたが、正式なものではないと思うので、州や県にユニークなIDを持たせる以外の使い道はないと思われます。

### 元データ

元データは下記サイトから入手しました。

https://www.geonames.org

ライセンスはクリエイティブコモンズ3ということなのでクレジットを入れればOK！らしいのだがAPIにクレジットって？ということでJSONの中にクレジット入れてあります。

### データの更新

自動で更新とか実装してないので作者の気が向いた時にします（二度としないかも）。いつ作成したデータなのか一応JSONの中にupdateを入れてあります。現在のデータは2019-03-01に作成しました。
