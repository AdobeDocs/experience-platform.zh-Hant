---
solution: Experience Platform
title: 探索和處理原始資料集支援Experience Platform控制面板
type: Documentation
description: 了解如何使用Query Service探索及處理原始資料集，在Experience Platform中支援設定檔、區段和目的地控制面板。
source-git-commit: 1facf7079213918c2ef966b704319827eaa4a53d
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 1%

---


# 使用Query Service探索、驗證及處理控制面板資料集

Adobe Experience Platform可透過Experience PlatformUI中的控制面板，提供貴組織的設定檔、區段和目的地資料的重要資訊。 接著，您就可以使用Adobe Experience Platform Query Service來探索、驗證及處理在資料湖中支援這些控制面板的原始資料集。

## Query Service快速入門

Adobe Experience Platform Query Service可協助行銷人員運用標準SQL在資料湖中查詢資料，從其資料中獲得深入分析。 Query Service提供使用者介面和API，可用來加入資料湖中的任何資料集，並將查詢結果擷取為新資料集，以用於報表、機器學習或擷取至即時客戶個人檔案。

若要進一步了解查詢服務及其在Experience Platform中的角色，請先閱讀[查詢服務概述](../query-service/home.md)。

## 可用的資料集

您可以使用Query Service查詢設定檔、區段和目的地控制面板的原始資料集。 以下小節說明可在資料湖中找到的原始資料集。

### 設定檔屬性資料集

「即時客戶設定檔」中，每個作用中的合併原則都會有設定檔屬性資料集，可供資料湖使用。

這些資料集的命名慣例為&#x200B;**設定檔屬性**，後面接著英數字值。 例如︰`Profile Attribute 14adf268-2a20-4dee-bee6-a6b0e34616a9`

若要了解每個資料集的完整結構，您可以使用Experience PlatformUI中的資料集檢視器來預覽和探索資料集。

### 區段中繼資料資料集

資料湖中有可用的區段中繼資料資料集，內含組織每個區段的中繼資料。

此資料集的命名慣例為&#x200B;**設定檔區段定義**，後接英數字值。 例如︰`Profile Segment Definition 6591ba8f-1422-499d-822a-543b2f7613a3`

若要了解資料集的完整結構，您可以使用Experience PlatformUI中的資料集檢視器來預覽和探索結構。

![](images/query/segment-metadata.png)

### 目的地中繼資料資料集

您組織所有啟動目的地的中繼資料都可作為資料湖的原始資料集使用。

此資料集的命名慣例為&#x200B;**DIM_Destination**。

若要了解資料集的完整結構，您可以使用Experience PlatformUI中的資料集檢視器來預覽和探索結構。

![](images/query/destinations-metadata.png)

## 範例查詢

下列範例查詢包含可用於Query Service中的範例SQL，以探索、驗證和處理支援控制面板的原始資料集。

### 依身分的設定檔計數

此設定檔分析可提供資料集中所有合併設定檔的身分劃分。 依身分劃分的設定檔總數（換句話說，將每個命名空間顯示的值加總）可能高於合併的設定檔總數，因為一個設定檔可能有多個相關聯的命名空間。 例如，如果客戶在多個管道上與您的品牌互動，則多個命名空間將會與該個別客戶相關聯。

**查詢**

```sql
Select
        Key namespace,
        count(1) count_of_profiles
     from
        (
           Select
               explode(identitymap)
           from
              profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
        )
     group by
        namespace;
```

### 依區段的設定檔計數

此受眾深入分析可提供資料集中每個區段內合併的設定檔總數。 此數字是將區段合併原則套用至您的設定檔資料的結果，以便將設定檔片段合併在一起，為區段中的每個個人形成單一設定檔。

```sql
Select          
        concat_ws('-', key, source_namespace) segment_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Segmentmembership)
                  from
                    profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
              )
        )
      group by
      segment_id
```

## 後續步驟

閱讀本指南後，您現在可以使用Query Service執行數個查詢，探索及處理支援設定檔、區段和目的地控制面板的原始資料集。

若要進一步了解每個控制面板及其量度，請在檔案導覽中，從可用控制面板清單中選取控制面板。
