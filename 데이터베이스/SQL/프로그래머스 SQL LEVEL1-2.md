푼거 다 안올림
점검할 점 
- count()의 사용
- DATE 형식들
## COUNT
아래 같은 테이블이 있으면
- SAMPLE

|NO|NAME|QUANTITY|
|--|--|--|
|1|A|1|
|2|A|2|
|3|B|10|
|4|C|3|
|5|NULL|NULL|

SELECT COUNT(NO),COUNT(NAME) FROM SAMPLE
의 결과는
|COUNT(NO)|COUNT(NAME)|
|--|--|
|5|4|

## 날짜함수
DATE_FORMAT으로 대부분 해결 가능
```
SELECT DATE_FORMAT('1999-05-24', '%y %m %d'); -- 99 05 24
SELECT DATE_FORMAT('1999-05-24', '%Y %M %D'); -- 1999 May 24th
SELECT DATE_FORMAT(NOW(), "%b %m %D %H %i %s"); -- Sep 09 5th 10 02 28
```
|구분 기호|역학|구분기호|역할|
|--|--|--|--|
|%Y|4자리 년도|%m|숫자 월(두 자리)|
|%y|2자리 년도|%c|숫자 월(한자리는 한자리)|
|%M|긴 월(영문)|%d|일자(두자리)|
|%b|짧은 월(영문)|%e|일자(한자리는 한자리)|
|%W|긴 요일 이름(영문)|%l|시간(12시간)|
|%a|짧은 요일 이름(영문)|%H|시간(24시간)|
|%i|분|%r|hh:mm:ss AM,PM|
|%T|hh:mm:SS|%S|초|


날짜
- DATE( ) : 문자열에 따라 날짜 정보 생성 
- YEAR( ) : 날짜 정보에서 연도에 해당하는 값 반환
- MONTH( ) : 날짜 정보에서 월에 해당하는 값 반환
- MONTHNAME: 날짜 정보에서 월(영문)에 해당하는 값 반환
- DAYOFMONTH( ) , DAY( ) : 날짜 정보에서 일자에 해당하는 값 반환
- WEEKDAY( ) : 날짜 정보에서 요일값 반환(월요일이 0임)
- DAYNAME( ) : 날짜 정보에서 요일명 반환

시간
- TIME( ) : 문자열에 따라 시간 정보 생성 
- HOUR( ) : 시간 정보에서 시간에 해당하는 값 반환
- MINUTE( ) : 시간 정보에서 분에 해당하는 값 반환
- SECOND( ): 시간 정보에서 초에 해당하는 값 반환

시간/날짜 연산
ADDDATE, DATE_ADD(date, INTERVAL  value unit) : 시간/날짜 더하기
```
SELECT 
  date(now()), #2024-06-23
  ADDDATE(date(now()), INTERVAL 1 YEAR), #2025-06-23
  ADDDATE(date(now()), INTERVAL -2 MONTH), #2024-04-23
  ADDDATE(date(now()), INTERVAL 3 WEEK),
  ADDDATE(date(now()), INTERVAL -4 DAY),
  ADDDATE(date(now()), INTERVAL -5 MINUTE),
  ADDDATE(now(), INTERVAL 6 SECOND);
```

## SELECT문 사용하기

### 역순 정렬
desc,asc 안쓰는 경우 기본적으로 asc
```
SELECT NAME,DATETIME FROM ANIMAL_INS ORDER BY ANIMAL_ID DESC
```
<br>

### 아픈 동물 찾기

```
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS WHERE INTAKE_CONDITION='Sick' ORDER BY ANIMAL_ID
```
<br>

### 어린 동물 찾기(not 사용)<br>
(intake condition이 aged가 아닌 것 즉 not 사용)

```
select animal_id, name from animal_ins where not intake_condition='aged' order by animal_id asc;
```

### 여러 기준으로 정렬하기

```
select animal_id, name, datetime from animal_ins order by name asc, datetime desc
```

### 상위 n개 레코드

```
select name from animal_ins order by datetime limit 1;
```

### 동물 수 구하기

```
select count(*) from animal_ins
```

### 이름이 있는 동물의 아이디(not null 사용)

```
SELECT animal_id from animal_ins where name is not null order by animal_id asc;
```

### 중복 제거하기

```
select count(distinct(name)) from animal_ins where name is not null
```

### 경기도에 위치한 식품창고 목록 출력하기

```
select warehouse_id,warehouse_name,address,ifnull(freezer_yn,'N') from food_warehouse where address like '경기도%' order by warehouse_id
```

### 나이정보가 없는 회원 수 구하기

```
select count(*) as USERS from user_info where age is null;
```

