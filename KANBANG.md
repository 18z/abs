### 翻譯看板


* 近期目標：將整本書翻譯完，產出中文初稿。
* 中期目標：潤稿。
* 長期目標：完成翻譯及潤稿，並分享給有需要的朋友。

翻譯節奏：

```
deanboole	每天一句
colorbook	休息
klaywang03	
Rslw		每天一句
Goldie Lin	每週三句
```

翻譯者 / 正在翻譯章節：

```
deanboole	ch6
colorbook	ch2	
klaywang03	
Rslw		ch3
Goldie Lin	ch4-2..ch5
```

翻譯流程：

```
1. fork https://github.com/deanboole/abs
2. 開始翻譯/編輯
3. 發 Pull Request 給 https://github.com/deanboole/abs
```

編輯格式：

```bash
* 英文在上，中文在下

例如：

英文原文
>`中文翻譯`

* 範例 script 部份的程式區塊語法，從原本 "縮排4個空格"
改成 "不用縮排，而是在頭尾各加3個反引號(```)來包住，
並於開頭三個反引號後面明確標示使用 bash 語法標亮"。

例如：

echo “scripts 排版範例”
```

commit message：格式

```
中文翻譯新增 所編輯文件名
中文翻譯修改 所編輯文件名
英文文本新增 所編輯文件名
英文文本修改 所編輯文件名
排版修正     所編輯文件名
文件新增     所新增文件名

例如：

$ git commit -m "中文翻譯新增 ch4-1.md" -m "
> 英文原文
> `中文翻譯`"
```

專有名詞參照表：

```
建構中
```

推薦使用工具

```
CLI Google Translate	https://github.com/soimort/translate-shell
```
