#Git 心得

## Git 基本觀念
* 先用 add 將檔案放進 temp 概念的資料夾，進 stage 階段，再用 commit ，將 temp 資料夾改名為 Hash 亂碼，成為真正的新版本。
* 版本名稱會用 Hash 亂碼，避免版本名稱重複，例如：`888cee9cbe44dea043b4440c40717db716cfa0f6`
* git 可供遠端repo讓工作團隊下載，個人編輯後再上傳、合併。

![](https://backlog.com/git-tutorial/tw/img/post/intro/capture_intro1_2_2.png)

* git可提供不同版本提交的時間軸。

![git log](https://backlog.com/git-tutorial/tw/img/post/intro/capture_intro1_3_1.png)

###* 建立 Git ＆查看狀況
* 在資料夾內建立 Git 版本控制  
`git init`
* 刪除 Git 版本控制
`rm -r .git`
* 查看版本控制狀況
`git status`
```On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

###* add將檔案加入版本控制
`git add code.js`


加入所有檔案  
`git add .` 
```
➜ git:(master) ✗ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   code.js
	new file:   rock.txt
```

取消加入的檔案( unstage )，變成 untracked
`git rm --cached code.js`

###* commit 新建一個版本
`git commit -m "first commit"`

commit 出去之後代表已經建立一個新的 Git版本了，會存在 git log 裡面，可以查看歷史新建紀錄

###* 如何一個指令，新增所有的 modified 檔案 到 stage 並 commit 出去 (全新檔案不適用，會失敗)
`git commit -am
`
* 全新的檔案，需要先 add 到 stage 裡面，才能進行 commit -am



###* log 查看版本更新歷史紀錄
`git log`
``` 
commit 888cee9cbe44dea043b4440c40717db716cfa0f6 (HEAD -> master)
Author: 王茂己 <rock@wangjiajide-MacBook-Air.local>
Date:   Mon Jun 15 20:51:04 2020 +0800

    first commit
```
`git log --oneline` 簡短顯示歷史
```
888cee9 (HEAD -> master) first commit
(END)
```
###* diff ，在 commit 之前，查看這次 stage 裡的版本與上次的版本的差異
`git diff`
```
diff --git a/rock.txt b/rock.txt
index 4e1053c..062e147 100644
--- a/rock.txt
+++ b/rock.txt
@@ -1 +1 @@
-Code6
+Code4
(END)
```

###* checkout 回到過去
* 初始狀態( log )，有三次 commit 紀錄
```
commit 2d4ef193227d567d3c7df70c0721b8323a0e161c (HEAD -> master)
Author: 王茂己 <rock@wangjiajide-MacBook-Air.local>
Date:   Mon Jun 15 21:28:32 2020 +0800

    third commit

commit 1f9d406a9ea3665f5a36eb949cfead3e3e7640c0
Author: 王茂己 <rock@wangjiajide-MacBook-Air.local>
Date:   Mon Jun 15 21:27:53 2020 +0800

    second commit

commit 888cee9cbe44dea043b4440c40717db716cfa0f6
Author: 王茂己 <rock@wangjiajide-MacBook-Air.local>
Date:   Mon Jun 15 20:51:04 2020 +0800

    first commit
(END)
```
* 切換到第二次版本提交後的時間點
`git checkout 1f9d406a9ea3665f5a36eb949cfead3e3e7640c0 `
* 再看一次狀態
```
commit 1f9d406a9ea3665f5a36eb949cfead3e3e7640c0 (HEAD)
Author: 王茂己 <rock@wangjiajide-MacBook-Air.local>
Date:   Mon Jun 15 21:27:53 2020 +0800

    second commit

commit 888cee9cbe44dea043b4440c40717db716cfa0f6
Author: 王茂己 <rock@wangjiajide-MacBook-Air.local>
Date:   Mon Jun 15 20:51:04 2020 +0800

    first commit
(END)
```
* 是不是回到第二次的時間了！
* 如何回去：
`git checkout master`
* 就會回到最新的版本時間上了

###* .gitignore 將不想加入版本控制裡的檔案忽略( untracked )，例如系統內建執行檔
順序：
```
touch .gitignore
vim .gitignore
test //在vim編輯器裡面輸入檔名，例如test
git status  //🍵看檔案是否還被認為是需要被 add 的，
其實就是會剩下.gitignore被偵測到
```
------


## Branch 分支
* 建立一個新的 branch，例如：
`git branch week1[branch 名稱]`  。

* 切換 branch
`git branch checkout week1[branch 名稱]`。
* 查看目前在哪個 branch，例如：
`git branch -v`
```
  master 61fb6ac forth commit
* week1  61fb6ac forth commit
(END)
```

* 刪除 branch
`git branch -d week1[branch 名稱]`






## Merge 合併

在 master 分支，把另一個分支合併進來
`git merge test[分支名稱]`

------

## Conflict 衝突
想像一下，分別有Ａ檔案與Ｂ檔案，我們建立一個 new-feature 分支，在兩人操作不同分支的情況下，分兩種狀況：
1. 同事甲改Ａ檔案，同事乙改Ｂ檔案，兩人改完後 merge，天下太平！
2. 同事甲改Ａ、Ｂ檔案，同事乙改Ｂ檔案，兩人改完之後 merge，天下大亂！

在狀況2中，Git 的邏輯要怎麼解決呢？
按照時間嗎？先 Merge 的先贏？
也不行！

解決方法： **手動解決！**


例如：衝突發生，使用 merger 的時候 :
```
➜  git git:(master) git merge new-feature
Auto-merging code.js
CONFLICT (content): Merge conflict in code.js
Automatic merge failed; fix conflicts and then commit the result.
```
檔案會出現 :

```
<<<<<<< HEAD
@@@@@@@@@@@@@      //master branch
=======
!new feature       //another branch(new-feature)
>>>>>>> new-feature
```

這時就可以直接在這個檔案修改成你要的最終版本，
```
resolve conflict
@@@@@@@@@@@@@
!new feature
```
然後改完之後存檔，直接 commit :

`commit -am "resolve confilcts"`

就解決啦！







###* Push
![](https://backlog.com/git-tutorial/tw/img/post/intro/capture_intro3_1_1.png)

參考資料：[連猴子都能懂的 Git 入門指南](https://backlog.com/git-tutorial/tw/)