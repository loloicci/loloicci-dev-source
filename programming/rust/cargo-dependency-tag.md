---
title: |
  cargo dependency: version のみでは main branch 以外にある tag を指定できない
description: Cargo.toml の dependency で version を指定する場合の注意点。version が指す tag が main branch にない場合には指定できない。また、その解決策について。
author: loloicci
created_at: 2021-04-10
modified_at: 2021-04-12
robots: index,follow
---

```Cargo.toml
[dependency]
package = { git = "...", version = "0.2.0" }
```

で version を指して依存クレートを指定する場合、version tag のついた commit は main branch 中になくてはならないらしい。(2021/04/10 現在)

また、main branch 以外にある tag を指定する方法についても記述する。

### 現象例
main branch にない version が指定できないことと、その時のエラーを見ていく。

https://github.com/loloicci/cargo-single-package を依存クレートとして使用する。このクレートは
- v0.1.0 が branch: master に存在
- v0.2.0-alpha と v0.2.0 が branch: prerelease に存在
している。
こんな状況は github flow で開発を行っていたらまず起こらないわけだが、git flow とかで開発しているとたまに起こり得る。
github flow でも、v0.2.0 をリリースした後に v0.1.1 を作ったりすると起こりそう。

また、このクレートを使用するクレートの名前を cargo とする。

```Cargo.toml
[dependency]
cargo-single-package = { git = "https://github.com/loloicci/cargo-single-package", version = "0.2.0" }
```

`cargo check` を実行。

```shell
$ cargo check
    Updating git repository `https://github.com/loloicci/cargo-single-package.git`
error: failed to select a version for the requirement `cargo-single-package = "^0.2.0"` 
  candidate versions found which didn't match: 0.1.0
  location searched: Git repository https://github.com/loloicci/cargo-single-package.git
required by package `cargo v0.1.0 (/Users/loloiccl/Work/rust/cargo)`
```

エラーメッセージは stable, nightly ともに同じ。

「[ワークスペース](https://doc.rust-jp.rs/book-ja/ch14-03-cargo-workspaces.html) にいくつかクレートが含まれていてそのうちひとつに依存して……」とかをやりだすと、version によってエラーメッセージが変わってくるようだが、ここでは省略。
(今回の個人的ハマりポイントはここだった)

### 解決策
main branch に存在していない tag を指定する方法もしっかり存在している。

#### version と branch を併記する
~~version tag の含まれている branch 指定してやると、しっかりと tag を探してきてくれる。~~  
branch での指定は branch の head の commit hash を rev として指定した時の挙動と同様らしい。
そのため、以下の方法では version 0.2.0 は指定できても version 0.2.0-alpha は指定できない。

```Cargo.toml
[dependency]
cargo-single-package = { git = "https://github.com/loloicci/cargo-single-package", version = "0.2.0", branch = "prerelease" }
```

~~で依存解決できる。~~  
素直に tag を直接指定しよう。

#### tag を直接指定する
実は cargo は tag を直接指定することもできる。

```Cargo.toml
[dependency]
cargo-single-package = { git = "https://github.com/loloicci/cargo-single-package", tag = "v0.2.0" }
```

同様に rev ~~, branch (version を指定しない場合は branch の head を使用)~~ も使用できる。
