================
筆記區
================

學習歷程筆記，期望對其他人也能有一些基礎知識的幫助，


如有錯誤或指教，歡迎寄信至 < sunaaronxp@gmail.com >

----





.. contents:: 目錄





Git
==================
這是一種版本控制的系統, 不論是不是工程師, 我們每次工作都會有新的進度, 
對檔案修修改改的, 如果是團隊作業, 大家修改的地方不一樣, 如何讓大家的東西最後可以統一,
Git 是一款分散式的版控系統 (Distributed Version Control) 雖然通常也會有共同的伺服器, 
但即使在沒有伺服器或是沒有網路的環境, 依舊可以使用 git 來進行版控, 
待伺服器恢復正常運作或是在有網路的環境後再進行同步, 不會受影響。

而且, 事實上在使用 Git 的過程中, 大多的 Git 操作也都是在自己電腦本機就可以完成。

Git 指令
--------------------

 ``$ git init`` 在要建立數據庫目錄的位置, 進行版本控制

 ``$ git add <檔案名稱>`` : 追蹤檔案或目錄到索引, 可以直接指定檔案名稱, 可以將檔案註冊到索引, 如果加上 -p 參數, 可以只選擇修改檔案的一部分, 
 -i 參數, 會以互動的方式詢問要註冊在索引的檔案

 ``$ git commit`` : 可以提交新的索引到檔案, 添加 -a 參數, 就可以檢測出有修改的檔案(不包括新增的檔案), 將其加入索引並提交, 添加 -m 參數, 
 就可以指令提交 "提交指令" , 不添加 -m 參數, 就會啟動修改提交訊息的編輯器

 ``$ git status`` : 顯示修改檔案的清單, 加上 -s 參數, 僅會顯示已修改的檔案名稱, 
 如果在 -s 後再加上 -b 的參數, 則會顯示分支的名稱

 ``$ git diff`` : 查看修改檔案的差異, 加上 --cached 參數, 會顯示索引與 HEAD 之間的差異

 ``$ git log`` : 顯示提交紀錄, 如果是 ``git lg`` 就是簡單版

 ``$ git mv <原本的檔案名稱> <新的檔案名稱>`` : 修改/移動一個檔案/目錄名稱

 ``$ git rm <檔案>`` : 刪除檔案

 ``$ git checkout -- <檔案>`` : 還原在工作目錄已更改的檔案

 ``$ git reset HEAD -- <檔案>`` : 刪除已追蹤到索引的檔案

 ``$ git add -u`` : 只追蹤已提交過的檔案到索引


Git push
--------------------

事前準備 :

註冊 `github <http://www.github.com/>`_ 

安裝 git
    
:: 

    sudo apt install git
    sudo dnf install git

接著到自己的 github 上創建一個新專案, 
這邊要注意的是, 存取權如果選擇 Public 那麼是可以免費使用的, 
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

代表成功初始化這個資料夾, 
現在你可以把檔案丟進這個資料夾, 
這邊先假設從0開始, 

建立空白檔案

::

    touch index.html

這時在 git 上輸入 ls , 即可看到檔案夾內有什麼檔案


查詢哪些檔案還沒被 git 追蹤

::

    git status


把檔案加入到 git 

::

    git add 檔案名稱

這時再下一次 git status 的指令, 就可以看到剛剛的檔案 git 已經追蹤可以 commit , 


每次檔案的變動如何去自動比較

::

    git diff

如果是舊檔案更動，再更動完後, 可以用下面指令新增 commit 訊息

::

    git commit -a

使用 git lg 就可以看到多了一條最新的 commit




Personal web backend building
==============================

須知
-------------------
要架設一個網站, 我們可以間單的說需要兩種服務,
一個是資料存放的地方, 一個是網域。

資料存放可以把它想像成我們需要一個雲端硬碟來存資料, 
而網域可以當作是你的網頁的一個地址或一個門牌

網域
-------------------
網域大部分並非免費, 需要到網路上網域註冊商購買,
這裡推薦給大家 `godaddy <https://tw.godaddy.com/>`_ , 
在哪裡買的都可以, 網路上也會有零星的免費網域提供可以去申請, 
不過穩定性較低, 故暫不考慮。

