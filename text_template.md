<!-- Title of the text -->
# Title
<!-- <!-- Info section: This section contains all information of the exhibition(s)/ film(s)/ Music (shows)/ design item(s) the text is writing about. For all text and naming, they should be bilingual if possible, in TC and then EN, for example: "'titleTC'&&' '&&'titleEN'" or "'ArtistTC'&&' '&&'ArtistEN'.-->

<!-- (1) IF the text is about exhibition(s), it needs to include these fields: Exh, ExhPeriod, Venue, Artists, Curators (#optional) -->
```
Exh: "title"
ExhPeriod: "ExhStartDate - ExhEndDate"
Space: "Artspace"
Artists: 
- "Artist1"
- "Artist2"
- "Artist3"
Curators: 
- "Curator1"
- "Curator2"
- "Curator3"
```
<!-- (2) IF the text is about a film, it needs to include these fields: Film, FilmYear, Directors -->
```
Film: "Film"
FilmYear: "FilmYear"
Directors:
- "Director1"
- "Director2"
```
<!-- (3) IF the text is about a music show or performance, it needs to include these fields: Perf, PerfDay (#optional), Venue (#optional) Artists -->
```
Perf: "Perf"
Venue: "Venue"
PerfDay: "PerfDay"
Artists: 
- "Artist1"
- "Artist2"
- "Artist3"
```
<!-- (4) IF the text is about an album, it needs to include these fields: Album, AlbumYear, Artists -->
```
Album: "Album"
AlbumYear: "Album"
Artists: 
- "Artist1"
- "Artist2"
- "Artist3"
```
<!-- (5) IF the text is about a design piece, it needs to include these fields: DesignItem, DesignYear, Designers -->
```
DesignItem: "DesignItem"
DesignYear: "DesignYear"
Designers:
- "Designer1"
- "Designer2"
```
<!-- (6) There could be other possible formats. Please flat it if there are something missing. -->

<!-- in case the text is referring to 2 or more exhibitions, or films, or etc., add one separate ``` block per exhibition (do not merge them into one block) -->
<!-- ```
info: "info"
``` -->

<!-- divider to start the main text -->
---
<!-- Main text: the paragraphs and images layout below depends on each text content. The style follow straightly that of .md files' style https://github.com/adam-p/markdown-here/wiki/markdown-cheatsheet -->

![image](./img/banner.jpg)
<H6>Caption as cition of banner.jpg</H6>

### Subtitle 1
Para1
<!-- for all images in the text, citation is needed, as in H6 -->
|![image](./img/img1.jpg)|![image](./img/img2.jpg)|
|-----|-----|
|<H6>Caption as cition of img1.jpg</H6>|<H6>Caption as cition of img2.jpg</H6>|

### Subtitle 2
Para2
<!-- for all quotes and direct in-text citaions, use blockquote-->
> quote[^1]

> <H3>Quote as Subtitle 3</H3>
Para3[^2]

###### Caption as cition of img3.jpg
![image](./img/img3.jpg)
<H6>Caption as cition of img3.jpg</H6>

### Subtitle 4
Para4 [^3]

<!-- Footnote: Optional. This section is for footnotes -->
---
[^1]: ref1
[^2]: ref2
[^3]: ref3

<!-- Reference List: this part is compulsory if there is any reading reference or any artworks. All citations should be in Harvard style citation. 
- Citation Examples for Artworks
-- Artworks in Chinese title (TC/SC): 藝術家（年份）。《藝術品名稱》。〔媒介〕。藝術空間，城市。
-- Artworks in English title (EN): Artist, A. (Year) *Title of the work*. [Medium]. Venue, City. 
*keep ascending order of last name of the artist
-->
---
#### 參考目錄 Reference List
1. Citation 1  
2. Citation 2  
3. Citation 3  
...

<!-- publish date: in yyyy-mm-dd; the "_" acts as a short divider -->
_  
(pub.date)  
<!--post notes: this part is optional and will be written personally by author-->
*notes  