### 가장 비싼 상품 구하기

```
SELECT max(price) as MAX_PRICE from product
```

### 가격이 제일 비싼 식품이 정보 출력하기


```
SELECT * from food_product order by price desc limit 1;
```

### 흉부외과 또는 일반외과 의사 목록 출력하기

```
select dr_name, dr_id,mcdp_cd,Date_format(hire_ymd,"%Y-%m-%d") from doctor where mcdp_cd ='cs' or mcdp_cd='gs' order by hire_ymd desc , dr_name asc;
```

### 이름이 없는 동물의 아이디

```
select animal_ID from animal_ins where name is null order by animal_id asc;
```

### NULL 처리하기

```
SELECT animal_type,ifnull(name,'No name') as name,sex_upon_intake from animal_ins
```

### 조건에 맞는 회원 수 구하기

```
select count(*) from user_info where Year(joined)=2021 and age>=20 and age<=29
select count(*) from user_info where DATE_FORMAT(JOINED,"%Y")=2021 and age>=20 and age<=29
```

### 조건에 맞는 아이템들의 가격의 총합 구하기

```
select sum(price) as total_price from item_info where rarity='legend'
```

### 12세 이하인 여자 환자 목록 출력하기

```
SELECT PT_NAME, PT_NO,GEND_CD,AGE,IFNULL(TLNO,'NONE') FROM PATIENT WHERE AGE<=12 AND GEND_CD='W' ORDER BY AGE DESC, PT_NAME
```

### 조건 맞는 도서 리스트 출력하기

```
select book_id,date_format(published_date,'%Y-%m-%d') from book where category='인문' 
and published_date like '2021%' order by published_date asc
```
### 3월에 태어난 여성 회원 목록 출력하기

```
select member_id, member_name, gender,
Date_format(date_of_birth,"%Y-%m-%d") as date_of_birth
from member_profile
where Month(date_of_birth)=3 and tlno is not null and gender='w'
order by member_id
```
### 평균 일일 대여 요금 구하기

```
SELECT ROUND(AVG(DAILY_FEE)) AS AVERAGE_FEE 
FROM CAR_RENTAL_COMPANY_CAR 
WHERE CAR_TYPE='SUV'
```

### 잡은 물고기 중 가장 큰 물고기의 길이 구하기

```
select concat(max(length),'cm') as max_length from fish_info;
```
### 잔챙이 잡은 수 구하기

```
select count(*) as fish_count from fish_info where length is null;
```

### 최대값 구하기

```
select max(datetime) from animal_ins
```

### 가장 큰 물고기 10 마리 구하기

```
select id, length from fish_info order by length desc,id limit 10;
```

### 잔챙이 잡은 수 구하기(null 카운트)

```
select count(*) as fish_count from fish_info where length is null;
```

## group by

```
select name,count(name) from animal_ins group by name having count(name)>1 order by name
```

### 고양이와 개는 몇 마리 있을까

```
select animal_type, count(*) from animal_ins 
where animal_type='Dog' or animal_type='Cat'
group by animal_type order by animal_id asc;
```

### 카테고리별 상품 개수 구하기

```
select substring(product_code,1,2) as category , count(*) as products from product
group by substring(product_code,1,2) order by product_code
```

### 진료과별 총 예약 횟수 출력하기

```
select MCDP_CD as '진료과코드' , count(*) as '5월예약건수' from appointment 
where apnt_ymd like "2022-05%" group by MCDP_CD order by count(apnt_no),mcdp_cd
```

### 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기

```
SELECT CAR_TYPE , COUNT(*) AS CARS 
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS in ('%시트%') 
GROUP BY CAR_TYPE
ORDER BY CAR_TYPE ASC;
```

### 월별 잡은 물고기 수 구하기

```
SELECT COUNT(*) AS FISH_COUNT ,MONTH(TIME) AS MONTH FROM FISH_INFO 
GROUP BY MONTH ORDER BY MONTH ASC;
```


## String
이름에 el이 들어가는 동물

```
select animal_id, name from animal_ins where name like '%el%' and animal_type='dog' order by name asc
```

### DATETIME에서 DATE로 형변환

```
select animal_id,name,date_format(datetime,"%Y-%m-%d") as '날짜' from animal_ins order by animal_id asc
```

### 중성화 여부 파악하기(CASE WHEN)

```
select animal_id,name,
case when sex_upon_intake like "Spayed%" or sex_upon_intake like "Neutered%"
Then 'O' 
ElSE 'X' 
End As "중성화" from animal_ins
```

### 입양 시각 구하기

