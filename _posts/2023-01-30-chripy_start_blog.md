---
title : Jekyll Blog 첫 글쓰기 (using Chirpy Thema)
date : 2023-01-30 11:33:00 + 0900
categories : [GITHUB, JEKYLL]
tags : [github, jekyll, chripy, md, markdown]
render_with_liquid: false
---

## ● POST 등록 규칙 

+ $BLOG_HOME/_posts/ 디렉토리 밑에 등록하고 싶은 POST 파일 생성
+ Post 파일 형식 : yyyy-mm-dd-[title].md *`ex)2023-01-30-start_chripy_blog.md`*
+ 파일명 중간에 공백을 넣지 않는다. 

<br>
## ● Post Header 작성 
```yml
---
title : Title name
date : yyyy-mm-dd HH:MM:SS  +/-TTTT 
categories : [category1, category2]
tags : [tag1, tag2]                     # only lower case
---

```

### Example Post Header 
```yml
---
title : Jekyll Blog 첫 글쓰기 (using Chirpy Thema)
date : 2023-01-30 11:33:00 + 0900
categories : [GITHUB, JEKYLL]
tags : [github, jekyll, chripy, md, markdown]
---
```
<br> 


## ● Post 배포하기 
local에서 작성한 파일을 github에 배포
```
$ cd $BLOG_HOME
$ git add .  

$ git commit -m 'first_post' 
[gh-pages exxxe9] first_post
 2 files changed, 45 insertions(+), 7 deletions(-)
 create mode 100644 _posts/2023-01-30-chripy_start_blog.md


$ git push
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 8 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 1008 bytes | 1008.00 KiB/s, done.
Total 6 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To github.com:majuboki12/majuboki12.github.io.git
   a5009b5..ecc9ce9  gh-pages -> gh-pages
```




 