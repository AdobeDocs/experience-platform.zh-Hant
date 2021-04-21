---
keywords: Experience Platform;home；熱門主題；etl;ETL;etl轉換；ETL轉換
solution: Experience Platform
title: 範例ETL轉換
topic-legacy: overview
description: 本文將示範擷取、轉換、載入(ETL)開發人員可能遇到的下列範例轉換。
exl-id: 8084f5fd-b621-4515-a329-5a06c137d11c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# 範例ETL轉換

本文將示範擷取、轉換、載入(ETL)開發人員可能遇到的下列範例轉換。

## 將CSV平整至階層

### 範例檔案

範例CSV和JSON檔案可從公開ETL參考[!DNL GitHub]回購取得，由Adobe維護：

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)

### 範例 CSV

下列CRM資料已匯出為`CRM_profiles.csv`:

```shell
TITLE   F_NAME  L_NAME  GENDER  DOB EMAIL   CRMID   ECID    LOYALTYID   ECID2   PHONE   STREET  CITY    STATE   COUNTRY ZIP LAT LONG
Mr  Ewart   Bennedsen   M   2004-09-25  ebennedsenex@jiathis.com    71a16013-d805-7ece-9ac4-8f2cd66e8eaa    87098882279810196101440938110216748923  2e33192000007456-0365c00000000000   55019962992006103186215643814973128178  256-284-7231    72 Buhler Crossing  Anniston    Alabama US  36205   33.708276   -85.7922905
Dr  Novelia Ansteys F   1987-10-31  nansteysdk@spotify.com  2eeb6532-82e1-0d58-8955-bf97de66a6f5    50829196174854544323574004005273946998  2e3319208000765b-3811c00000000001   65233136134594262632703695260919939885  704-181-6371    79 Northfield Hill  Charlotte   North Carolina  US  28299   35.2188655  -80.8108885
Mr  Ulises  Mochan  M   1996-03-20  umochanco@gnu.org   6f393075-addb-bdd6-73f8-31c393b700f5    70086119428645095847094710218289660855  2e33192080003023-26b2000000000002   82011353387947708954389153068944017636  720-837-4159    00671 Mifflin Trail Lacolle Qu√©bec CA  E5A 45.08338    -73.36585
Mrs Friederike  Durrell F   1979-01-3   fdurrellbj@utexas.edu   33d018ec-5fed-f1a3-56aa-079370a9511b    50164729868919217963697788808932473456  2e33192080006dfc-0cdf400000000003   64452712468609735658703639722261004071  798-528-3458    47 Fremont Hill Independencia   Veracruz Llave  MX  91891   19.3803931  -99.1476905
Rev Evita   Bingall F   1974-02-28  ebingallod@mac.com  8c93db88-f328-8efb-dc73-d5654d371cbe    74973364195185450328832136951985519627  2e331920800038db-0559e00000000004   58945501950285346322834356669253860483  397-178-5897    56 Crescent Oaks Court  Buenavista  Oaxaca  MX  71730   19.4458447  -99.1497665
Mr  Eugenie Bechley F   1969-05-19  ebechley9r@telegraph.co.uk  b0c76a3f-6526-0ad0-e050-48143b687d18    67119779213799783658184754966135750376  2e331920800001a4-24b2800000000005   59715249079109455676103900762283358508  718-374-7456    5760 Southridge Junction    Staten Island   New York    US  10310   40.6307451  -74.1181235
Dr  Cammi   Haslen  F   1973-12-17  chaslenqv@ehow.com  56059cd5-5006-ce5f-2f5f-15b4d856a204    61747117963243728095047674165570746095  2e33192080007c25-2ec0600000000006   86268258269066295956223980330791223320  865-538-8291    83 Veith Street Knoxville   Tennessee   US  37995   35.95   -84.05
```

### 映射

下表概述了CRM資料的對應需求，並包含下列轉換：
- `identityMap`屬性的標識列
- 出生日期(DOB)至年和月日
- 將字串加倍或縮短整數。

| CSV欄 | XDM路徑 | 資料格式 |
| ---------- | -------- | --------------- |
| 標題 | person.name.courtesyTitle | 複製為字串 |
| F_NAME | person.name.firstName | 複製為字串 |
| L_NAME | person.name.lastName | 複製為字串 |
| 性別 | person.gender | 將性別轉換為對應人。性別列舉值 |
| DOB | person.byrthDayAndMonth:&quot;MM-DD&quot;<br/>person.birthDate:&quot;YYYY-MM-DD&quot;<br/>person.birthYear:YYYY | 將birthDayAndMonth轉換為string<br/>Transform birthDate為string<br/>Transform birthYear為short int |
| 電子郵件 | personalEmail.address | 複製為字串 |
| CRMID | identityMap.CRMID[{&quot;id&quot;:x, primary:false}] | 複製為字串至identityMap中的CRMID陣列，並將Primary設為false |
| ECID | identityMap.ECID[{&quot;id&quot;:x,primary:false}] | 複製為字串至identityMap中ECID陣列中的第一個項目，並將Primary設為false |
| Loyaltyid | identityMap.LOYALTYID[{&quot;id&quot;:x, primary:true}] | 複製為字串至identityMap中的LOYALTYID陣列，並將Primary設為true |
| ECID2 | identityMap.ECID[{&quot;id&quot;:x, primary:false}] | 複製為字串至identityMap中ECID陣列中的第二個項目，並將Primary設為false |
| 電話 | homePhone.number | 複製為字串 |
| 街道 | homeAddress.street1 | 複製為字串 |
| 城市 | homeAddress.city | 複製為字串 |
| 州 | homeAddress.stateProvince | 複製為字串 |
| 國家／地區 | homeAddress.country | 複製為字串 |
| ZIP | homeAddress.postalCode | 複製為字串 |
| LAT | homeAddress.latitude | 轉換為雙重 |
| 長 | homeAddress.longitude | 轉換為雙重 |