資料存放
------------------
需要一個雲端上可以存放資料的地方, 雲端服務幾乎都是要收費的,
最近 Google 有一個 `Google Cloud Plarfrom <https://cloud.google.com/gcp/?hl=zh-tw&utm_source=google&utm_medium=cpc&utm_campaign=japac-TW-all-zh-dr-bkws-all-super-trial-e-dr-1003987&utm_content=text-ad-none-none-DEV_c-CRE_263264845604-ADGP_Hybrid%20%7C%20AW%20SEM%20%7C%20BKWS%20~%20T1%20%7C%20EXA%20%7C%20General%20%7C%201:1%20%7C%20TW%20%7C%20zh%20%7C%20cloud%20platform%20%7C%20google%20cloud%20platform%20%7C%20en-KWID_43700031884576410-kwd-26415313501&userloc_9040379&utm_term=KW_google%20cloud%20platform&gclid=Cj0KCQjwjtLZBRDLARIsAKT6fXy56R0dHDS-kpBk7NrELQwv4flOnQ9sGDCCJUXwqwtKoran5T4n7zIaAnbGEALw_wcB&dclid=CMC9g4aY9tsCFcezlgodWUkCMQ/>`_ , 
提供了一年的免費試用服務, 對於初學者來說簡直是個福音, 
上面不單單是提供資料的存放, 還有很多而外的服務 虛擬主機、App Engine 之類的,
有興趣的朋友可以自行去玩玩看其他功能。

DNS
------------------
首先我們要把網域和資料做連結前, 我們需要先了解一下 DNS ,

網域名稱系統 ( Domain Name System , 縮寫 DNS):

它是網際網路的一項服務, 將域名和 IP 位置相互對應的一個分散式資料庫, 目前對於每一級域名長度的限制是 63 個字元,
域名總長度則不能超過 253 個字元。

DNS系統中常見的資源紀錄類型

* **A** 紀錄 : 將 IP 位址連接主機名稱
* **CNAME** 紀錄 : 一個主機允許擁有一個以前的DNS
* **mx** 紀錄 : 確定電郵會傳送到正確位置
* **NS** 紀錄 : 含有名稱伺服器的資料
* **TXT** 紀錄 : 提供有關主機的額外資訊, 或提供更多伺服器的技術資料
* **SRV** 紀錄 : 尋找託管特定服務的電腦
* **AAAA** 紀錄 : 提供不合標準 A 紀錄的 IP 位址
* **SPF** 紀錄 : 用來防止垃圾郵件

Google Cloud Plarfrom
--------------------
由於自己本身是使用 Google Cloud Plarfrom 作為資料存放,
故以下用此作為範例, 

首先我們登入 Google Cloud Plarfrom 後,  在頁面左上角有個下拉式箭頭, 
開啟後會請你選取專案, 我們按右上角的新增專案, 後面輸入你自己的專案名稱, 位置選擇無機構,

這時會跳回剛剛的首頁, 可以看到剛剛的下拉式箭頭已經多了一個我們剛剛創建的新專案, 
我們由左上角的選單尋找 **Storage** , 並選到**瀏覽器**, 然後創建一個 Bucket, 

這裡要特別注意!! 使用上會有費用的差別 ( Google 有提供一年免費和300美金試用 )

* 名稱須與你的網域相同, 前面加 www. (就是未來要給 user 連線的網址相同, 例: www.xxxxx.xxx)
* 在你建立 Bucket 名稱, Google 會要求你證明網域所有人是你, 或到 `Google Search Console <https://www.google.com/webmasters/tools/home?hl=zh-TW/>`_ 進行認證
* 預設儲存空間級別, 建議選擇 Regional , 當然有其他不同級別可供不同用途選擇, 這邊架設網頁 Regional就夠了
* 位置選擇只要是 aisa 都可以

接著就可以選擇你喜歡的方式上傳檔案, 接著記得把後面的公開共用的公開連結打開, 
你按下公開連結的超連結, 就可以看到你的網頁呈現了, 
但是可以注意到網址的部分是由 Google 提供的,
下篇會教使用 DNS 連結你的資料與網域

