#Git 本日のまとめ

##開発運用での注意点
公開用ブランチと作業用ブランチを分ける。

* 公開用ブランチ：master
* 作業用ブランチ：dev,develop,developmentなど

これの意図することは、  
masterは、公開状態を常に保持し、  
devは、開発の最新版を常に保持することで、  
それぞれのブランチをきれいに保つことを目的とします。  

公開用ブランチで作業してはいけない、テストアップFix後、作業用ブランチからマージしてくる。  
ブランチの分岐もとは、なるべく上記ブランチから生成するようにする。


##復習コマンド
###ブランチ
####生成
	## 生成のみ
	$ git branch <branchname>
	## 生成とcheckout
	$ git checkout -b <branchname> [<start point>]
	

####削除
	$ git branch -d <branchname>


###インデックス
####追加
	$ git add .


####追加更新
	$ git add -u
	
***注意点***  
Git管理下にあるファイルの内、変更点のあるものだけをステージに追加します  
すなわち新規ファイルはステージしない。


####個別の削除
	$ git rm --cached <filename>
	## または、
	$ git reset <filename>


####事前のadd自体の取り消し
	$ git reset HEAD
	


###コミット
####コメント付きコミット
	$ git commit -m "<str>"
	

####事前のコミットの打ち消し
	$ git reset <mode> HEAD~~
	
**モード(デフォルトは、mixed)**

mode　　　　　|HEAD        | インデックス     | ワークツリー
:----------- |:----------- | :-----------: | -----------:
--sort       |変更する      | 変更しない      | 変更しない
--mixed      |変更する      | 変更する        | 変更しない
--hard       |変更する      | 変更する        | 変更する


#### 統合(3つ前までのリビジョン)
	$ git rebase -i HEAD~~~
	
その後、vim起動

	pick xxxxxxx コメント１
	pick xxxxxxx コメント２
	pick xxxxxxx コメント３ 最新のコミット

pickをaquash

	pick xxxxxxx コメント１
	aquash xxxxxxx コメント２
	aquash xxxxxxx コメント３ 最新のコミット
	
保存・終了(:wq!)  
その後統合したコメントが再びvimが起動するので適宜対処(コメントの書き換え)して終了


#### 修正
	$ git rebase -i HEAD~
	
その後、vim起動

	pick xxxxxxx コメント１

pickをedit

	edit xxxxxxx コメント１
	
保存・終了(:wq!) そのコミット 

	$ git commit --amend -m "<comment>"
	
最後にこのコミットの作業が終了したことを知らせる。
	
	git rebase --continue
	
#### rebase中止
	git rebase --abort	



###差分
####ワークツリーとインデックス
	$ git diff
	

####個人リポジトリの最新のcommitとワークツリー
	$ git diff HEAD
	
	
####個人リポジトリの最新のcommitとインデックスに記録した状態との
	$ git diff --cached
	

####コミット間の差分を表示
	$ git diff HEAD^..HEAD
	
####コミット間の差分ファイル名のみ
	$ git diff --name-only <commit> <commit>
	
	## filterで検索
	## D:追加、C:コピー、A:削除、M:更新、R:リネーム、
	## T:チェンジ、U:マージされてない、X:不明、B:壊れた
	$ git diff --diff-filter=DCAMR --name-only <commit> <commit>

###アーカイブ
####差分ファイル抽出
	$ git archive --format=zip --prefix=projectname/ HEAD `git diff --name-only <commit>` -o archive.zip
	
**TODO:**  
deleteファイルがあるとエラーを起こすので引き続き調査が必要

以上が、今日の内容だと思います。