# Android on CircleCI 2.0 Playground

* https://circleci.com/docs/2.0/language-android/
* http://in.fablic.co.jp/entry/migrating_to_circleci_2
* https://qiita.com/noboru_i/items/186e7b9dbb7925a7a226


## 暗号化したファイルをCI上で復号化する

* ハマったこと
 * ローカルPCでopenssl使って暗号化したけど、CI上にあるopensslとバージョンが違って復号化できない問題
 * ローカルPCのopensslのバージョン最新にしたほうがええで
 * 最新にしたら暗号化し直す
 * 復号に使うKeyはどうするの？ → CI上のEnvironment Variablesに設定
* https://qiita.com/smith_30/items/a275f30b040c1ea74520
* https://qiita.com/tomoima525/items/dbeeb6d451304333b17d
* https://qiita.com/yamacraft/items/771522138e9d8724c9ba
* https://qiita.com/noboru_i/items/687387148468e16c059a

```bash
# passは適用に打つ
# CircleCIのEnvironment Variablesに設定するので覚えておく
openssl aes-256-cbc -e -in private_properties -out encryptedProperties

# config.ymlの適当なところで以下っぽいこと書いて復号化する
# CIのEnvironment Variablesにdecryption_keyで復号に使う値を設定した場合を想定
openssl aes-256-cbc -d -k $decryption_key -in encryptedProperties -out private_properties
```