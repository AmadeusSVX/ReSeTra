# ReSeTra 0.1

* ReSeTraはRealSense D4xxシリーズで動作する光学、距離値複合式の高速な簡易モーションキャプチャシステムです。
* VirtualMotionTrackerと組み合わせる事で、SteamVRに腰、左足、右足の3点のトラッカーを追加する事が可能です。
* Oculus Rift SやPCと接続したOculus Questで、簡易的なフルボディトラッキングが実現できます。

## 更新履歴
* 0.1 初版公開

## 動作環境
* Windows10 VR ready対応PC
* [ReSeTra](https://dummy)
* [VirtualMotionTracker](https://github.com/gpsnmeajp/VirtualMotionTracker) Segmentation Fault氏作 
* [SteamVR](https://store.steampowered.com/app/250820/SteamVR/)
* Oculus Rift SもしくはOculus Quest（Oculus LinkあるいはVirtual Desktopでの接続）
 * **WindowsMRでは現状可視光カットフィルタが別途必要（要検証）。HTC Vive、Valve Indexでは未検証**
* Intel RealSense D415/D435/D435i/D455のいずれか (D455を推奨 [参考](https://store.intelrealsense.com/products.html?product_list_order=price))
* RealSense接続用の長めのUSB-Cケーブル（USB3接続必須 3m程度を推奨 [参考 ※未検証](https://www.amazon.co.jp/gp/product/B081N1W39Y/)）
* メンディングテープ ([参考](https://www.amazon.co.jp/dp/B0013N1VCO/))
* 反射マーカー x3 (自作できます。次節参照)

## 反射マーカーの作成
### 準備する物<br>

![マーカーの材料](/images/markerkit.png)

* ピンポン玉　（ガチャポンの球形空カプセルでも可） : [参考URL1](https://www.amazon.co.jp/dp/B073WDYLJK/) [参考URL2](https://www.amazon.co.jp/dp/B00MX2FNTG/)
* 再帰性反射テープ　： [参考(※未検証注意)](https://www.amazon.co.jp/dp/B00762A3LG/)
* リストバンド　：　伸縮性のあるゴムバンド
* 穴あけ用のドリルもしくはキリ
* 裁縫道具

### 作成方法

1. ピンポン玉に再帰性反射テープを貼ります。底面になる部分は穴を開けるため開けておきます。<br>
![テープ貼り付け](/images/taping.png)
1. ピンポン玉に穴を4つ開けます。ガチャポンの空カプセルには予め穴が開いている物もあるので、そちらを使うと労力を減らせます（※ただし球形の物を選ぶ必要があります）<br>
![底面に穴あけ](/images/drilling.png)
1. ボタンを縫い付ける要領でリストバンドに縫い付けます ([参考](https://kaden.watch.impress.co.jp/docs/column/lifestyle/1161391.html)) 。ただし、糸足を作る必要はありません。<br>
![縫い付け](/images/sewing.png)
1. 3つ作れば完成です。お疲れさまでした!<br>
![完成](/images/completemarker.png)

## セットアップ
1. SteamVRをPCにインストールします<br>
1. VirtualMotionTracker(VMT)をインストールします。ファイルコピー後、SteamVRが起動可能な状態(=Rift SもしくはQuestが接続された状態)でvmt_manager.exeを起動してください。起動後、「Install」タブ内のInstallボタンを押してドライバのインストールを行ってください。その後SteamVRを再起動して、SteamVRの通信をファイヤウォールの設定で許可してください ([VMT公式解説はこちら](https://github.com/gpsnmeajp/VirtualMotionTracker/blob/master/docs/howto.md))<br>
1. RealSenseの赤外線プロジェクタにメンディングテープを貼付します<br>
![プロジェクタ上にテープを張り付け](/images/tapedprojector.png)
1. RealSenseを設置します。USB-CケーブルでPCと接続して、ユーザーが立つ位置の真正面に下半身が視界に入るよう配置してください。<br>
1. 反射マーカーを装着します。お腹にはバンドの中にベルトを通してあげると固定しやすいです。<br>
![身体にマーカー装着](/images/bodymarker.png)<br>
1. RealSenseの正面に立って、ReSeTraを起動します。初回起動時はファイヤウォールの許可画面が出ると思いますが、許可してください。右のBody points画像で、Waist, L Foot, R Footが各位置にそれぞれ対応していれば成功です。<br>
![アプリケーションウィンドウ](/images/appwindow.png)
1. 背景の他の物に誤対応している場合は、IR imageで検出の様子（検出領域が矩形で囲まれます）を見ながら、背景の反射物を片づけたり、窓からの太陽光を遮るなどの対策を行ってください。<br>
1. 対策後、Binalize thresholdの値を変化させてみてください。基本的に大きい値にすると誤検出は減少します。その反面、検出したマーカーがロストしやすくなります。<br>
1. もしWaist, L Foot, R Footの対応がおかしい場合は、Reset Indexを押して対応付けをリセットしてみてください。リセットでロストした場合は、再びthresholdの値を変えて調整してください。<br>
1. 安定して3点を検出できるようになったら、三点がなす三角形が地面に垂直になるように頑張って立って、Zero setボタンを押してください。押した位置が初期位置=原点になります。<br>
1. SteamVRを起動します。<br>
1. ReSeTra側のStart VMTボタンを押して位置の送信を開始します。SteamVRのウィンドウにVMTのアイコンが3つ現れたら正常に動作しています。<br>
![SteamVRウィンドウ](/images/steamvr.png)
1. HMD側の原点も同じ位置で正面を向いてリセットしてください（Oボタン長押し）。ReSeTra側の初期位置はZero set後に固定されるので、その位置に合うようにHMD側でリセットを行います。<br>
これで完了です。**2回目以降の使用では5.～13.の手順になります。一度設定が決まれば7.～9.もほぼ省略可能です(つまり5. 6. 10.～13.のみ)。良いフルトラライフを！**<br>

## トラブルシューティング・FAQ
**ReSeTraが起動しない**<br>
→USB3で接続されている事を確認してください。[RealSense Viewer](https://github.com/IntelRealSense/librealsense/releases/download/v2.38.1/Intel.RealSense.Viewer.exe)を使えば、現在繋がっているRealSenseがUSB3接続かどうかを確認できます。もしUSB2.xで接続されている場合は、RealSenseのファームウェアを最新に更新する、ケーブルをつなぎ直す、USB-Cコネクタの向きを変える、ポートを変える、ケーブルを変えて見るなどの対策を行い、USB3での接続を確認後に上記の6.の手順に戻ってください。

**SteamVRがエラーを起こしてVMTプラグインが無効化されてしまう**<br>
→SteamVRの起動前にReSeTra側からVMT向けデータの送信を始めると正しく起動しなくなります。ReSeTra起動直後はVMTへの送信を開始せず、上記手順の11.と12.の順序を守って再度試してみてください。

**プレイ時にWaist, L Foot, R Footの対応がおかしくなって戻らない**<br>
→RealSenseの真正面に立って、Reset Indexボタンを押すことで対応付けのリセットが可能です。また、VRアプリケーションの体験中でボタンを押すのが困難な場合は、正面に立った状態で3つのうちのマーカーの2つを手や他の部位で隠して一度ロストさせてみてください。対応付けが自動的にリセットされます。

## 免責事項
* 本アプリケーションに発生した不具合について、本アプリケーション開発者は一切の修正・改善の義務を負いません。
* 本アプリケーションの使用、または使用時の不具合等に伴って生じた損害について、本アプリケーション開発者は一切の責任を負いません。
