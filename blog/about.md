---
title: loloicci.dev に関して
description: loloicci.dev の構成と GitHub Repository の紹介
author: loloicci
created_at: 2021-04-02
modified_at: 2025-12-08
robots: index,follow
---

### Flat File CMS
loloicci.dev は自作した Flat-File CMS で管理、生成しています。
CMS の開発言語は rust で、名前は "rustatto"。
Open にはしていないけど、気が向いたら準備して公開するかも。

### GitHub
文書ソースは大体が Markdown なので、CMS を通さなくてもそのまま読める + 編集も可能です。
どうせなら誤字脱字修正の PR が簡単に出せると便利かもしれないと思い、ソースを GitHub で公開してみます。

その他の本音としては、修正などに関するコメントを DB で管理するよりも、GitHub の Issue や PR で管理したほうが色々楽ができそうと考えたというのもあります。
各記事に Report Issue という節を設けているので、誤りに気づいた方は報告・修正していただけると嬉しいです。

### 余談
自分は学生時代から、自分用に色々な CMS を自作してきました。
このブログを管理している rustatto は 4 代目です。

始めて Flat-File CMS を作ったのは 5 年前 (3 代目) で、当時は Flat-File CMS なんて言葉が流行る前だったはず。
少なくとも私はその概念を知らずに CMS を作っていましたが、自分のサイト管理用には Git 一つあれば DB は要らないと考えていました。
その後 Flat-File CMS が流行っているのだから、間違いではなかったようで嬉しいです。

有名所の [grav](https://github.com/getgrav/grav) は 6 年前に公開されているので、私が初めて Flat-File CMS を作ったのと大体同時期らしいですね。
自分がこの概念・設計やソースの公開を行っていないのは、そういうところに関する自分の能力不足を痛感します。

### 余談2
CMS は 4 代目だと言いましたが、毎回、CMS を作っている時間よりも記事を書いている時間の方が短いです。
Utilities を作成するのは楽しいのですが、Production みたいなものを作成するのはそんなに好きじゃないという自分の性格が出ていますね。
