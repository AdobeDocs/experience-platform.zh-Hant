---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料集與表和方案
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---


# 資料集與表和方案

檢視 [Adobe Experience Platform UI中可用的資料集清單](https://platform.adobe.com/datasets)，請務必觀察資料集名稱。
>[!NOTE]
>
>有些資料集名稱有空格，否則可能不是SQL安全。

![](../images/queries/datasets-and-tables/dataset-names.png)


按一下資料集表格中的架構名稱，以檢視UI中資料集架構的階層結構。

![](../images/queries/datasets-and-tables/schema-information.png)

開啟PSQL命令行，然後從此處使用連接詳細資訊： [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration).

![](../images/clients/psql/connect-bi.png)

要使用SQL查看平台上的可用表，可以使用或 `\d` 選擇 `SHOW TABLES;`。


`\d` 顯示標準PostgreSQL視圖

```
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` 是自訂命令，可提供更詳細的檢視並呈現表格，以及平台UI中的資料集名稱。

```
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

要查看表的根模式，請使用該命 `\d table_name` 令。

>[!NOTE]
>
>顯示的架構顯示根欄位，其中大多數是複雜的，在資料集架構UI中引用了對象類型。

`\d luma_midvalues`

```
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

要進一步進入模式，請使用下划線(`_`)在要描述的表中聲明列。 例如, `\d table_name_column`

`\d luma_midvalues_web`

```
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
