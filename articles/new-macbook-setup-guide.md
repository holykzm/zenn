---
title: "新しいMacBookを買ったら”絶対”すること"
emoji: "⚙️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["macOS", "vscode", "cli", "github", "homebrew"]
published: true
---

# 絶対必要

## Mac 自体の設定

#### 変換を Windows ライクに

1. 設定を開くか、`⌘` + `Space` で検索バーを表示
2. `language input methods` を検索
3. `Windows-like shortcuts` のチェックを入れる

![](/images/when-buy-new-macbook/1.png)

#### スクリーンショットの保存先を変更

1. `⌘` + `Shift` + `5` でスクリーンショット画面を開く
2. `Options`から`Other Location..`をクリックし、フォルダを指定する。

#### 隠しファイルの表示

1. `Finder`を開いて任意のディレクトリに移動する
2. `⌘` + `Shift` + `.` で表示

---

## CLI でのインストール

#### Homebrew

1. [公式サイト](https://brew.sh/ja/)に記載のコマンドでインストール
   ```
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
2. 途中で Warning が出る。
   ![=> Pouring portable-ruby-3.1.4.arm64_big_sur.bottle.tar.gz
Warning: /opt/homebrew/bin is not in your PATH.
Instructions on how to configure your shell for Homebrew
can be found
in the 'Next steps' section below.
==> Installation successful!](/images/when-buy-new-macbook/2.png)

   ![brew -v
-bash: brew: command not found](/images/when-buy-new-macbook/3.png)

3. パスを通す必要がある。

   ```
   ## zshを利用していない場合は、.bashrc または、.bash_profileを変更する
   vi ~/.zshrc

   ## 以下を追加して保存して閉じる
   export PATH=/opt/homebrew/bin:$PATH

   ## 設定を再読み込み
   source ~/.zshrc

   brew -v Homebrew x.0.0
   ```

#### GitHub CLI

1.  インストール
    `brew install gh`
2.  GitHub への SSH 接続を構築
    `gh auth login`
    ＊SSH を選択する。
3.  接続を確認
    `ssh -T git@github.com`
4.  `Hi {userName} ~`と表示されれば成功
5.  VScode でコミットするために ↓

```
git config --global user.name {ユーザー名}
git config --global user.email {メールアドレス}
```

# 個人的

## Mac 自体の設定

#### caps lock を言語切り替えに使う

1. 設定 or `⌘` + `Space`
1. 検索 `keyboard`
1. **Press 🌐 key to**を`Change Input Source`にする
   ![Change Input Source](/images/when-buy-new-macbook/4.png)

## CLI でのインストール

#### Node ([fnm](https://github.com/Schniz/fnm))

###### Fast Node Manager

1. インストール `brew install fnm`
2. `vi ~/.zshrc` で、**.zshrc** に`eval "$(fnm env --use-on-cd)"`を追加
3. 確認 `fnm -V`

###### NodeJS

1. インストールできる Node のバージョンを一覧表示 `fnm list-remote`
2. その中から Node のインストール `fnm install {version}`
3. セット `fnm use {version}`

---

#### Bun

1. [公式サイト](https://bun.sh/docs/installation)に記載のコマンドでインストール
   ```
   brew install oven-sh/bun/bun
   ```
2. 確認 `bun -v`

#### Rust

1. HomeBrew でインストール
   ```
   brew install rustup-init
   ```
2. `rustup-init`

   ```bash
   ~ % rustup-init
   Current installation options:
   default host triple: aarch64-apple-darwin
   default toolchain: stable (default)
   profile: default
   modify PATH variable: yes

   1) Proceed with installation (default)
   2) Customize installation
   3) Cancel installation
   1 // そのままEnterでも可

   ...
   ...
   ...

   Rust is installed now. Great!

   To get started you may need to restart your current shell.
   This would reload your PATH environment variable to include
   Cargo's bin directory ($HOME/.cargo/bin).

   To configure your current shell, run:
   source "$HOME/.cargo/env"

   ```

3. Path を追加

```

echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

```

4. Check

```

cargo --version

```

1. Uninstall

```

rustup self uninstall

```

## 公式サイトからインストール

個人的に必須のソフトをインストール

| 項目     | DL リンク／方法                           | 備考                      |
| -------- | ----------------------------------------- | ------------------------- |
| VScode   | https://code.visualstudio.com             | ⚠️ [設定](#vscode)        |
| Xcode    | https://developer.apple.com/jp/xcode/     |                           |
| Karabina | https://karabiner-elements.pqrs.org       | キーボード（Keycrone 用） |
| Clipy    | https://clipy-app.com                     | クリップボードの履歴      |
| Itearm   | https://iterm2.com                        |                           |
| Obsidian | https://obsidian.md/account               |                           |
| Figma    | https://www.figma.com/                    |                           |
| Chrome   | https://www.google.com/intl/ja_jp/chrome/ |                           |
| Docker   | https://www.docker.com/get-started/       |                           |

# Tips

### VScode

#### `code .`が使えない

1. Visual Studio Code を起動
2. コマンドパレットを開く `cmd` + `shift` + `p`
3. `"Shell Command: Install 'code' command in PATH"`を選択

#### Setting.json

1. Visual Studio Code を起動
2. コマンドパレットを開く `cmd` + `shift` + `p`
3. 検索 `setting.json
4.

```json
{
  "files.associations": {
    "*.css": "postcss"
  },

  "editor.defaultFormatter": "esbenp.prettier-vscode",

  "html.format.unformatted": "",

  "[typescriptreact]": {
    "editor.defaultFormatter": "rvest.vs-code-prettier-eslint"
  },

  "[jsonc]": {
    "editor.defaultFormatter": "vscode.json-language-features"
  },

  "editor.formatOnSave": true,

  "typescript.updateImportsOnFileMove.enabled": "always",

  "git.autofetch": true,

  "git.confirmSync": false,

  "[postcss]": {},

  "editor.accessibilityPageSize": 12,

  "editor.fontSize": 14,

  "terminal.integrated.fontSize": 14,

  "debug.console.fontSize": 14,

  "markdown.preview.fontSize": 16,

  "files.exclude": {
    "**/.git": false,

    "**/.svn": true,

    "**/.hg": true,

    "**/CVS": true,

    "**/.DS_Store": true,

    "**/Thumbs.db": true
  }
}
```
