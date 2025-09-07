# UNIX 工作站如何執行中文系統?

2000年以前，Linux 作業系統還不普及，一般人尤其是中小學生根本無法接觸到 UNIX 工作站或是大型主機。記得高中時有機會參加台大資工所舉辦的椰林資訊營，第一看到昇陽的工作站，原本還以為上面都只有英文系統，沒想到照樣可以執行中文軟體與程式。

年代有些久遠，要找到 SUN 工作站上的軟體執行畫面並不難，但要找到有網友特別介紹其中文技術與資訊的網頁，就不容易了。我們還是從 Oracle 公司的文件來了解當年執行中文環境的方式。

註: 後來昇陽公司被甲骨文(Oracle)公司所併購

## 輸入繁體中文文字

根據 [https://docs.oracle.com/cd/E19683-01/816-0670/6m751tou8/index.html](https://docs.oracle.com/cd/E19683-01/816-0670/6m751tou8/index.html) 這份文件，我們可以看到 Solaris 系統當年就支援:

* zh_TW/zh_TW.EUC
* zh_TW.BIG5
* zh_TW.UTF-8
* zh_HK.BIG5HK
* zh_HK.UTF-8

而輸入法則支援以下幾種:

* 新注音
* 注音
* 倉頡
* 行列
* 無蝦米
* 大易
* 簡易
* 粵拼
* EUC 內碼
* BIG5 內碼
* BIG5_HKSCS 內碼
* 英文-中文
* 選擇性字碼表輸入法（例如拼音和其他)

來看看當年的輸入畫面，以倉頡輸入法為例:

![Solaris 倉頡輸入法](https://docs.oracle.com/cd/E19683-01/816-0670/images/input_window_area.tif.gif)

## 其他公用程式

最有意思的是當年其實就有內建查找表，你可以快速透過此公用程式，找到不容易輸入的字。(當年還沒有方便的全字庫系統可以查詢)

使用 EUC_TW 編碼的查找表格

![](https://docs.oracle.com/cd/E19683-01/816-0670/images/lookuptable_euc.tiff.gif)

至於使用者自定義字元(UDC)，也就是我們常說的「自造字」，在當年也是有相關公用程式可以使用。

![](https://docs.oracle.com/cd/E19683-01/816-0670/images/utilities_udc.tiff.gif)

更有意思的事情是，系統還教你如何建立新的字碼表輸入法。

1. 建立空白文字檔，包含中文字或詞並加上按鍵的清單。
2. 檔案轉換至二進位格式以便使字碼表輸入法介面能夠辨識

表格格式如下:

```
[Description]
[Comment]
[Key_Prompt]
[Function_Key]
[Phrase]
[Single]
[Options]
區段 "[Description]”     # 說明字碼表屬性
區段 "[Key_Prompt]"      # 指定輸入鍵的要求字串
區段 "[Function_Key]"    # 功能鍵的按鍵定義
區段 "[Single]"          # 指定輸入碼及與其相對應的單一中文字元
區段 "[Phrase]"          # 指定輸入碼以及其相對應的詞組文字
```


```
# /usr/lib/im/locale/zh_TW/common/txt2bin source_codetable_file

binary_codetable_file 
# /usr/lib/im/locale/zh_TW/common/bin2txt binary_codetable_file

source_codetable_file 
```

## 顯示 Post Script 系統(DPS)

Solaris 系統有提供能使用 Post Script 影像模型與程式語言，產生螢幕上的圖案。

您可以參考 https://docs.oracle.com/cd/E19253-01/819-0399/usertwnfontedit-1/index.html 這份文件，有初步的介紹。

![](https://docs.oracle.com/cd/E19253-01/819-0399/images/84-01.tiff.gif)

使用短短的 ps 指令，也能產生出視窗介面。

```
defineps PSWDisplayText(char *text)
			/pointSize 50 def
			/Helvetica pointSize selectfont
			(Hello World) stringwidth pop 2 div neg 0 moveto
			(Hello World) show

			/cpSize 40 def
			/Kai-Medium cpSize selectfont
			(text) stringwidth pop 2 div neg pointSize neg moveto
			(text) show
endps
```

![](https://docs.oracle.com/cd/E19253-01/819-0399/images/87-01.tiff.gif)

明天我們來聊聊倉頡輸入法。