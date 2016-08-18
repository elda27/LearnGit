﻿#Learn Git 
## 初期化
まず，任意のディレクトリで以下のコマンドを実行し，gitリポジトリを初期化します．

`git init`

## 初めてのコミット
次に，適当なファイルを作成しそれをコミットします．  
今回は，"LICENSE"と"README．md"をそれぞれ別のコミットで追加していきます．
実行するコマンドは以下のとおりです．

`git add LICENSE`  
`git commit -m "[Add]:LICENSE"`  
`git add README．md`  
`git commit -m "[Add]:Add README"`  

ここで，`git add`は任意のファイルをバージョン管理に追加し，`git commit`で現状，追加されているファイルを記録します．  
その際，`-m`オプションを与えると，そのコミットに対してメッセージを入力することができます．  
できますと言っていますが，もし`-m`オプションを与えなくてもvimエディタが起動して，メッセージを入力する必要上がります．  
したがって，コミットメッセージが短文であれば`-m`，長文であればオプションなしを選べばよいでしょう．  

##Githubへのアップロード（リポジトリの作成）
ここまでの作業をgithubにアップロードします．
まず以下のコマンドを実行し，新たなリポジトリを作成します．

`git remote add <短縮名> <URL>`

ここで，URLですがgithubに新しいリポジトリを作りたい場合は以下のようになります．

`https://github.com/<ユーザー名>/<リポジトリ名>`

今回，私が作成するに本リポジトリを作成するうえで使ったのが以下のコマンド

`git remote add origin https://github.com/elda27/LearnGit`

ここでoriginはgitにおいて，デフォルトのリモートリポジトリの名前として慣例的に使われている名前なので，とりあえず最初に追加するリポジトリはこの名前にしておけばよいかと思います．  
もし，短縮名やURLを間違えた場合は以下のコマンドでリモートリポジトリを削除可能になっています．  

`git remote rm <短縮名>`

次にgithubのwebページからリポジトリを作成します．  
この時，リポジトリは初期化せずに作成すればよいかと思います．  
そして，以下のコマンドを実行して作成したリポジトリに初期化済みのリポジトリをpushします．  

`git push origin master`

なお，githubではpushに対して`-u`オプションが付いているかと思います．
これは，追跡設定といって，今後`git push`と実行するとリモートリポジトリと参照する対象をそれぞれ指定せずに実行すると常に`-u`オプションをつけて実行した時のpush先のリモートリポジトリと参照する対象が指定されるという機能です．

さて，ここまででgithubにローカルリポジトリの内容がアップロードされているはずなので確認しましょう．

## branchの作成
作成中のプログラムに対して新たな機能を追加したい時に複数人でそれにあたるためには，各機能ごとに複数のバージョンを保持する必要がある場合があります．
そのために，branchがあります．
まずbranchの作成には，以下のコマンドを実行します

`git branch <ブランチ名>`

でブランチが作成可能です．実際に"new-feature"という名前のブランチを作成するコマンドが以下のようになっています

`git branch new-feature`

実際にブランチを作成できているかの確認は，単に`git branch`と実行することで確認可能となっています．  
次にbranchを以下のコマンドで切り替えます．

`git checkout new-feature`

さて，ここまででbranchの切り替えを行いましたので，何か変更を加えて変更をpushまでしたいと思います．
リモートリポジトリへのpushは先に説明していますが以下のコマンドです．

`git push origin new-feature`

重要なところは，第三引数がmasterではなく，branch名である"new-feature"を選んでやるところです．


## branchのマージ
次に，これまでに作成したリポジトリをmasterブランチに統合します．  
まず，マージしたいbranchに切り替えます．

`git checkout master`

そして以下のコマンドを用いてnew-featureをmasterにマージします

`git merge new-feature`

するとファイルの内容が統合されているかと思います．

## rebase
マージの方法の一つとしてrebaseというものがあります．
通常のマージではマージしたという履歴が残りますがこちらでは，順当にコミットしていったという履歴に改ざんされてマージがなされます．
この方法の利点としては，ちょっとしたバグの修正の際，わざわざネットワーク履歴に残すほどではないけれどもバグを直すためにはブランチを切らねばならぬという時に便利でしょうね．

使い方は基本的にmergeと一緒．
今回はtest-rebaseというブランチを以下のコマンドで作ってやってから変更を加えます．

`git checkout -b test-rebase`

次にrebase先のブランチ，今回はmasterにチェックアウトして，以下のコマンドを実行するだけ．

`git checkout master
git rebase test-rebase
`
こうしてやるとマージを行うことができます．


