```
正則表達式 = 普通字符(例:a到z) + 特殊字符(稱:元字符)
普通字符
非打印字符 
特殊字符{	
	^開頭
	$結尾
}
限定符


切忌有些要跳脫(轉義){
	/	跳脫成	\/
}
```

# 常用範例

|形式|		範例|			說明|
|-|-|-|
|\b單辭編輯\b|	\bis\b		|	找"is",但是不找"this"這種 |
|/全部/g	|	/\bis\b/g	|	把一篇文章內全部的is找出,但不找"this"這種 |
|/忽略大小寫/i|	/\bis\b/gi	|	把一篇文章內全部的is找出,不考慮大小寫,但不找"this"這種 |
|[擁有之一]	|	/[abc]/g	|	把字串內a,b,c之一的全部找出 |
|[^這些字以外]|	/[^abc]/g	|	把字串a,b,c以外的全部找出 |
|[a-z]		|[0-9a-zA-Z-]	|	把字串內 0到9,a到z,A到Z,-  之一的全部找出 |
|中文字 	|	[\u4e00-\u9fa5] |   |
|(符1\|符2\|符3)|	(apple\|banana\|orange)	|	apple 或是 banana 或是 orange |

# 簡寫
```
.					簡寫代表 [^\r\n] (幾乎是任意字符)
\d					簡寫代表 [0-9]	數字字符
\D					簡寫代表 [^0-9]	非數字字符
\s					簡寫代表 [\t\n\x0B\f\r]	空白符				
\S					簡寫代表 [^\t\n\x0B\f\r]非空白符	
\w					簡寫代表 [a-zA-Z_0-9]	單辭字符
\W					簡寫代表 [^a-zA-Z_0-9]  非單詞字字符
```

# 邊界
```
^		/^.@/g			找出字串中 開頭.@ 
$		/.@$/g			找出字串中 .@結束 
\b		\bis\b			" is "	單辭邊界
\B		\Bis\b			"this "	非單辭邊界
/多行處理/m	/.@/gm			連同換行都處理	
```

# 次數
```
形式			說明
\d?			數字 出現 0or1次
\d+			數字 出現 >=1次
\d*			數字 出現 任意次
\d{8}			數字 出現 8次	
\d{8,}			數字 出現 >=8次
\d{8,12}		數字 出現 8到12次
\d{0,8}			數字 出現 0到8次



貪婪模式	盡可能 匹配次數多  12345678.replace(/\d{3,6}/g,'x');	//x78
非貪婪模式	盡可能 匹配次數少  12345678.replace(/\d{3,6}?/g,'x');	//xx78
```

# 分組
```
(apple){3}	//蘋果在字串中出現3次
'a1b2c3d4'.replace(/([a-z]\d){3}/g,'x');	//xd4
|	/ca(r|t)/g	找出car或cat
'2016-11-25'.replace(/(\d{4})-(\d{2})-(\d{2})/g,$3$2$1);	//25112016
(?:忽略分組)
```

# 前瞻
```
形式				範例			說明
正向前瞻 exp(?=assert)		\w(?=\d)		這個數字前面是否是字母,是的話
負向前瞻 exp(?!=assert)


.					1個任意字符
.+		http\/\/.+.\jpg		至少1個任意字符
```

# 甲級術士
* `(?=(.*skbank\.com\.tw.*))(?!(.*skbank\.com\.tw\/9ede721114\.html))` 唯獨9ede721114.html這頁面擋掉(排除字串
