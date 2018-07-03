# 關於Meta Tag  

放在HTML中的Head裡，全名叫做 **Metadata Tag**，中文名為詮釋資料標籤，意即資料的資料，是用來說明這一份HTML文件的特性和功能。以下用功能性分類常用的Meta Tag：

- SEO: Search Engine Optimization，搜尋引擎優化。
- OG: Open Graph Protocol，社群分享規範。

## SEO相關的Meta Tag

1. Title

   網頁的標題名稱，會顯示於搜尋結果中的網頁名稱。

```  html
<title>好房網</title>
```

2. Description

   網頁的描述，會顯示於搜尋結果中的網頁描述。

``` html 
<meta name='description' content='位於台北市松山區南京東路五段|藏富的南京捷運南方藏富'>
```

3. Keywords 

   由於此欄位容易被塞入垃圾訊息，現行主流瀏覽器皆已不採用。

``` html
<meta name='keywords' content='房屋,買屋,購屋,買房,售屋,賣房,賣屋,不動產'>
```

4. Robots

   機器人模式，用來告訴搜尋引擎的機器人如何處理這一份網頁。

``` html
<meta name='robots' content='index, follow'>
```

5. Viewport

   螢幕解析度，用來做響應式設計網頁，可以取得使用者裝置寬度來調整網頁版型。

``` html
<meta name='viewport' content='width=device-width, initial-scale=1.0, user-scalable=no'>
```

6. Canonical 

   用來整合多重網址的網頁，同一個網頁內容如果可以被多個不同的網址存取，會降低該網頁內容的搜尋權重。

``` html
<link rel="canonical" href="https://buy.housefun.com.tw">
```

## OG相關的Meta Tag

1. OG Title

   分享到社群後，社群網站顯示的物件標題。

``` html
<meta property="og:title" itemprop="name" content="買屋、購屋、買房子 | 好房網買屋">
```

2. OG Site_name

   分享到社群後，社群網站顯示物件所在的網站名稱。

``` html
<meta property="og:site_name" content="好房網Housefun買屋">
```

3. OG Type

   分享到社群後，社群網站定義的物件類型。

``` html 
<meta property="og:type" content="website">
```

4. OG Url

   分享到社群後，社群網站對於物件的標準網址。

``` html 
<meta property="og:url" itemprop="url" content="https://buy.housefun.com.tw/region/台北市_c">
```

5. OG Image

   分享到社群後，社群網站顯示的圖片連結。

``` html
<meta property="og:image" itemprop="image" content="https://buy.housefun.com.tw/images/fb-default.gif">
```

6. OG Description

   分享到社群後，社群網站顯示的物件描述。

``` html
<meta property="og:description" itemprop="description" content="好房網買屋提供您的資訊。最快速的找房搜尋，最多優質房屋仲介、影音看屋就上好房網Housefun!">
```

