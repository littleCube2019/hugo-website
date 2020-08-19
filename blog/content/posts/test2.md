---
title: "如何使用Hugo寫網頁"
date: 2020-08-18T18:02:20+08:00
draft: false
noshowdate: true
summary: 紀錄如何快速產生這個網頁
---
# 關於Hugo
是一個以**GO**語言寫成的**靜態網頁**生成器
可以分離很多設計上的工作，讓使用者專注於以Markdown撰寫內容

Go語言會體現在Go templates廣泛應用於hugo的html中

# 簡單的網頁生成步驟

(以下用\<\>包裹的代表變數，可自由迭代)
### step 0 安裝
Linux  
依github官網設定即可

	mkdir $HOME/src
	cd $HOME/src
	git clone https://github.com/gohugoio/hugo.git  
	cd hugo
	go install


windows  
1. 至https://github.com/gohugoio/hugo/releases  
下載對應版本，並將hugo.exe移至C槽之下
2. 設定環境變數，比如新增 C:\hugo  
(原因:很多操作需要在新增的網頁資料夾內呼叫hugo.exe)

### step 1 架設主體
先在hugo資料夾下輸入  
`hugo new site <網站名稱> `

就會產生名為　<網站名稱>　的資料夾，並預設以下內容  
![404](/how_to_hugo/1.png)
目前常用的有
* content 之後會製造posts資料夾，所有**內容檔**會以markdown的格式儲存於此  
* themes 是放關於**外觀主題**的資料夾  
* static 可以放置欲插入的**圖片**，之後md檔可以取用
* config.toml 是設定檔，設定重要**參數** 
* public 是放最終hugo輸出檔的資料夾

### step 2 添加文章
1. cd 至hugo/<網站名稱> 
2. `hugo new posts/<文章>.md `

最後編輯該md文件即可  
(參考: [markdown常用語法](https://markdown.tw/#link))  


### step 3 更換主題
  1. 至[官網](https://themes.gohugo.io/)找喜歡的主題  
  2. 下載並放置themes資料夾中  
  3. 於config.toml 添加 theme = <主題資料夾名稱>  

最後可以使用 `hugo server` 檢查效果

### step 4.部屬網站 
以下以github page為例  

1. 首先在github建立\<your-project\> (比如blog)與 \<username\>.github.io兩個repository  
2. git clone <\<your-project\>的url> && cd \<your-project\>  
3. 將之前寫好的<網站名稱> 貼入 \<your-project\>
4. 




# 遇到的問題與其解決方法
### 1.如何插入圖片?  
使用markdown語法，在想插入圖片的位置寫下   
由一個驚嘆號，後面接[替代文字], (圖片所在路徑)  
比如:  
![404](/how_to_hugo/2.png)

注意: 圖片路徑是以 <網站名稱> 內的static資料夾為root

### 2.如何微調別的大神寫好的主題?
如果有設定變數，就可以直接在config.toml中設定  
比如  
noshowdate = true  
就不會顯示日期

若想微調版面設計等  
通常在theme > layout > _default 中會有網頁架構的html檔案  
只要修改它就可以囉  
(因為通常設計不會太簡單，故可以先F12找到所在html元素，然後去trace code)

### 3.什麼是toml?
全名為 Tom's Obvious, Minimal Language
跟json、yaml一樣是資料交換的格式  
由Tom Preston-Werner大神所研發的項目，目的是簡化設定文件的格式
特性是可以唯一的轉換成一個hash table
由 key=value 、 [字節] 、 #註解 所組成  
並且擁有字串、整數、浮點數、布林、日期時間 ... 等資料型態  
EX:
```
# This is a TOML document.       

title = "TOML Example"       

[owner]    						
name = "Tom Preston-Werner"
dob = 1979-05-27T07:32:00-08:00 # First class dates

[database]
server = "192.168.1.1"
ports = [ 8001, 8001, 8002 ]
connection_max = 5000
enabled = true
```


# 參考資料
關於Hugo  
https://gohugo.io/  
https://www.minwt.com/webdesign-dev/html/21148.html  
https://gohugo.io/hosting-and-deployment/hosting-on-github/  
關於TOML  
https://zh.wikipedia.org/wiki/TOML  
https://www.cnblogs.com/sunsky303/p/9208848.html