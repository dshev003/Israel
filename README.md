Israel MK Analysis
================

The Members of the Knesset (MK) database, houses biographical
information in spreadsheet format of nearly 1200 individuals who served
in the Israeli Knesset from 1949 to 1977.

Israel is composed of a vast array of Jewish groups from across the
world, considering its foremost state policy is to encourage the growth
of its citizenry through Jewish emigration or Aliyah. Aside from the
native Druze, Bedouin and Arab citizens of Israel, its Jewish
inhabitants are almost entirely immigrants or descendents of immigrants
who arrived in Ottoman Palestine, Mandatory Palestine and Israel after
the 1880s. This database aims to catalog the origins of members of the
Israeli Knesset, which is the preeminent lawmaking body of the State of
Israel. The aims are sixfold:

1)  To compare patterns of Jewish immigration to the ethnic and regional
    composition of the Knesset over time.

2)  To examine how regional background, broad ethnic division, gender,
    age and type of birth locality tie to party membership in the
    Knesset over time.

3)  To analyze how the age and gender of MKs relate to ethnic and
    regional background over time.

4)  To pinpoint ideological variations in MKs born in Israel/Mandatory
    Palestine and those of foreign birth who immigrated to Israel over
    time.

5)  To view patterns of the “Hebraization” of Israeli political leaders
    over time.

6)  To link ethnic and regional attributes to geospatial data for public
    viewing.

## A Peak at the Dataset

Here is a sample of the individuals elected to the First Knesset between
1949 and 1951. This data was compiled from biographical information
about the various MKs that can be fetched from the Knesset website along
with other supplemental sources. There are a total of fifteen attributes
for which I collected data.

``` r
library(tidyverse)
library(kableExtra)
library(psych)

df = read.csv("1949-1951.csv")
kable(head(df))
```

| Knesset   | Party | Name              | Gender | Age | Birth.Year | Birth.Name          | Hebraized.Name. | Birthplace | Type.of.Birth.Locality | Birth.Region               | Birth.Country  | Birth.Country..Present. | Date.of.Immigration | Community | Notes |
|:----------|:------|:------------------|:-------|----:|-----------:|:--------------------|:----------------|:-----------|:-----------------------|:---------------------------|:---------------|:------------------------|:--------------------|:----------|:------|
| 1949-1951 | Mapai | Meir Argov        | Male   |  43 |       1905 | Meyer Grabovsky     | 1               | Rîbnița    | Town                   | Podolsk Governorate        | Russian Empire | Moldova                 | 1927                | Ashkenazi |       |
| 1949-1951 | Mapai | Ami Assaf         | Male   |  45 |       1903 | Ami Vilkomitz       | 1               | Rosh Pinna | Rural Community        | Beirut Vilayet             | Ottoman Empire | Israel                  | \-                  | Ashkenazi |       |
| 1949-1951 | Mapai | Zalman Aran       | Male   |  49 |       1899 | Zalman Aharonowitz  | 1               | Yuzovka    | City                   | Yekaterinoslav Governorate | Russian Empire | Ukraine                 | 1926                | Ashkenazi |       |
| 1949-1951 | Mapai | Yitzhak Ben-Zvi   | Male   |  64 |       1884 | Izaak Shimshelevich | 1               | Poltava    | City                   | Poltava Governorate        | Russian Empire | Russia                  | 1907                | Ashkenazi |       |
| 1949-1951 | Mapai | Aryeh Bahir       | Male   |  42 |       1906 | Aryeh Geller        | 1               | Odessa     | City                   | Kherson Governorate        | Russian Empire | Ukraine                 | 1924                | Ashkenazi |       |
| 1949-1951 | Mapai | David Bar-Rav-Hai | Male   |  54 |       1894 | David Borovoi       | 1               | Nizhyn     | Town                   | Chernigov Governorate      | Russian Empire | Ukraine                 | 1924                | Ashkenazi |       |

## Plots

Barplots and charts are an important visual aid to gain a better general
understanding of the data that was collected. Here is a prudent example.
Between the 1880s and Israel’s independence, immigration took place in
several stages. We can observe that the cohort of future MKs who arrived
in Ottoman Palestine in 1913 was much older than the future MKs who
arrived just a year later. On average, it appears that the future MKs
who arrived earlier were more likely to have changed their names in line
with Hebrew conventions than those who arrived later. However, there are
exceptions. The cohort that made aliyah in 1940 had Hebraized names in
contrast to those that arrived in 1938 and 1939. On the flipside, those
individuals who arrived in 1923 did not change their names, even though
most of the arrivals between 1921 and 1932 did change them. However, it
must be underscored that the sample size is only 130.

``` r
ggplot(df, aes(Birth.Year, Date.of.Immigration, colour = Hebraized.Name.)) + 
  geom_point() +  
  geom_smooth(method=lm, se=FALSE) + labs(x = "Birth Year", y = "Date of Immigration", color = "Hebraized Name")
```

![](README_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

Here is a barplot that shows the distribution of MKs who sat in the
Knesset between 1949 and 1951 by country of birth and political party.
We can see that most of the MKs born in former Russian/Soviet states
(Ukraine, Moldova, Belarus) overwhelmingly affiliated with leftist
parties. Those born in Poland and Israel (then Mandatory Palestine),
were more evenly divided between leftist and conservative parties. A
notable number of Israeli MKs of German Jewish origin affiliated with
the more liberal/centrist Progressive Party.

``` r

ggplot(df, aes(x = Birth.Country..Present., fill = Party)) + 
  geom_bar(width = 0.5) + 
  theme_minimal() + 
  labs(x = "Birth Country of Winning Candidates", y = "Number of Winning Candidates", fill = "Party") + 
  theme(axis.text.x = element_text(angle = -90), text = element_text(size = 10)) +  
  scale_fill_manual(values = c("#AF0000", "#0038B8", "#00ADCC", "#0077B9", "#FF524D", "#AD0101", "#FF0000", "#FFC800", "#0047AB", "#172d81", "#cd1b68", "#89C5C6"))
```

![](README_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->
