---
cssclass: cards
---
---

```button
name 豆瓣笔记生成
type command
action QuickAdd: Macro::豆瓣笔记生成
```

```button
name 新建Bilibili视频笔记
type command
action QuickAdd: Macro::bilibili
```

---

### 想读/待读
```dataview
table without id ("![](" + cover + ")") as Cover, file.link as Name, default(split(author," ")[1],author) as "Author","待读" as "Status"
from #book  
where pageprogress=none & EndDate=none
sort BeginDate asc

```
### 在读
```dataview
table without id ("![](" + cover + ")") as Cover,"<progress value=" + pageprogress + " max="+pages+"  class='yellow'>" as progress, file.link as Name, default(split(author," ")[1],author) as "Author",  ("已读**=="+(date(today)-date(BeginDate)).days+"==**天") as "Duration" 
from #book  
where EndDate=none & pageprogress!=none 
sort BeginDate asc

```

### 读完
````ad-blank
title: 今年
collapse: true
icon: book-open

```dataview
table without id ("![](" + cover + ")") as Cover, file.link as Name, default(split(author," ")[1],author) as "Author", ("**=="+(date(today)-date(EndDate)).days+"==**天前读完") as "Past", ("阅读周期==**"+(date(EndDate)-date(BeginDate)).days+"**==天") as "Period"
from #book
where EndDate!=none & date(EndDate).year=date(now).year
sort BeginDate desc
```
````

````ad-blank
title: 以往
collapse: true
icon: book-open

```dataview
table without id ("![](" + cover + ")") as Cover, file.link as Name, default(split(author," ")[1],author) as "Author", ("**=="+(date(today)-date(EndDate)).days+"==**天前读完") as "Past", ("阅读周期==**"+(date(EndDate)-date(BeginDate)).days+"**==天") as "Period"
from #book  
where EndDate!=none & date(EndDate).year<date(now).year
sort BeginDate desc
```

````
