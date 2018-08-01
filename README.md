iNaturalist推廣活動--屁孩常見植物
================
CTH
Aug 1, 2018

鳩竟未來國家棟樑很會的植物是？
------------------------------

蒙第58屆中小學科學展覽會邀請，小魯有幸協助推廣國立嘉義大學和特有生物研究保育中心大力支持的**iNaturalist**生物影音平台，在現場招架各種形狀 (?) 的屁孩，<del>抄襲隔壁ebird攤位</del>發想出個題目，讓屁孩們有事做。<br> 題目是這樣的：**請說出一個植物名稱**，在屁孩放電後期加入獎勵機制，若是現場第一次講到的植物可得小獎品，目的是增加一些潛在常見植物，也加速發送<del>好重不想背回去的</del>小獎品的效率。<br> 結果如何，就讓我們繼續看下去。<br>

資料在這邊請笑納 -&gt; [我是資料](https://drive.google.com/open?id=1qVfn7v4TgSTIF0eNJ_b_bmkYnEvmcJqc)

### 資料前處理

一共問啊問的，共收集到好棒棒的377筆資料，一些俗名稍微轉換一下，方便後續統計，例如大花咸豐草就出現大花咸豐草、咸豐草、鬼針草、恰查某各種同物異名的狀況，必須統一，其他還有一些資料輸入時的打字錯誤等等。<br>

### 資料統計

#### 載入套件

``` r
library(magrittr);library(tidyverse);library(readxl)
```

#### 載入資料

資料已在excel中小計好了，直接匯入統計表。

``` r
dat <- read_xlsx("d:/iNaturalist/iNatEXB_plantlist.xlsx",sheet = "output",col_names = FALSE)
colnames(dat) <- c("vname","count")
```

#### 物種數、排名

依照次數多寡採降冪排序。

``` r
dat %>% dim() %>% .[1] %>% cat("共紀錄",.,"物種\n")
```

    ## 共紀錄 169 物種

``` r
dat %>% arrange(desc(count))
```

    ## # A tibble: 169 x 2
    ##    vname      count
    ##    <chr>      <dbl>
    ##  1 玫瑰花        30
    ##  2 大花咸豐草    18
    ##  3 榕樹          17
    ##  4 向日葵        14
    ##  5 仙人掌        13
    ##  6 含羞草        12
    ##  7 蒲公英         8
    ##  8 薰衣草         8
    ##  9 九層塔         7
    ## 10 黑板樹         6
    ## # ... with 159 more rows

#### 繪製長條圖

所謂無三不成禮，我們取次數大於3的物種繪圖。

``` r
p <- ggplot(data = dat %>% filter(count>=3),mapping = aes(x = reorder(vname,count),y = count)) +
  geom_col() +
  coord_flip() +
  labs(x="")
p
```

![](iNat_exhib_files/figure-markdown_github/unnamed-chunk-4-1.png)
