# 如何設置Github

接下來說明如何將local repository push上Github。
首先
## 建立新的Repo
到Github 個人頁面，並點New建立。
![建立Repo](./Github_Repo.png)

接下來可自由填入你想填的，你甚至想亂寫(不建議)都可以，記得最後按Creat Repository按鍵。

再來你會看到如圖
![建立Repo](./Github_initial%20page.png)
上面還有告訴你快速設定，但先不討論，我們要看的是SEt up in Desktop那一行，今天你可以用Github Desktop來做，但這裡主要提到用Terminal設置。


我們先複製後面的LINK，並到Terminal輸入
```bash
git branch -M main                                       
```
這個指令是將branch重新命名為main，
倘若出現
```bash
fatal: cannot rename the current branch while not on any 
```
代表你前面沒有切換回去，還在歷史存檔點(詳見上篇)，接下來輸入
```bash 
git remote add origin https://github.com/AZNitro/test.git
```
這時沒意外我們本地的Repo就連上github的remote repo了
接下來嘗試push看看
```bash
git push -u origin main
```
這時顯示
```bash
fatal: The current branch main has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin main

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.
```
這代表目前Github上的Repo沒有任何的上傳分支，要先設置main分支，倘若之後要自動上傳並設置好遠端分支，可到push.autoSetupRemote修改。

這邊我們先手動設置，請輸入
```bash
git push --set-upstream origin main
```
你會看到
```bash
PS C:\test> git push --set-upstream origin main
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 231 bytes | 231.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/AZNitro/test.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```
這時回到Github網頁上看，就成功push到remote repository了。
