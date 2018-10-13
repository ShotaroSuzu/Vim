# Vimのキャッチアップメモ
## 概要
　テキストエディタの一種。  
　テキストの編集、検索などの強みを持っている。  
　様々なプラグインを追加することで、自分にあったカスタマイズができることが魅力  
　詳細についてはVimの日本語チュートリアルがあるので、そちらを参照。  
　[Vimチュートリアル（日本語）](https://vim-jp.org/vimdoc-ja/usr_01.html#tutor)  
## モードについて
　Vimの大きな特徴として、「モード」がある。  
　「モード」によって、キーボードからの入力をどのように扱うのかがきまるのだ  
　モードには大きく分けて３つ  
- ノーマルモード
- 挿入モード
- コマンドモード

　　これらを順に見ていこう  
#### ノーマルモード
　Vimを起動したとき、最初に表示さるのはノーマルモードだ。  
　ノーマルモードは、文字の検索をしたり、カーソルの異動をしたりすることができるモードのことを言う  
　このモードのとき、文字の削除はできるが追加はできない。  
　ここが初心者がVimに触れた時に戸惑う大きなポイントとなる部分だろう。  
　キーボードから入力した値は、何らかの操作としての意味を持つ。  
　例えば、h、j、k、lはそれぞれ左、下、上、右へのカーソル移動を意味していたりする。  

#### 挿入モード
　文字の追加、削除を行えるモードである。  
  ノーマルモードの時に、iを入力することで挿入モードに移行できる。  

#### コマンドモード
　Vimの文字の挿入以外の様々な操作を行えるモードである。  
　「:」ノーマルモードの時に、「:」を入力することでコマンドモードに移行する。  
　文字の検索だったり、ファイルの保存やVimから出るなど、文字の編集以外の様々な操作を行える。  
　プラグインを追加することで利用できるコマンドが増えたりもする。  

## プラグインについて
　Vimの便利さの一つとしてサードパーティのプラグインを利用できるところにある。  
　サードパーティのプラグインを管理するために、Vim用のプラグインマネージャーを利用するのが一般的なようだ。  
　現在ではVundleというプラグインマネージャーが人気があるようだ。  

### プラグインマネージャーのインストール
　では、実際にVimをインストールした直後に、Vundleを導入してみよう。  
　VundleはGitHubに公開されているため、[ここ](https://github.com/VundleVim/Vundle.Vim#quick-start)からアクセスする。  
　詳細は、Readmeに書いてあるが、以下の手順で行う。  
  1. Gitのインストールがされていない場合はGitのインストールを行う  
  2. Vundleの入手  

   ` git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim`

  3. プラグインの設定

  以下の設定を ' .vimrc ' に追加。

  ``` .vimrc
   set nocompatible
   filetype off
   set rtp+=~/.vim/bundle/Vundle.vim
   call vundle#begin()
   
   Plugin 'VundleVim/Vundle.vim'
   
   " 導入したいプラグインを以下に列挙
   " Plugin '[Github Author]/[Github repo]' の形式で記入
   Plugin 'airblade/vim-gitgutter'
   Plugin 'plasticboy/vim-markdown'
   Plugin 'kannokanno/previm'
   Plugin 'tyru/open-browser.vim'
   
   call vundle#end()
   filetype plugin indent on
   
  "　その他のカスタム設定を以下に書く
  ```

### プラグインの追加
　インストールが終わったら、次は練習のためにマークダウンのプラグインを追加してみよう。  
　マークダウンのプラグインはいろいろなものがあるようだが、[このQiita](https://qiita.com/iwataka/items/5355bdf03d0afd82e7a7)と[このブログ](をhttp://kaworu.jpn.org/vim/vim%E3%81%A7Markdown%E3%82%92%E3%83%97%E3%83%AC%E3%83%93%E3%83%A5%E3%83%BC%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95)を参考に、Markdown エディタのプラグインとプレビューのプラグインを追加してみる  
　Vundleのプラグインを記述するところに以下のプラグインを追記。
　
  ```.vimrc
   Plugin 'plasticboy/vim-markdown'
   Plugin 'kannokanno/previm'
   Plugin 'tyru/open-browser.vim'
   ```
   
   を記述してあげ、コマンドモードで ` :PluginInstall ` を実行してあげると、.mdの拡張子を持つファイルに、シンタックスハイライトなどを適用してくれる。  
   なお、デフォルトではMarkdownの見出しごとに折りたたむような設定が入っているため、無効にしたい場合は、以下を`.vimrc`に追記してあげればよい。  
   ```
   " 自動で折り畳まれないようにする
   let g:vim_markdown_override_foldtext = 0
   set nofoldenable
   ```

