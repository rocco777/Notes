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

增加上傳位置(網址為 github 上, 該專案的上傳網址, origin 是可以替換的名稱)

::

    git remote add origin 網址

驗證是否完成設定, 可以輸入 ``git remote``  ``git remote -v`` 一個是顯示名稱, 一個是詳細內容, 
而輸入 ``git remote show origin`` 會讓程式真的去訪問伺服器的狀態

設定 push 的路徑 ( -u 是為了設定本地端版本, 永遠跟著伺服器上的, 所以下次 push 不用打 ``git push origin master`` , 直接輸入 ``git push`` )

::

    git push -u origin master

輸入後他會要求輸入你 Github 的帳號, 接下來是打密碼, 成功驗證會顯示 ``* [new branch]   master  ->  master`` , 
這樣以後要 push 上去, 只要輸入 ``git push`` 即可。` 








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


安裝
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
 如果你不使用 SQLite，則必須添加一些額外設置，比如 USER 、 PASSWORD 、 HOST 等等。
 想了解更多數據庫設置方面的內容。


Exprees 
==================

安裝
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


在 Express 中提供靜態檔案
--------------------------

如果想在 Express 中使用靜態的檔案, 只要將檔案傳遞給 express.static 中介函數, 即可。

在名為 **public** 的資料夾中, 提供靜態檔案 :

::

    app.use(express.static('public'));

載入位於 public 資料夾目錄中的檔案 : 

::

    http://localhost:3000/picture.jpg
    http://localhost:3000/images/picture.jpg
    http://localhost:3000/html/myweb.html


而這個中介函數是可以多是使用, 在你要使用多個靜態檔案資料夾時 :

::

    app.use(express.static('public'));
    app.use(express.static('video'));

如果要為 express.static 函數提供的檔案, 建立虛擬路徑字首, 為檔案指定裝載目錄 : 

::

    app.use('/static', express.static('public'));

現在就可以透過 /static 路徑, 來載入 public 目錄中的檔案 : 

::

    http://localhost:3000/static/picture.jpg
    http://localhost:3000/static/images/picture.jpg
    http://localhost:3000/static/html/myweb.html

但是如果你是想從額外的資料夾, 執行 Express 應用程式, 請使用絕對路徑 : 

::

    app.use('/static', exprss.static(__dirname + '/public'));


中介軟體
----------------------------

Express 是一個本身功能極簡的路由與中介軟體 Web 架構：本質上，Express 應用程式是一系列的中介軟體函數呼叫。
中介軟體函數是一些有權存取要求物件 (req)、回應物件 (res) 和應用程式要求/回應循環中之下一個中介軟體函數的函數。
下一個中介軟體函數通常以名為 next 的變數表示。
中介軟體函數可以執行下列作業：

 - 執行任何程式碼
 - 對要求和回應物件進行變更
 - 結束要求/回應循環
 - 呼叫堆疊中的下一個中介軟體函數

如果現行中介軟體函數不會結束要求/回應循環, 它必須呼叫 next(), 以便將控制權傳遞給下一個中介軟體函數。否則, 要求將會停擺。
使用 app.use() 和 app.METHOD() 函數, 
將應用程式層次的中介軟體連結至 app object 實例, 
其中 METHOD 是中介軟體函數要處理的 HTTP 要求方法(例如 GET、PUT 或 POST), 並採小寫。

如果現行中介軟體函數不會結束回應循環, 它就會需要使用 next() , 以便將控制傳遞給下一個中介軟體, 否則, 要求將會被停止。

使用 app.use() 和 app.METHOD() 函數, 將應用程式層次的中介軟體至 app object , 
其中METHOD 是中介軟體函數處理 HTTP 要求的方法 (例如 GET PUT POST), 

顯示沒有裝載路徑的中介函數, 每當應用程式收到要求時, 就會執行此函數 : 

::

    var app = express();


    app.use(function (req, res, next)) {
      console.log('Time : ', Date.now());
      next();
    })

顯示裝載在 /user/:id 路徑的中介軟體函數, 會對 /user/:id 路徑上任何類型的 HTTP 要求, 執行此函數 : 

::

    app.use('/user/:id', function (req, res, next) {
      console.log('Request Type : ', req.method);
      next;
    });

顯示路由和其處理函示函數(中介軟體系統), 此函數會處理指向/user/:id 路徑的 GET 要求 : 

::

    app.get('/user/:id', function (req, res, next) {
      res.send('USER');
    });


Exprees 自動產生器
--------------------------

使用應用程式產生器工具 express , 快速建立應用程式架構

使用下列指令來安裝 express :

::

    npm install express-generator -g

使用 -h 選項可以顯示指令選項

在現行工作目錄中建立一個名為 myapp 的 Express 應用程式 :

::

    $ express --view=pug myapp


        create : myapp
        create : myapp/package.json
        create : myapp/app.js
        create : myapp/public
        create : myapp/public/javascripts
        create : myapp/public/images
        create : myapp/routes
        create : myapp/route/index.js
        create : myapp/route/user.js
        create : myapp/public/stylesheets
        create : myapp/public/stylesheets/style.css
        create : myapp/views
        create : myapp/views/index.pug
        create : myapp/views/layout.pug
        create : myapp/views/error.pug
        create : myapp/bin
        create : myapp/bin/www

在安裝相依的項目(先 cd 進要的資料夾) : 

::

    $ cd myapp
    $ npm install

在 MacOS 或 Linux 中, 使用下列指令來執行應用程式 :

::

    $ DEBUG=myapp: * npm start

在 windows 中, 使用下列指令來執行應用程式 :

::

    $ DEBUG=myapp: * & npm start

然後在瀏覽器中載入 ``http://localhost:3000/`` , 以存取應用程式

錯誤處理
----------------------

錯誤處理中介軟體函數的定義方式, 與其他中介軟體函數相同, 
差別在於錯誤處理函數的引數是四個而非三個：(err, req, res, next)

::

    app.use(function(err, req, res, next) {
       console.error(err.stack);
       res.status(500).send('Something broke!');
    });

您是在定義其他 app.use() 和路由呼叫之後, 最後才定義錯誤處理中介軟體

::

    var bodyParser = require('body-parser');
    var methodOverride = require('method-override');

    app.use(bodyParser());
    app.use(methodOverride());
    app.use(function(err, req, res, next) {
    });

中介軟體函數內的回應可以是任何喜好的格式，如：HTML 錯誤頁面、簡式訊息或 JSON 字串。
為了方便組織(和更高層次的架構), 可以定義數個錯誤處理中介軟體函數, 
就像處理一般中介軟體函數一樣。
舉例來說, 如果想為使用及沒有使用 XHR 所建立的要求, 各定義一個錯誤處理程式, 可以使用下列指令：

::

    var bodyParser = require('body-parser');
    var methodOverride = require('method-override');

    app.use(bodyParser());
    app.use(methodOverride());
    app.use(logErrors);
    app.use(clientErrorHandler);
    app.use(errorHandler);








        
MongoDB
======================

MongoDB 是一個基於分布式文件儲存的數據庫。旨在為 WEB 應用提供可擴展的高性能數據儲存解決方案。


安裝
----------------------

先更新 Homebrew 套件 : 

::

    brew update

安裝 mongodb : 

::

    brew install mongodb

之後需等待一段時間, 安裝完成後, 在使用前還要先建立資料庫存放的目錄, 
預設的資料庫存放路徑 ``/data/db`` : 

::

    mkdir -p /data/db

建立好目錄後, 確認一下這個目錄可以被執行 ``mongod`` 的使用者存取, 
可能會需要用管理者權限修改一下這個目錄的擁有者, 最後再用擁有者的權限來啟動 ``mongod`` : 

::

    mongod

如果安裝的 MongoDB 是自己開發或測試用的話, 建議可以把資料庫放在自己的主目錄下, 
然後用自己的權限來執行 ``mongod`` 即可, 省去處理檔案權限的麻煩。

::

    mkdir -p ~/data/db
    mongod --dbpath ~/data/db


Mongoose
--------------------

使用 npm 安裝 : 

::

    npm install mongoose


連結 MongoDB :

如何連結檔案, 首先先 import 套件, 其中 ``./testDBService`` 是路徑, 請依照自己設定的路徑設置, 
而 ``testDBService`` 是我們自己寫的一個函式, 用於確認是否有連線成功(意思是 import 了自己的另一個檔案) :  

::

  let mongoose = require('mongoose');
  let testDBService = require('./testDBService');

schema 為模板, 就是往後的資料存入要依照什麼格式, 哪些規則去使用, 以下面例子就是資料需要有 userName 跟 pass , 
而 pass 並不是必要資料可有可無, 因為可以看到再 userName 的下面多了兩個規則,  ``required`` 意思為是不是必須的, 
userName 設定為 true , 故每筆資料輸入都需要有這個欄位的資料,  ``unique`` 意思為是不是唯一, 
就是這筆資料能不能以同個名稱重複創建, 這裡設定為 ture 必須是唯一, 故資料輸入不得重複名稱 : 

::

    mongoose.connection.once("open",function(){
        var schema = mongoose.Schema({
            userName: {
                type: String,   
                required:true,  
                unique:true  
            },
            pass:{
                type:String
            }
        });
    }

接著我們要創建一個 table 分類這些資料, User 那個欄位就是為資料分類創建的名稱, 跟要分發的類別, 
這樣丟的資料都會丟到名為 User 的分類下 :

::

    let users = mongoose.model('User', schma);

接著把資料專門拉出來, 以後找資料或是要做處理都會比較方便 : 

::

    testDBService.testUserModel(user);


我們為了要讓其他的檔案可以使用這個函式, 所以我們要把檔案傳出去, 這時我們就要使用 exports ,
以後其他檔案要使用就 require 即可 : 

::

    exports.mongoose_connect = mongosse_connect;

附上完整程式碼 :

::

    let mongoose = require('mongoose');
    let testDBService = require('./testDBService');

    function mongoose_connect () {
        try{
            mongoose.connect('mongodb://localhost:27017/test')
        }catch(error){
            console.log(error)
        }
        mongoose.connection.once("open",function(){
            var schema = mongoose.Schema({
                userName: {
                    type: String,   
                    required:true,  
                    unique:true  
                },
                pass:{
                    type:String
                }
            });
            let users = mongoose.model('User', schema);
            testDBService.testUserModel(users);
        }).on('error',function(err){
            throw err
        })
    }
    
    exports.mongoose_connect = mongoose_connect;



    --------------------------------------------------

    testDBService的程式碼 : 

    let mongoose = require('mongoose')
    let userModelInService = "";

    function testUserModel(userModel){
        userModelInService = userModel;
        console.log("waduhek ", userModelInService);
    }

    exports.testUserModel = testUserModel;

創建一個可以讓前台跟後台拿資料的 API ,   ``.create`` 是建造存取資料, 
並且在創建成功或失敗 print 出相對印的結果, 用於確認程式狀態, 
最後一樣別忘記 export 檔案出去, 這樣前台才可以使用(這部分的程式寫在後台的文件裡) :  

::

    function create(user) {
    userModelInService.create(user, (err, result)=>{
        if(err){
            console.log("create err occur ", err);
        }else{
            console.log("create success");

        }
    }

    exports.createUser = create;

接下來在前台的文件中, 我們要去使用剛剛後台寫好的 API , 不過因為在練習沒有數據, 
故我們在上面先 let 一個數據用於練習,  ``fetch`` 是 RESTful API 的管道, 
mathhod 是要使用的方法, body 中的 ``stringify`` 用途是把 JSON 格式的資料轉換成為字串節省空間, 
header 先不理他, 就是一個 Tittle , 最後一樣錯誤處理, 用於瞭解程式狀態 : 

::

    let createUserURL = "http://localhost:3000/users/test";


    function createUser(){
    let userData = {
        userName: "dandan",
        pass: "Waduhek"
    } 

    fetch(createUserURL, {
        method: 'POST', 
        body: JSON.stringify(userData),
        headers: new Headers({
            'Content-Type': 'application/json'
        })
    }).catch(error => console.error('Error:', error))
    .then(response => console.log('Success:', response));
    }


前後台溝通流程
---------------------

首先在我們讓 Express 框架自動產生後, 可以看到 bin 檔案夾底下有一個 www 的檔案, 
而這份 ``./bin/www/`` 就是啟動其他檔案的文件 (其他文件包括 app.js  router 之類的), 
其中 app.js 檔案, 裡面寫了我們的 router , 接下來因為要操作 mongodb 所以要使用套件 mongoose , 
使用 schema 去創造 table , 最後在 user.js 補上 router 路徑, 使其正確啟動。  


獲取使用者鏡頭
========================

先提供 javascripts 的 程式碼 :

::

    navigator.getUserMedia = (navigator.getUserMedia ||
    navigator.webkitGetUserMedia ||
    navigator.mozGetUserMedia ||
    navigator.msGetUserMedia);

    var video;
    var webcamStream;

    function startWebcam() {
        if (navigator.getUserMedia) {
            navigator.getUserMedia(

                {
                    video: true,
                    audio: false
                },

                // successCallback
                function (localMediaStream) {
                    video = document.querySelector('video');
                    video.src = window.URL.createObjectURL(localMediaStream);
                    webcamStream = localMediaStream;
                },

                // errorCallback
                function (err) {
                    console.log("The following error occured: " + err);
                }
            );
        } else {
            console.log("getUserMedia not supported");
        }
    }

    var canvas, ctx;

    function init() {
        canvas = document.getElementById("myCanvas");
        ctx = canvas.getContext('2d');
    }

    function snapshot() {
        ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
    }

第一段 navigator.getUserMedia 是為了讓程式, 在每一個瀏覽器上都可以運行, webkit 代表 chrome 跟 safari , 
moz 代表 Firefox, ms 代表 Edge 。

第二段 document.querySelector('video') 這段就是抓取第一個標籤為 video 的元素, 
靜態方法 URL.createObjectURL() 用於建立一個帶有 URL 的 DOMString 以代表參數中所傳入的物件,  
這個新的物件 URL 代表了所指定的 File 物件 或是 Blob 物件。 API是這樣 : 

::

    objectURL = URL.createObjectURL(blob)

blob : 一個用以建立物件 URL 的 File 物件 或是 Blob 物件

而 errorCallback 是指電腦找不到 webcam 時所顯示的錯誤訊息, else 就是 getUserMedia 並未成功啟動, 
function init() 則是針對畫面截圖作處理, 先找到 id 為 myCanvas 的物件, 2d 這個參數是設定一個平面的畫布, 
用於儲存影像截圖, function snapshot() 就是設定畫布大小和在哪顯示, API是這樣 : 

::

    context.drawImage(img,x,y,width,height)


















