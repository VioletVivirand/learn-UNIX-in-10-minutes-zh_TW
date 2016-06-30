# Learn UNIX in 10 minutes

This is a Chinese Traditional Version of ["Learn UNIX in 10 minutes"](http://freeengineer.org/learnUNIXin10minutes.html)

## Learn UNIX in 10 minutes. Version 1.3

目次：

* 目錄
* 在檔案系統內遨遊
* 條列出目錄內容
* 更改檔案權限和屬性
* 移動、重新命名、和複製檔案
* 瀏覽和編輯檔案
* Shells
* 環境變數
* 互動式（指令）歷史紀錄
* 檔名補齊
* Bash 是一個很酷的 shell
* 重導
* 管線
* 指令替代
* 在檔案中搜尋字串：grep 指令
* 尋找檔案：find 指令
* 讀取或寫入磁帶、備份、和壓縮：tar 指令
* 需要幫忙？man 和 apropos 指令
* vi 編輯器的基本操作

## 目錄

在 UNIX 內，檔案和目錄的路徑，會被每個目錄名稱之前的斜線 "/" 給隔開。

範例：

	/					「根」目錄 ("root")
	/usr				usr 目錄（是 / 根目錄的子目錄）
	/usr/STRIM100		STRIM100 是 /usr 的子目錄


## 在檔案系統內遨遊

	pwd					顯示「目前工作目錄」，或是目前所在的目錄
	cd					切換目前所在目錄到家目錄 (HOME directory)
	cd /usr/STRIM100	切換目前所在目錄到 /usr/STRIM100
	cd INIT				切換目前所在目錄到目前所在目錄的子目錄 INIT
	cd ..				切換目前所在目錄到目前所在目錄的父目錄 (parent directory)
	cd  $STRMWORK		切換目前所在目錄到環境變數定義的目錄 'STRMWORK'
	cd  ~bob			切換目前所在目錄到使用者 bob 的家目錄 (home directory)（如果您有足夠的權限）


## 條列出目錄內容


* `ls`: 條列出一個目錄的內容<br>
* `ls -l`: 用長(long)（包含細節）格式條列出一個目錄的內容<br>

範例：

	$ ls -l 
	drwxr-xr-x    4 cliff    user        1024 Jun 18 09:40 WAITRON_EARNINGS
	-rw-r--r--    1 cliff    user      767392 Jun  6 14:28 scanlib.tar.gz
	^ ^  ^  ^     ^   ^       ^           ^      ^    ^      ^ 
	| |  |  |     |   |       |           |      |    |      | 
	| |  |  |     | 擁有者    群組       檔案大小  日期  時間   名稱
	| |  |  |     目錄和檔案包含的連結(link)數量
	| |  |  其他人的權限
	| |  群組成員擁有的權限
	| 檔案擁有者的權限：r = 讀取, w = 寫入, x = 執行 , - = 沒有權限
	檔案類型：- = 一般檔案, d = 目錄, l = 符號連結…等等


## 更改檔案權限和屬性

	chmod 755 file			將屬於檔案擁有者的檔案權限更改為 rwx，以及將檔案擁有者所屬的群組和其他人的權限改為 rx。（7 = rwx = 二進位 111。 5 = r-x = 二進位101）
	chgrp user file			將檔案所屬群組指定為 user 群組
	chown cliff file		將檔案擁有者指定為 cliff
	chown -R cliff dir		將目錄和目錄樹裡所有檔案的擁有者指定為 cliff

在執行這些指令以前，您需要成為檔案 / 目錄的擁有者，又或者您是 root 使用者。


## 移動、重新命名、和複製檔案

	cp file1 file2			複製 (copy) 一個檔案
	mv file1 newname		移動 (move) 一個檔案或將它重新命名
	mv file1 ~/AAA/			將檔案 file1 移到您的家目錄的子目錄 AAA 中
	rm file1 [file2 …]		移除 (remove) 一個檔案
	rm -r dir1 [dir2…]		遞迴移除一個目錄和它的所有內容（小心操作！）
	mkdir dir1 [dir2…]		建立目錄
	mkdir -p dirpath		建立 dirpath 目錄，並包含路徑中列舉到的所有目錄
	rmdir dir1 [dir2…]		移除一個空的目錄


## 瀏覽和編輯檔案

	cat filename		將檔案的內容顯示在螢幕上
	more filename		逐漸地將檔案的內容顯示在螢幕上：ENTER = 往下移動一行，
						SPACEBAR = 往下移動一頁，q = 離開預覽
	less filename		跟 more 指令相似，但還可以使用 Page-Up 功能。不一定適用於所有系統
	vi filename			用 vi 編輯器編輯一個檔案。所有 UNIX 系統都一定會有 vi
	emacs filename		用 emac編輯器編輯一個檔案。不是所有系統都會有 emacs
	head filename		顯示一個檔案的前幾行
	head -n  filename	顯示一個檔案的前 n 行
	tail filename		顯示一個檔案的後幾行
	tail -n filename	顯示一個檔案的後 n 行


## Shells


命令列介面的功能會因為使用的 shell 程式的不同而有些微的差異。

根據使用的 shell，可能會有些實用的額外功能。

您可以使用以下的指令查詢您正在使用的 shell：

    echo $SHELL

當然您可以製作一個包含一長串指令的檔案，並且像執行程式一樣執行它，以完成一項工作。我們稱這樣的檔案叫 shell script。這其實就是大多數 shell 的主要目的，而不只是做為一個互動式的命令列。


## 環境變數

您可以使用環境變數，來教您正在使用的 shell 記住一些事情。使用 bash shell 當作範例：

	export CASROOT=/usr/local/CAS3.0			
	定義 CASROOT 的值為 /usr/local/CAS3.0
	
	export LD_LIBRARY_PATH=$CASROOT/Linux/lib	
	定義 LD_LIBRARY_PATH 為 CASROOT 加上 /Linux/lib，也就是 /usr/local/CAS3.0/Linux/lib

在變數名稱之前加上 $ 首碼之後，您可以跟以下命令搭配操作：

	cd $CASROOT			將您的目前工作目錄變更為 CASROOT 的值
	echo $CASROOT			在螢幕上顯示 CASROOT 的值，也就是 /usr/local/CAS3.0
	printenv CASROOT		在 bash 或是其他 shell 裡面，這個指令等於之前描述的 echo $CASROOT


## 互動式（指令）歷史紀錄

bash 和 tcsh（其他 shell 也可能有）的特殊功能：您可以按鍵盤的「上」鍵來存取、修改、和執行先前使用過的指令。


## 檔名補齊

bash 和 tcsh（其他 shell 也可能有）的特殊功能：您可以按下 TAB 鍵來補齊已經漸入了一部份的檔名。舉例來說：如果您想要編輯一個在目錄裡的且叫做 "constantine-monks-and-willy-wonka.txt" 的檔案，您可以鍵入 `'vi const'`，再按下 TAB 鍵，這時 shell 會補齊剩下的文字（不過這個檔名必須是獨一無二的）。


## Bash 是一個很酷的 shell

Bash 甚至可以補齊指令跟環境變數的名稱。而且如果這時有很多可以被捕齊的名稱可以選擇，你可以按下兩次 TAB 鍵，bash 會顯示所有補齊的結果。Bash 是大多數 Linux 系統的預設 shell。


## 重導

	grep string filename > newfile		將 grep 指令輸出的內容重導到檔案 'newfile' 之內。
	grep string filename >> existfile	將 grep 指令輸出的內容附加到檔案 'existfile' 的結尾。

重導指令 `>` 和 `>>` 可以將大部份指令輸出的內容導入檔案中。


## 管線

管線符號 `|` 是用來將一個指令輸出的內容導到另外一個指令中。

範例：

	ls -l | more
	這可以將使用 "ls -l" 長格式輸出的目錄內容導（也可以稱作「過濾）到 more 指令中。這個例子的意義是將一個原本很長的目錄明細用多頁的方式瀏覽。
		
	du -sc * | sort -n | tail
	"du -sc" 這個指令會列出目前工作目錄內所有檔案和目錄的容量大小。內容被導到 "sort -n" 之後會依照容量大小，由小到大排序。內容最後被導到 "tail" 指令以後只會顯示倒數幾個項目（檔案容量最大的那幾個）。


## 指令替代

透過指令替代，您可以將一個指令輸出的內容輸入另一個指令當中。指令替代的執行方法，就是將要被替代的指令用兩個反單引號（`）框起來。舉個例子：

	cat `find . -name aaa.txt`

這串指令會用 cat 指令顯示目前所在目錄跟所有子目錄裡，檔案名稱為 aaa.txt 的檔案。


## 在檔案中搜尋字串：grep 指令

	grep string filename		顯示在檔案內容中，所有包含字串 string 的所有文字行。


## 尋找檔案：find 指令

`find search_path -name filename`

	find . -name aaa.txt						在目前所在目錄跟所有子目錄裡，尋找檔案名稱為 aaa.txt 的所有檔案。
	find / -name vimrc							在整個系統裡，尋找檔案名稱為 'vimrc' 的所有檔案。
	find /usr/local/games -name "*xpilot*"		在 /usr/local/games 的目錄樹裡，
												所有檔名包含字串 xpilot 的所有檔案。


## 讀取或寫入磁帶、備份、和壓縮：tar 指令

tar 指令代表的是 "tape archive（磁帶封裝）"。這是一個讀取或寫入封裝檔（可以是很多檔案或是整個目錄樹的集合）的標準做法。

您通常會看到很多名稱叫做 stuff.tar、或是 stuff.tar.gz 之類的檔案。這些是 tar 的封裝檔，還有使用 gzip 這隻程式壓縮過的 tar 封裝檔。

當有人給你一個 UNIX 系統在使用的磁帶時，它應該是屬於 tar 格式的，而你應該可以用 tar（和你的磁帶機）去讀取它。

同樣的，如果你想要將資料寫入一個磁帶並交給別人，你或許也應該使用 tar 指令。

Tar 範例：

	tar xv					將檔案在顯示檔案名稱明細 (v = verbose) 時從預設的磁帶機解除封裝
	tar tv					顯示預設磁帶機的檔案名稱明細，但不解除封裝
	tar cv file1 file2		將檔案 'file1' 和 'file2' 寫入預設的磁帶機
	tar cvf archive.tar file1 [file2...]
							製作一個名稱為 "archive.rar" 且包含檔案 file1, file2…等檔案的 tar 封裝檔
	tar xvf archive.tar		將 tar 封裝檔解除封裝
	tar cvfz archive.tar.gz dname
							建立一個用 gzip 壓縮過的 tar 封裝檔，
							而這個檔案包含目錄 'dname' 裡的所有檔案。但這個指令並不適用於所有版本的 tar
	tar xvfz archive.tar.gz	
							解除一個用 gzip 壓縮過的 tar 封裝檔。但這個指令並不適用於所有版本的 tar
	tar cvfI archive.tar.bz2 dname
							建立一個用 bz2 壓縮過的 tar 封裝檔。但這個指令並不適用於所有版本的 tar


## 需要幫忙？man 和 apropos 指令

大多數的指令都會有一個好用的的說明頁面，也多多少少會寫到一些細節的東西，像是一些很隱晦或是或是莫測高深的東西。有些人打趣說就叫 man 頁面的原因是因為只有真正厲害的人 (real men) 才看得懂裡面在寫些啥。

範例：

	man ls			顯示 ls 指令的說明頁面

您也可以用 apropos 來搜尋說明頁面

範例：

	apropos build	顯示一份有包含 "build" 的所有說明頁面的列表

用 `man apropos` 指令來查詢 `apropos` 的詳細用法。


## vi 編輯器的基本操作

### 開啓一個檔案

	vi filename

### 輸入文字

編輯模式(Edit modes)：按下這些按鍵可以進入編輯模式並且開始輸入文字到您的文件裡

	i		在游標之後插入文字
	I		在目前所在行的開始處插入文字
	a		在游標之前插入文字
	A		在目前所在行的結尾處插入文字
	r		取代一個文字
	R		取代模式
	<ESC>	離開插入或是複寫模式

### 刪除文字

	x		刪除一個文字
	dd		把目前所在行的內容給刪除，並且存放到緩衝區
	ndd		刪除 n 行(n 是一個數字)內容，並且存放到緩衝區
	J		把下一行文字接到目前所在行的末端（把換行符號刪除）

### 噢噢（刪錯東西了）

	u		復原最後一個指令

### 剪下和貼上

	yy		把目前所在行的內容放到緩衝區
	nyy		把 n 行的內容放到緩衝區
	p		Put the contents of the buffer after the current line
	P		Put the contents of the buffer before the current line

### 游標定位
           
	^d			移到下一頁
	^u			移到上一頁
	:n			把游標移到第 n 行
	:$			把游標移到檔案的結尾
	^g			顯示目前的行號
	h,j,k,l 	上、下、左、右。當然，如果您鍵盤上的方向鍵如果還沒有失去理智的話，也是可以用來操作的。

### 字串取代

	:n1,n2:s/string1/string2/[g]
	在第 n1 行到第 n2 行之間，將 string1 用 string2 給取代。如果同時有加上 g 參數（代表全域(global)），任何行中的 string1 都會被取代。如果沒有加上 g 參數，就只有設定的行號裡且第一個符合的結果才會被取代。
	
* ^ 符合行首符號
* . 符合任一個文字
* $ 符合換行符號

除了這些符號以外，還有一些「特殊字元」（像是倒斜線）可以用 `\` 符號來「逃脫」，例如：符合"/usr/STRIM100/SOFT"條件就要寫成 "\/usr\/STRIM100\/SOFT"

範例：

	:1,$:s/dog/cat/g		把第 1 行到第 $ 行（檔案結尾）的所有 'dog' 用 'cat' 給取代掉
	:23,25:/frog/bird/		把第 23 行到第 25 行的第一個 'frog' 用 'bird' 給取代掉


### 存檔、離開以及一些額外的操作

這些指令在使用之前要先輸入冒號(:)，然後再用輸入小寫的指令代碼在左下角的輸入格。會稱作額外操作的原因，是因為這些指令需要輸入在文字編輯器之外，在編輯模式裡輸入這些指令是沒有意義的。

按下 \<ESC> 以從編輯模式離開。

	:w					儲存目前的檔案
	:w new.file			儲存目前的檔案為 'new.file'
	:w! existing.file	覆蓋掉一個已經存在且正在被編輯的檔案的檔案（強制寫入）
	:wq					儲存目前的檔案並離開
	:q					離開
	:q!					離開並且不存檔
	
	:e filename			打開檔名為 'filename' 的檔案並編輯
	
	:set number			顯示行號
	:set nonumber		不顯示行號
