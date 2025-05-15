# 如何安裝Git以及基礎設置

首先Git的安裝很簡單，只需要到
`https://git-scm.com/downloads`下載選擇你要的版本即可。

這邊我個人使用Vscode 作為我的主要IDE，也可根據個人去做選擇，也有人推薦Jetbrains系列，聽說跟Git的整合更好，不過我Surface用起來會卡，就沒去使用了。

## 基礎指令

### 查看Git版本號
```bash
git --version
``` 
這個指令可以查看目前你安裝Git的版本是多少，以我的為例會顯示
```bash
git version 2.49.0.windows.1
```

### 設置全局個人資料

設置名字以及mail  
YOUR_NAME及YOUR_DOMAIN請記得更換
```bash
git config --global user.name 'YOUR_NAME'
```
```bash
git config --global user.email 'YOUR_NAME@YOUR_DOMAIN.com'
```

## What is Repository(Repo)
中文叫儲存庫，不太常聽到的詞彙，不重要，什麼是Repo?你可以想像成一個資料夾存放你所有版本的程式碼，當一個資料夾被Git追蹤時，就可以稱它為一個repo。  


初始化Git
```bash
git init                               
```
這時會回覆
```bash                             
Initialized empty Git repository in C:/test/.git/
```
當看到這行時代表我們已經成功初始化Git，並且建立一個`.git`的隱藏資料夾。
你不須去碰此資料夾，裡面主要存放commit 歷史、分支、遠端 repos 等。   

這邊提個小插曲，現在初始化後都會`main`這個branch，以前會`master`，倘若要更改可以輸入  
```bash
git config --global init.defaultBranch main
```
重要!!:更改完後記得重新初始化。

## 介紹Branch以及基本操作(暫定)
前面提到我們已經成功初始化，接下來我們嘗試新增檔案看看。
假設我新增test.md檔案並在裡面隨便寫內容，寫完後請打
```bash 
git status
```
你會看到
```bash
PS C:\test> git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.md

nothing added to commit but untracked files present (use "git add" to track)
```
由上而下看第一行
```bash
On branch main
```
代表我們目前在main這個分支上，若顯示master或是其他，可以參照上方說明修改。  

第二行
```bash 
No commits yet
```
代表目前沒有

