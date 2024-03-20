---
title: "ollamaとUnityの連動"
author:
  name: lee
date: 2024-03-19 15:00:00 +09:00
categories: [AI]
tags: [AI, Unity, Server]
---

## このアプリで何ができる?
* Unityアプリから、質問内容をLocalのChatBotサーバへ送るとサーバから返事を貰うことができる。

## 全体的な構造
![whimsical](/assets/img/Ollama-Unity/whimsical.JPG){: width="400" height="400" }

## 使用した機材、ソフト
1. OrangePi 5(メモリ8GB モデル)
2. Ollama, Docker
3. Ubuntu Server

## 実機動画
{% include embed/youtube.html id='X3Jx69wiGVk' %}

## メリット
1. ChatGPTみたいなサービスをlocal上で構築するのができる。

## デメリット
1. ChatBotサーバを構築したハードウェアの性能が低いので、サーバから返事を貰うまで、約２０秒以上かかる。
2. 日本語で答えると、返事のクオリティ低いので、まず、英語で翻訳して質問する必要があり、

## 今後にやりたいモノ
* 現在はUnityアプリから、ChatBotの連動のみになるが、今後はChatBotから返事した内容をAI TTSで読める機能を作りたい。

## 参考サイト
- [ollama-GitHub](https://github.com/ollama/ollama)
- [ollama公式サイト](https://ollama.com/)