# 限界集落 MC Server

ピスタチオゲーム部の自前マイクラサーバー「限界集落」です。

どなたでもご自由に入って遊んでいただければとおもいます。

JAVA & BE(統合版) どちらも入れます。

## Spec

- JAVA 版 MINECRAFT LATEST
	- JAVA 版ですが BE 版 も入れます
- メモリ
	- 4G
	- `docker-compose.yml` の `services.mc.environment.MEMORY` で定義してます

## 導入プラグイン

- GeyserMC
    - https://ci.opencollab.dev/job/GeyserMC/job/Geyser/job/master/
- Floodgate
    - https://ci.opencollab.dev/job/GeyserMC/job/Floodgate/job/master/
- ProtocolLib
    - https://www.spigotmc.org/resources/protocollib.1997/
- LWC Extended
    - https://www.spigotmc.org/resources/lwc-extended.69551/
- Hidden Armor
    - Dependencies
        - ProtocolLib
    - https://www.spigotmc.org/resources/hidden-armor.100374/
- Dynmap
    - https://dev.bukkit.org/projects/dynmap/files

### プラグインの追加 & 導入方法

**リモートサーバーの場合**
1. 必要なバージョンの jar ファイルをダウンロード
1. scp でファイルをremoteにコピー
    - `scp {target_file} {server}:{hogehoge}/genkai-mc-server/data/plugins`
    - target_file: コピーしたいファイル
    - server: 接続先情報(.ssh/config に定義した名前も使える)
    - hogehoge: 自分がマイクラサーバーをインストールした場所
1. リモートサーバー上の不要なプラグインファイルを削除
1. マイクラサーバーを再起動
    - `make up`


## Commands

make がない場合は、Makefile の中身を読んで定義されているコマンドを実行してください

Init
```shell
# minecraft-log-forwarder などのセットアップ
export DISCORD_WEBHOOK_URL=YOUR_WEBHOOK_URL
./setup.sh

# サーバーの起動
make up
```

バージョンアップ
- `docker-compose.yml` の `services.mc.environment.VERSION` を更新してリスタートすると指定したバージョンに変更されます
- デフォルトでは LATEST を指定してあるので最新版になります
```
make up
```

サーバー停止
```
make stop

or

make down
```

## Data Directory

https://github.com/itzg/docker-minecraft-server#data-directory

## TODO

### High
- [x] dynmap の https 化
- [x] サーバーアイコンの設定
- [ ] サーバーの定期再起動設定
- [ ] 自動定期バックアップ
	- 参考: https://github.com/sksat/mc.yohane.su
- [x] ~~tkm999からOP権限を剥奪~~
- [ ] 全員寝なくても過半数が寝たら朝になるように設定変更
- [x] 旧サーバーからのデータ移行
- [x] set `server-icon.png`
- [ ] plugins
	- [x] GeyserMC
	- [x] Floodgate
	- [x] LWC Extended
	- [x] Hidden Armor
		- [ ] ProtocolLib エラー調査(@zztkm だけかも)
			- https://www.spigotmc.org/resources/protocollib.1997/
	- [x] Dynmap
- [x] mc server log forwarder
	- https://github.com/MICKeyzwo/minecraft-log-forwarder
- [ ] 権限管理 (`/dmarker`など)
- [x] BE版のスキン適用
### Mid
- [ ] ログイン前のチャット表示 ChatReplay導入 (参考: https://seesaawiki.jp/perominecraft/d/ChatReplay)
- [ ] 初期リスでの サーバー説明
- [ ] 再起動10分前くらいにチャットでアナウンスを表示「10分後サーバーが自動再起動されます」のような文言
### Low
- [ ] 拠点の保護機能
- [ ] Discordでの現在オンラインのプレイヤー数表示 (参考: https://github.com/ZixeSea/ServerStats)
- [ ] plugins のインストールスクリプト
	- 導入したいプラグインをインストールするスクリプトを作成する

## 謝辞

サーバーの設定やスクリプトなど色々参考にさせていただきました。

- [sksat/mc.yohane.su](https://github.com/sksat/mc.yohane.su)

## 参考

- https://github.com/itzg/docker-minecraft-server#versions
