---
title: "AirTest, Pocoを使ったUnity Appの自動テスト"
author:
  name: lee
date: 2024-03-18 18:30:00 +0900
categories: [Git]
tags: [自動タスと, Unity, ios, Android]
---

## 何ができる?

- Test Framework(Airtest+Poco)とpythonコードで、Unity アプリを自動テストする技術
- BlueStacks、Android、iosをサポート(iosの場合は、Apple製のバソコンが必要)

## テストプロジェットを実行

- Unityプロジェットダウンロードして、apkをBlueStacksや実機デバイスにインストール
  -[SampleProject](https://github.com/RiceUmai/airTest-poco-test)
    
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

## 実機動画
{% include embed/youtube.html id='3Xkd5EqhUtI' %}

## テストのレポート
{% include embed/youtube.html id='2UXcHy_2qw0' %}

## GitHub Link
- [AirTest](https://github.com/AirtestProject/Airtest)
- [Poco-SDK](https://github.com/AirtestProject/Poco-SDK)
## 公式ドキュメント
- [Airtest doc](https://airtest.netease.com/)
- [poco doc](https://poco.readthedocs.io/en/latest/source/doc/poco-example/basic.html)

## テストしたPythonコード
```py
# import unity poco driver from this path
from poco.drivers.unity3d import UnityPoco
import time
import sys

# -*- encoding=utf8 -*-
__author__ = "test"

from airtest.core.api import *
from airtest.cli.parser import cli_setup

if not cli_setup():
    auto_setup(__file__, logdir=True, devices=["android://127.0.0.1:{任意なポート番号}/127.0.0.1:{任意なポート番号}",])


# script content
print("start...")


# generate html report
# from airtest.report.report import simple_report
# simple_report(__file__, logpath=True)

poco = UnityPoco()

# ==========================
# ==========================
# GUI Demo uiのButtonを押す
newgame_btn = poco('Newgame', type='Button')
newgame_btn.click()

contunue_btn = poco('Continue', type='Button')
contunue_btn.focus('anchor').click()

settings_btn = poco('Settings', type='Button')
settings_btn.click()


# ==========================
# ==========================
# GameplaySetting PageのボタンとSliaderを操作
settings = poco('SettingsWindow')
settings.wait_for_appearance()

gameplay_btn = poco('Gameplay', type='Button')
gameplay_btn.click()

gamePlayWindow = poco('GamePlayWindow')
gamePlayWindow.wait_for_appearance()

settingsSlders = gamePlayWindow.offspring(type = 'Slider').child('Handle Slide Area')

for slider in settingsSlders:
    startSlide = slider.focus([0, 0.5])
    endSlide = slider.focus([1, 0.5])
    startSlide.drag_to(endSlide)    
    endSlide.drag_to(startSlide)


AOToggle = gamePlayWindow.offspring(type = 'Toggle').child('Checkmark')
AOToggle.click()
AOToggle.click()

close_btn = gamePlayWindow.child('Panel').child(type='Button')
close_btn.click()
gamePlayWindow.wait_for_disappearance()


# ==========================
# ==========================
# VideoSetting PageのボタンとSliaderを操作

video_btn = poco('Video', type='Button')
video_btn.click()
videoWindow = poco('VideoWindow')
videoWindow.wait_for_appearance()

videoSettingSliders = videoWindow.offspring(type= 'Slider').child('Handle Slide Area')

for slider in videoSettingSliders:
    startSlide = slider.focus([0, 0.5])
    endSlide = slider.focus([1, 0.5])
    startSlide.drag_to(endSlide)
    endSlide.drag_to(startSlide)
    
videoSettingToggles = videoWindow.offspring(type= 'Toggle').child('Checkmark')

for toggle in videoSettingToggles:
    toggle.click()
    toggle.click()

close_btn = videoWindow.child('Panel').child(type='Button')
close_btn.click()
videoWindow.wait_for_disappearance()

# ==========================
# ==========================
# AudioSetting PageのボタンとSliaderを操作

audio_btn = poco('Audio', type='Button')
audio_btn.click()

audioWindow = poco('AudioWindow')
audioSettingSliders = audioWindow.offspring(type= 'Slider').child('Handle Slide Area')

for slider in audioSettingSliders:
    startSlide = slider.focus([0, 0.5])
    endSlide = slider.focus([1, 0.5])
    startSlide.drag_to(endSlide)
    endSlide.drag_to(startSlide)
    
close_btn = audioWindow.child('Panel').child(type='Button')
close_btn.click()
audioSettingSliders.wait_for_disappearance()

# ==========================
# ==========================
#  Settingsページから出すボタンを押す
back_btn = poco('Back', type='Button')
back_btn.click()

```