網站架設 (資料與網域連結)
-------------------------
個人是使用 GoDaddy 購買網域, 下面用這個當範例

先到 GoDaddy , 進到會員中心, 接著按左上角**網域管理員**的下拉式選單, 
選到網域, 頁面跳轉後對著自己網域名稱點進去( 請注意並非是 *使用我的網域* ), 
移至頁面最下的其他設定中點選管理 DNS , 這邊我們就可以看到一些 GoDaddy 為我們設定好的紀錄, 
先解釋右下角的轉址, 意思為當有 user 連結到此網域, 自動跳轉連結到你指定的網域, 
這時我們先回到 Google Cloud Plarfrom , 一樣在左邊的選單中找到 **網路服務** -> **Cloud DNS** , 
按下建立區域

* 區域名稱可以取自己喜歡的, 並無影響
* DNS 名稱請取自己買下網域的名稱 ( 例 : xxxxx.xxx )

創建完, 進入看到 Google 幫你產生了兩個紀錄, NS 紀錄跟 SOA 紀錄, 
這是給我們連結網域跟資料使用的, 回到 GoDaddy , 
看到網域名稱伺服器的地方, 按下變更 選擇自訂, 
把剛剛 Google 幫你產生四條的 NS 紀錄貼過來,
這邊要注意貼過來的時候, 記得把末端的點給 dele 掉, 
儲存後回到 Google Cloud Plarfrom 的 DNS 這, 
在紀錄集的地方按下新增紀錄集, DNS 名稱請取跟你 Bucket 一樣的名稱,
資源紀錄類型選擇 CNAME , 正式名稱請打 ``c.storage.googleapis.com.`` , 
這樣我們就已經完成設定了, 不過需要等待 30 分鐘更新, 
更新完成後就可以到你的網域看到你的網站拉, 不會再是 google 所提供的網域。

Django
=====================

Django 是一種網頁框架, 目前有許多的框架可供套用, Django 只是 Python 框架的其中一種, 
主要用於用來支援動態網站、網路應用程式及網路服務的開發, 
這種框架有助於減輕網頁開發時共通性活動的工作負荷, 例如許多框架提供資料庫存取介面、標準樣板以及會話管理等, 
可提昇程式碼的可再用性。


install
---------------------

先確認電腦是否已安裝 Django , 在 Terminal 輸入

::

    $ python -m django --version

如果 Django 已經被安裝了, Terminal就會顯示目前的版本


Step 1.  確認 Pyhon 版本

::

    python --version


Step 2.  確認 PiP 版本

::

    pip --version


**如果尚未安裝, 請至官網安裝或用 terminal 安裝**


Step 3.  使用 pip 安裝 Django


::

    sudo pip install Django



開始 Django 專案 
------------------------ 

打開 Terminal , cd 進 Desktop 或任何想要存放檔案的位置

::

    django-admin.py startproject mysite

就可以看到有一個名為 test 的檔案夾已經創建完成, 裡面已經自動創建了相關的網頁架構文件

 - 最外層的 mysite 檔案夾, 它跟 Django 無相關, 可以命名為任何你想要的名稱
 - manage.py : 是一個 command-line , 可以讓我們以各種方式與此 Django 互動, 可以在 `django-admin and manage.py <https://docs.djangoproject.com/en/2.0/ref/django-admin/>`_    看到更多的詳細資訊
 - 檔案夾內的 mysite 是 Pyhon 的 package , 它的名稱是用來導入內容的 (例如 : mysite.urls )  
 - mysite/settings.py : 儲存 Django 的配置和設置
 - mysite/urls.py : Django 的 URL , 顯示 Django 所連結網站的目錄
 - mysite/wsgi.py : 與 WSGI 兼容的 Web 服務器的入口點 


接著使用 Terminal 進入 mysite 檔案夾後, 輸入

::

    python manage.py runsever



可以看到 Terminal 中顯示 

``Starting development sever at http://127.0.0.1:8000/``

