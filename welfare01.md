20200730
================
주윤하
July 30, 2020

# 한국인의 삶의 이해 ‘복지패널데이터’

복지패널데이터는 경제활동, 생활실태, 복지욕구 등 천여 개 변수로 구성 된 데이터입니다. 엄밀한 절차로 수집되었고 다양한 변수를
담고 있기 때문에 해당 데이터 분석을 통해 대한민국 사람들이 어떻게 살아가는지 알 수 있습니다.

## 1\. 한국복지패널데이터 분석 준비하기

데이터를 분석하기 위한 준비작업

### 데이터 분석 준비하기

#### 1\. 데이터 준비하기

Koweps\_hpc10\_2015\_beta1.sav 파일을 다운로드해 프로젝트 폴더에 삽입한다.

#### 2\. 패키지 설치 및 로드하기

해당 파일은 SPSS 전용 파일로 되어 있다. foreign 패키지를 이용하여 파일을 불러돈다.

``` r
install.packages("foreign")  # foreign 패키지 설치
library(foreign)             # SPSS 파일 로드
library(dplyr)               # 전처리
library(ggplot2)             # 시각화
library(readxl)              # 엑셀 파일 불러오기
```

#### 3\. 데이터 불러오기

foreign 패키지의 read.spss()를 이용해 복지패널데이터를 불러온다.

``` r
#데이터 불러오기
raw_welfare<-read.spss(file="Koweps_hpc10_2015_beta1.sav",
                       to.data.frame=T)
```

    ## Warning in read.spss(file = "Koweps_hpc10_2015_beta1.sav", to.data.frame = T):
    ## Koweps_hpc10_2015_beta1.sav: Compression bias (0) is not the usual value of 100

``` r
#복사본 만들기 
welfare <- raw_welfare
```

#### 4\. 데이터 검토하기

데이터의 구조와 특징을 파악하기

``` r
head(welfare)
tail(welfare)
View(welfare)
dim(welfare)
str(welfare)
summary(welfare)
```

#### 5\. 변수명 바꾸기

분석에 사용할 몇 개의 변수를 이해하기 쉬운 변수명으로 변경.

``` r
welfare<-rename(welfare, 
                sex=h10_g3,
                marriage=h10_g10,
                religion=h10_g10,
                code_job=h10_eco9,
                income=p1002_8aq1,
                code_region=h10_reg7)
```

### 데이터 분석 절차

  - 1단계. 변수 검토 및 전처리 가장 먼저 사용할 변수들을 전처리 한다. 변수의 특성을 파악하고 이상치를 정제한 다음
    파생변수를 만든다. 전처리는 분석에 활용한 변수 각각에 대해 실시한다.

  - 2단계. 변수 간 관계 분석 ![](img/09_01.png)