### 輸出XDM

以下範例顯示轉換為XDM的CSV的前兩列，如`CRM_profiles.json`所示：

```json
{
   "person": {
      "name": {
         "courtesyTitle": "Mr",
         "firstName": "Ewart",
         "lastName": "Bennedsen"
      },
      "gender": "male",
      "birthDayAndMonth": "09-25",
      "birthDate": "2004-09-25",
      "birthYear": 2004
   },
   "identityMap": {
      "CRMID": [{
         "id": "71a16013-d805-7ece-9ac4-8f2cd66e8eaa",
         "primary": false
      }],
      "ECID": [{
         "id": "87098882279810196101440938110216748923",
         "primary": false
      },
      {
         "id": "55019962992006103186215643814973128178",
         "primary": false
      }],
      "LOYALTYID": [{
         "id": "2e33192000007456-0365c00000000000",
         "primary": true
      }]
   },
   "homePhone": {
      "number": "256-284-7231"
   },
   "personalEmail": {
      "address": "ebennedsenex@jiathis.com"
   },
   "homeAddress": {
      "street1": "72 Buhler Crossing",
      "city": "Anniston",
      "stateProvince": "Alabama",
      "country": "US",
      "postalCode": "36205",
      "_schema": {
         "latitude": 33.708276,
         "longitude": -85.7922905
      }
   }
},{
   "person": {
      "name": {
         "courtesyTitle": "Dr",
         "firstName": "Novelia",
         "lastName": "Ansteys"
      },
      "gender": "female",
      "birthDayAndMonth": "10-31",
      "birthDate": "1987-10-31",
      "birthYear": 1987
   },
   "identityMap": {
      "CRMID": [{
         "id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5",
         "primary": false
      }],
      "ECID": [{
         "id": "50829196174854544323574004005273946998",
         "primary": false
      },
      {
         "id": "65233136134594262632703695260919939885",
         "primary": false
      }],
      "LOYALTYID": [{
         "id": "2e3319208000765b-3811c00000000001",
         "primary": true
      }]
   },
   "homePhone": {
      "number": "704-181-6371"
   },
   "personalEmail": {
      "address": "nansteysdk@spotify.com"
   },
   "homeAddress": {
      "street1": "79 Northfield Hill",
      "city": "Charlotte",
      "stateProvince": "North Carolina",
      "country": "US",
      "postalCode": "28299",
      "_schema": {
         "latitude": 35.2188655,
         "longitude": -80.8108888
      }
   }
}
```

## 資料幀到XDM架構

資料幀（如Parce檔案）的層次必須與要上載到的XDM架構的層次匹配。

### 資料幀示例

以下示例資料幀的結構已映射到實現[!DNL XDM Individual Profile]類的方案，並包含與該類型的方案關聯的最常見欄位。

```python
[
    StructField("person", StructType(
        [
            StructField("name", StructType(
                [
                    StructField("courtesyTitle", StringType()),
                    StructField("firstName", StringType()),
                    StructField("lastName", StringType())
                ]
            )),
            StructField("gender", StringType()),
            StructField("birthDayAndMonth", StringType()),
            StructField("birthDate", StringType()),
            StructField("birthYear", LongType())
        ]
    )),
    StructField("identityMap", MapType(
        StructField("CRMID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        )),
        StructField("ECID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        )),
        StructField("LOYALTYID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        ))
    )),
    StructField("homePhone", StructType(
        [
            StructField("number", StringType())
        ]
    )),
    StructField("personalEmail", StructType(
        [
            StructField("address", StringType())
        ]
    )),
    StructField("homeAddress", StructType(
        [
            StructField("street1", StringType()),
            StructField("city", StringType()),
            StructField("stateProvince", StringType()),
            StructField("country", StringType()),
            StructField("postalCode", StringType()),
            StructField("_schema", StructType(
                [
                    StructField("latitude", DoubleType()),
                    StructField("latitude", DoubleType()),
                ]
            ))
        ]
    ))    
]
```

在構建資料幀以用於Adobe Experience Platform時，必須確保其分層結構與現有XDM模式的層次結構完全匹配，以便欄位能夠正確映射。

## 身分圖到身份圖

### 身分陣列

```json
[
  {
    "xdm:id": "someone1@example.com",
    "xdm:namespace": {
      "xdm:code": "Email"
    }
  },
  {
    "xdm:id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5",
    "xdm:namespace": {
      "xdm:code": "CRMID"
    }
  },
  {
    "xdm:id": "2e3319208000765b-3811c00000000001",
    "xdm:namespace": {
      "xdm:code": "LOYALTYID"
    }
  }
]
```

### 映射

下表概述了身份陣列的映射要求：

| 身分欄位 | identityMap欄位 | 資料類型 |
| -------------- | ----------------- | --------- |
| identities[0].id | identityMap[電子郵件][{"id"}] | 複製為字串 |
| identities[1].id | identityMap[CRMID][{"id"}] | 複製為字串 |
| identities[2].id | identityMap[LOYALTYID][{"id"}] | 複製為字串 |

### 輸出XDM

以下是轉換為XDM的身份陣列：

```JSON
"identityMap": {
      "Email": [{
         "id": "someone1@example.com"
      }],
      "CRMID": [{
         "id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5"
      }],
      "LOYALTYID": [{
         "id": "2e3319208000765b-3811c00000000001"
      }]
   }
```
