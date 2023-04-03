---
title: "gitの複数のssh private Key運用"
author:
  name: lee
date: 2023-04-03 18:30:00 +0900
categories: [Git]
tags: [Git, SSH]
---

# 目的
* 2以上のssh Private Keyを登録して、それぞれのGitHubのRepositoryにAccessする方法

# ssh Config設定

```bash
* /.ssh/config
# work account
Host github.com-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_work

# me account
Host github.com-me
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_me
```

# Repository GitのConfig設定

```bash
* /.git/config
[remote "origin"]
url = git@github.com-work:"Repository URL"
# url = git@"ssh Config Host":"Repository URL"
fetch = +refs/heads/*:refs/remotes/origin/*

[user]
name = "UserName"
email = "Email"
```