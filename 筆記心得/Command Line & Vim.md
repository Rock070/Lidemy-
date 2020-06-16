#vim 
1. 打開 iterm
2. 輸入 [ vim 檔案名稱]，例如 [ vim test ]
3. 按鍵盤 [ i ]，開啟輸入模式
4. 按 [ esc ]，開啟普通模式（無法編輯）
5. 在普通模式下，輸入[ : ]進入命令模式，輸入[ q ]，退出 vim

##如果有修改內容又沒存檔，會出現
`
E37: No write since last change (add ! to override) 無法離開
`

##在普通模式下，離開的輸入：
* [ qa! ] 
放棄存檔離開

* [ q! ]，按[ enter ] 
離開

* [ wq ]，按[ enter ] 
存檔離開( w = write，存入，也就是存檔)

#command line

* cat 顯現檔案內文字
* grep 抓取關鍵字
例如，從 test.html 這個檔案中，抓取有提到[ o ]，這個字母的行，用於搜尋功能。
`
grep o test.html
`
* wget ，下載檔案或網頁原始碼
例如:下載 GOOGLE 首頁的原始碼
`wget https://google.com`
下載圖片
`wget https://avatars0.githubusercontent.com/u/53036805?v=4`

* curl 送出 Request
例如 : 得到 GOOGLE 的 Response
`curl https://google.com`
得到 GOOGLE 的 Head
`curl -i https://google.com`
* echo 印出文字
例如： 印出 123
`echo "123"`

* redirection > 重新導向，並蓋掉原本檔案內的內容
例如： 把ls -a 的 CLI 結果輸出到 list_result 這個檔案裡面
`ls -a > list_result`
把 echo 的結果重新導向到 test.txt 這個檔案裡面
`echo "123" > test.txt`

* append >> 附在後方
例如：text.txt 內已有文字 "123"，將 "456"，負載原有文字後方
`echo "456" >> test.txt`


* pipe | 指令組合，將前面檔案的輸出，變成後面檔案的輸入
例如：找出 test.txt 中 含字元 [ o ]的行
```
cat test.txt | grep o 
等於
grep o test.txt
將結果重新導向成檔案
cat test.txt | grep o > result
```