```
select hour(datetime) as hour, count(*) as count from animal_outs where hour(datetime)>=9 and hour(datetime)<=19
group by hour(datetime) order by hour(datetime);

SELECT DATE_FORMAT(DATETIME,"%k") AS HOUR,COUNT(*) AS COUNT FROM ANIMAL_OUTS 
WHERE DATE_FORMAT(DATETIME,"%k")>=9 AND DATE_FORMAT(DATETIME,"%k")<20
GROUP BY DATE_FORMAT(DATETIME,"%k") ORDER BY HOUR(DATETIME) ASC
```

### 루시와 엘라 찾기

```
select animal_id,name,sex_upon_intake from animal_ins 
where name = 'Ella' or name='Lucy' or name='Pickle'or name='Rogan'or name='Sabrina'or 
name='Mitty' order by animal_id asc
```

### 조건에 맞는 도서 리스트 출력하기


published_date 형식이 2021-08-20 00:00:00 형식임(DATE 타입)

```
select book_id,date_format(published_date,'%Y-%m-%d') from book where category like '인문' 
and published_date like '2021%' order by published_date asc
```

### 잡은 물고기 중 가장 큰 물고기의 길이 구하기(concat)

```
select concat(max(length),'cm') as max_length from fish_info;
```

### 연도 별 평균 미세먼지 농도 조회하기

```
SELECT YEAR(YM) AS YEAR, ROUND(AVG(PM_VAL1),2) AS 'PM10',ROUND(AVG(PM_VAL2),2) AS 'PM2.5' 
FROM AIR_POLLUTION
WHERE LOCATION2='수원'
GROUP BY YEAR 
ORDER BY YEAR
```

### 조건에 부합하는 중고 거래 상태 조회하기

```
SELECT  BOARD_ID,WRITER_ID,TITLE,PRICE,CASE
        WHEN STATUS = 'DONE' THEN '거래완료'
        WHEN STATUS = 'SALE' THEN '판매중'
        ELSE '예약중' END AS STATUS
  FROM  USED_GOODS_BOARD
 WHERE  DATE_FORMAT(CREATED_DATE,'%Y-%m-%d') = '2022-10-05'
 ORDER BY BOARD_ID DESC
```

## JOIN

### 조건에 맞는 도서와 저자 리스트 출력하기

```
SELECT BOOK_ID,AUTHOR_NAME,DATE_FORMAT(PUBLISHED_DATE,"%Y-%m-%d") FROM BOOK, AUTHOR 
WHERE BOOK.AUTHOR_ID=AUTHOR.AUTHOR_ID AND BOOK.CATEGORY='경제'
ORDER BY BOOK.PUBLISHED_DATE ASC;
```

### 성분으로 구분한 아이스크림 총 주문량

```
SELECT INGREDIENT_TYPE,SUM(TOTAL_ORDER) AS TOTAL_ORDER FROM 
FIRST_HALF AS F INNER JOIN ICECREAM_INFO AS I ON
F.FLAVOR=I.FLAVOR
GROUP BY INGREDIENT_TYPE ORDER BY TOTAL_ORDER ASC;
```

### 상품 별 오프라인 매출 구하기

```
SELECT PRODUCT_CODE,SUM(PRICE*SALES_AMOUNT) AS SALES FROM
PRODUCT AS P INNER JOIN OFFLINE_SALE AS O ON P.PRODUCT_ID=O.PRODUCT_ID
GROUP BY PRODUCT_CODE ORDER BY SALES DESC , PRODUCT_CODE ASC;
```

### 물고기 종류 별 잡은 수 구하기

```
SELECT COUNT(FISH_NAME) AS FISH_COUNT,FISH_NAME 
FROM FISH_NAME_INFO AS NAME INNER JOIN FISH_INFO AS INFO
ON INFO.FISH_TYPE = NAME.FISH_TYPE
GROUP BY FISH_NAME ORDER BY FISH_COUNT DESC;
```

### ROOT 아이템 구하기

SELECT INFO.ITEM_ID/ORDER BY INFO.ITEM_ID 에서 INFO. 빠지면 틀림
```
SELECT INFO.ITEM_ID,ITEM_NAME FROM 
ITEM_INFO AS INFO INNER JOIN ITEM_TREE AS TREE ON  INFO.ITEM_ID=TREE.ITEM_ID
WHERE PARENT_ITEM_ID IS NULL ORDER BY INFO.ITEM_ID;
```

## 비트 연산

### 특정 형질을 가지는 대장균 찾기

```
SELECT COUNT(*) AS COUNT
FROM ECOLI_DATA
WHERE NOT(GENOTYPE & 2) AND (GENOTYPE & 1 OR GENOTYPE & 4)
```
