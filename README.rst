================
筆記區
================

學習歷程筆記，期望對其他人也能有一些基礎知識的幫助，


如有錯誤或指教，歡迎寄信至 < sunaaronxp@gmail.com >

----





.. contents:: 目錄





Git push
==================

事前準備 :

註冊 `GitHub<https://www.github.com>`帳號

安裝 git
    
:: 

    sudo apt install git
    sudo dnf install git

接著到自己的 github 上創建一個新專案，

這邊要注意的是，

存取權如果選擇 Public 那麼是可以免費使用的，

但是如果選取 Privte 是必須每月付費的。


回到本身 Terminal

建立本機的資料夾

::

    mkdir 資料夾名稱
然後進入到資料夾

::

    cd 資料夾名稱
初始化這個資料夾

::

    git init
如果出現 Initialized emptyGit repository in xxx/xxx/xxx.git

代表成功初始化這個資料夾

現在你可以把檔案丟進這個資料夾

這邊先假設從0開始

建立空白檔案

::

    touch index.html

這時在 git 上輸入 ls

即可看到檔案夾內有什麼檔案

查詢哪些檔案還沒被 git 追蹤

::

    git status
把檔案加入到 git 

::

    git add 檔案名稱
這時再下一次 git status 的指令

就可以看到剛剛的檔案 git 已經追蹤可以 commit

每次檔案的變動如何去自動比較

::

    git diff

如果是舊檔案更動，再更動完後

可以用下面指令新增 commit 訊息

::

    git commit -a
使用 git lg 就可以看到多了一條最新的 commit






















