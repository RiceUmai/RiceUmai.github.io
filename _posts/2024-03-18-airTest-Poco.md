---
title: "AirTest, Pocoを使ったUnity Appの自動テスト"
author:
  name: lee
date: 2024-03-18 18:30:00 +0900
categories: [Git]
tags: [自動タスと, Unity, ios, Android]
---

## 技術について

- Test Framework(Airtest+Poco)とpythonコードで、Unity アプリを自動テストする技術
- BlueStacks、Android、iosをサポート(iosの場合は、Apple製のバソコンが必要)

## テストプロジェットを実行

- Unityプロジェットダウンロードして、apkをBlueStacksや実機デバイスにインストール
    
    [poco-test-2.zip](https://prod-files-secure.s3.us-west-2.amazonaws.com/1be30fc7-a255-44c2-954a-9ed0fe1cd885/d03f70de-fef4-4843-9f4b-ebae7ddfe388/poco-test-2.zip)
    
- PCでAirtest IDE上で「poco-test-2/python」の中にいる「autoTest.py」を開く
- デバイスをAirtest IDEに接続
    - **BlueStacke**の場合は、
        - BlueStackeを実行する
        - Devicesのremote connection欄をチェックして、BlueStackeのADBアドレスを入力して、Connectを押す
        - pythonスクリプトの以下のコードにも、ADBアドレスを修正

        ```py
        if not cli_setup():
        auto_setup(__file__, logdir=True, devices=["andorid adb アドレス])
        ```
        ![Desktop View](/assets/img/connection.jpg){: width="700" height="400" }
        ![Desktop View](/assets/img/BlueStackADB.jpg){: width="700" height="400" }

        
    - **Androidの実機デバイス**の場合は
        - Androidのデバイスをusbで接続して、リストから、connectボタンを押す
        ![Desktop View](/assets/img/androidDevice.jpg){: width="700" height="400" }
        - 接続に成功したら以下のイメージになる
        ![Desktop View](/assets/img/connection12.jpg){: width="700" height="400" }
        - テストが終了した後、以下のアイコンを押すと、WebBrowserからテストレポートの確認ができる。
        ![Desktop View](/assets/img/report.jpg){: width="700" height="400" }