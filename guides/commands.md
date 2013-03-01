#[ Git ]


##基本コマンド

###gitリポジトリ作成

	$ git init



###現在の状態を見る
	
	$ git status
	
	
	
###インデックスに追加

	$ git add [ file name ] ([ file name ])



###ログを見る
	
	$ git log ([ file name ])
	$ git log --follow ([ file name ])



###コミット

	$ git commit -m "message"



###コミットの省略パターン

	$ git commit [ --all or -a ]
	


###rebase(過去のコミットをまとめる)

	$ git rebase -i HEAD~~



	
###ammend

	$ git commit --ammend
	

###revert

	$ git revert HEAD
	

###reset 

	$ git reset --hard HEAD~~
	
	
###reset前の状態へ戻す

	$ git reset --hard ORIG_HEAD
	

	
###cherry-pick

	git cherry-pick [ SHA1 ]
		
	
###ブランチの作成

	$ git branch [ branch name ]
	
	
###ブランチの切り替え

	$ git checkout [ branch name ]	


###ブランチの作成とチェックアウトを同時に行う
	
	$ git chechout -b [ branch name ]
	
	
	
###ブランチの一覧を見る

	$ git branch


###ブランチの削除

	$ git barnch -d [ branch name ]	
	
###マージ

	$ git merge [ branch name ]
	
	
	
###タグ

	$ git tag [ tag name ]

###注釈付きタグ

	$ git tag -a [ tag name ]
	
###注釈も一緒に指定

	$ git tag -am "[ meassage ]" [ tagname ]



###タグ一覧の確認

	$ git tag

###タグとメッセージを表示

	$ git tag -n
	
	
	

###詳細は decorate

	$ git log --decorate

	
###HEADの親の指定の仕方

	HEAD^^^
	HEAD~3
		
	
###ファイルの削除

	$ git rm [ file name ]
	$ git rm --cached [ file neme]
	$ git rm -f [ file name ]



###ファイル名の変更
（インデックスに追加している必要あり）
	
	$ git mv [ old name ] [ new name ]
	
 別パターン
 	
	$ mv [ old name ] [ new name ]
	$ git rm [ old name ]
	$ git add [ new name ]
	
	
	
###オブジェクトモデルの内側(SHA1)を見る

	$ git ls-files --stage
	($ git hash-object data)
	
	
	

###DIFF(納品ファイルの作成方法)
####現在のHEADecからのアーカイブ

	git archive --format=zip --prefix=<folder name>/ HEAD `git diff --name-only <commit name>` -o <zip name>.zip

####2つ前のHEADからのアーカイブ

	git archive --format=zip --prefix=<folder name>/ HEAD~~ `git diff --name-only <commit name>` -o <zip name>.zip
	
	
#####用語
- マージ: 複数の履歴の流れを行流させる ツリーの分岐は残したまま
- リベース: 複数の履歴の流れを合流させる ツリーを一本にする
- スタッシュ: 一時的に変更内容を記録し退避させる
