# 如何安裝 Git 以及基礎設置

首先 Git 的安裝很簡單，只需要到 [Git 官方網站](https://git-scm.com/downloads) 下載選擇你要的版本即可。

這邊我個人使用 VSCode 作為我的主要 IDE，也可根據個人去做選擇，也有人推薦 Jetbrains 系列，聽說跟 Git 的整合更好，不過我 Surface 用起來會卡，就沒去使用了。

## 基礎指令

### 查看 Git 版本號

```bash
git --version
```

這個指令可以查看目前你安裝 Git 的版本是多少，以我的為例會顯示：

```bash
git version 2.49.0.windows.1
```

### 設置個人資料

設置名字以及 mail（YOUR_NAME 及 YOUR_DOMAIN 請記得更換）：

```bash
git config --global user.name 'YOUR_NAME'
```

```bash
git config --global user.email 'YOUR_NAME@YOUR_DOMAIN.com'
```

## What is Repository (Repo)

中文叫儲存庫，不太常聽到的詞彙，不重要。什麼是 Repo？你可以想像成一個資料夾存放你所有版本的程式碼，當一個資料夾被 Git 追蹤時，就可以稱它為一個 repo。

### 初始化 Git

```bash
git init
```

這時會回覆：

```bash
Initialized empty Git repository in C:/test/.git/
```

當看到這行時代表我們已經成功初始化 Git，並且建立一個 `.git` 的隱藏資料夾。你不須去碰此資料夾，裡面主要存放 commit 歷史、分支、遠端 repos 等。

這邊提個小插曲，現在初始化後都會是 `main` 這個 branch，以前會是 `master`，倘若要更改可以輸入：

```bash
git config --global init.defaultBranch main
```

**重要！** 更改完後記得重新初始化。

## 介紹 Branch 以及基本操作

前面提到我們已經成功初始化，接下來我們嘗試新增檔案看看。

假設我新增 test.md 檔案並在裡面隨便寫內容，寫完後請打：

```bash
git status
```

你會看到：

```bash
PS C:\test> git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.md

nothing added to commit but untracked files present (use "git add" to track)
```

由上而下看第一行：

```bash
On branch main
```

代表我們目前在 main 這個分支上，若顯示 master 或是其他，可以參照上方說明修改。

第二行：

```bash
No commits yet
```

代表目前未有任何 Commits，意即目前還未有任何存檔點。

第三行後：

```bash
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.md

nothing added to commit but untracked files present (use "git add" to track)
```

Git 預設不會去追蹤任何文件，需自己新增要追蹤的文件，可以打：

```bash
git add YOUR_FILE
```

也可以改成：

```bash
git add .
```

這會新增目前資料夾下所有未被追蹤的文件。`git add ./` 也有類似效果。

接下來是重點，請記得要 Commit，設置好存檔點，就跟遊戲一樣，沒有存檔你就得整個重來！

commit 指令為：

```bash
git commit -m 'message'
```

`-m` 後可以新增訊息，新增後顯示：

```bash
PS C:\test> git commit -m 'Add test.md'
[main (root-commit) 59cdc7f] Add test.md
 1 file changed, 1 insertion(+)
 create mode 100644 test.md
```

這樣就代表成功了。

接下來我們可以嘗試來看log紀錄，請打：

```bash
git log
```

會顯示：

```bash
commit 59cdc7ff76a7cea7edd26582a7ae4d0ae2517331 (HEAD -> main)
Author: AZNItro <86358964+AZNitro@users.noreply.github.com>
Date:   Sun May 18 15:50:22 2025 +0800

    Add test.md
```

這邊是我剛剛commit一次後所顯示的紀錄，第一行為commit id由Git自動生成，後面Author和Date則不多做贅述。

知道id對我們來說很重要，假設我們今天要回去看前面的版本，我們可以使用checkout這個command，使用它需要知道id，這裡填入我的id，同時Git也只需要前面幾個字符就可以抓到：

```bash
git checkout 59cdc7ff76a7cea7edd26582a7ae4d0ae2517331
# 或是簡短版本
git checkout 59cdc7f
```

會顯示：

```bash
Note: switching to '59cdc7ff76a7cea7edd26582a7ae4d0ae2517331'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 59cdc7f Add test.md
```

一句一句來看，首先是：

```bash
You are in 'detached HEAD' state. 
```

這段大意就是，你原本沿著一條路（分支）走，現在你跳到了路上的某一個點（特定的commit），但你並沒有站在任何一條已命名的路上。

```bash
You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.
```

這段代表你可以自由地查看該次commit的程式碼、進行實驗性的修改，甚至建立新的commit。這些新的commit是「匿名的」，它們不屬於任何現有的分支。

```bash
If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>
```

你在分離狀態下做了一些修改並且建立了新的commit，而你希望保存，你可以建立新的分支。

```bash
Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 59cdc7f Add test.md
```

你可以打 `git switch -` command 切換回上次的分支，算是很方便的command。同時如果你經常使用分離狀態，並且不希望每次都看到這段訊息，你可以透過設定 Git 的配置變數 `advice.detachedHead` 為 `false` 來關閉它。最後再次說明目前的 HEAD 正直接指向 commit `59cdc7f`。

講這麼多，到底有甚麼重點？
當你處於 `detached HEAD` 狀態時：
1.  你可以隨意查看歷史版本的程式碼。
2.  看完後，使用 `git switch main` (或你的主要分支名稱) 或 `git switch -` 切換回去。
3.  如果你在 `detached HEAD` 狀態下做了修改並 commit，記得使用 `git switch -c <新分支名稱>` 來建立一個新分支保存這些變更。否則，一旦切換到其他分支，這些在分離狀態下所做的提交可能會遺失。