``127.0.0.1`` 意思等同於 ``localhost`` , 
這時在瀏覽器上輸入 ``http://localhost:8000`` 或 ``http://127.0.0.1:8000`` , 
就可以看到自己的網頁。

Django 本身有一個很實用的命令, 請確保在 ``manage.py`` 的檔案位置

::

    $ python manage.py startapp polls

你就可以在該位置看到, 它自動幫你生成了一個名為 polls 的資料夾

現在, 打開 mysite/settings.py , 這是個包含了 Django 項目設置的 Python 模塊。
這個配置文件使用 SQLite 作為默認數據庫, 如果你不熟悉數據庫, 或者只是想嘗試下 Django, 
這是最簡單的選擇。 Python 內置 SQLite，所以你無需安裝額外東西來使用它。
當你開始一個真正的項目時, 你可能更傾向使用一個更具擴展性的數據庫, 例如 PostgreSQL, 
避免中途切換數據庫這個令人頭疼的問題。

如果你想使用其他數據庫，你需要安裝合適的 database bindings , 
然後改變設置文件中 DATABASES 'default' 項目中的一些鍵值：
 - ENGINE -- 可選值有 'django.db.backends.sqlite3' , 'django.db.backends.postgresql' , 
 'django.db.backends.mysql' , 或 'django.db.backends.oracle' , 其它可用後端。

 - NAME - 數據庫的名稱。如果使用的是 SQLite，數據庫將是你電腦上的一個文件，在這種情況下， NAME 應該是此文件的絕對路徑，包括文件名。默認值 os.path.join(BASE_DIR, 'db.sqlite3') 將會把數據庫文件儲存在項目的根目錄。
 如果你不使用 SQLite，則必須添加一些額外設置，比如 USER 、 PASSWORD 、 HOST 等等。想了解更多數據庫設置方面的內容，請看文檔：DATABASES 。


Exprees 
==================

install
------------------

假設已安裝 Node.js , 請建立目錄來保留您的應用程式, 並使它成為的工作目錄

::

    $ mkdir myapp
    $ cd myapp


使用 npm init 指令, 為應用程式建立 package.json 檔, 如需 package.json 如何運作的相關資訊, 
請參閱  `Specifics of npm’s package.json handling <https://docs.npmjs.com/files/package.json/>`_ 

::

    $npm init

這個指令會提供一些事項, 例如：應用程式的名稱和版本。現在, 只需按下 RETURN 鍵, 接受大部分的預設值, 但下列除外：

::

    entry point: (index.js)

輸入 app.js , 或所要的主要檔名稱。如果希望其名稱是 index.js , 請按 RETURN 鍵 , 接受建議的預設檔名。
現在, 將 Express 安裝在 app 目錄中, 並儲存在相依關係清單中。例如：

::

    $ npm install express --save

如果只想暫時安裝 Express , 而不新增至相依關係清單, 請省略 --save 選項：

::

    $ npm install express


基本路由
-------------------

路由是指判斷應用程式如何回應用戶端對特定端點的要求, 
而這個特定端點是一個 URI（或路徑）與一個特定的 HTTP 要求方法(GET、POST 等), 
每一個路由可以有一或多個處理程式函數, 當路由相符時, 就會執行這些函數。

路由定義的結構如下：

::

    app.METHOD(PATH, HANDLER)

其中

 - app 是 express 的實例
 - METHOD 是   `HTTP 要求方法 <https://zh.wikipedia.org/wiki/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE/>`_
 - PATH 是伺服器上的路徑
 - HANDLER 是當路由相符時要執行的函數

下列範例說明如何定義簡單的路由

首頁顯示 Hello World! :

::

    app.get('/', function (req, res) {
    res.send('Hello World!');
    });

對根路由 (/)（應用程式的首頁）發出 POST 要求時的回應 :

::

    app.post('/', function (req, res) {
    res.send('Got a POST request');
    });

對 /user 路由發出 PUT 要求時的回應 ：

::

    app.put('/user', function (req, res) {
    res.send('Got a PUT request at /user');
    });

對 /user 路由發出 DELETE 要求時的回應 ：

::

    app.delete('/user', function (req, res) {
    res.send('Got a DELETE request at /user');
    });



























