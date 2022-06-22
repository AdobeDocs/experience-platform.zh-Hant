---
title: 派生屬性
description: 派生屬性允許您計算常規節奏上的屬性，並根據需要將這些派生屬性作為配置檔案屬性發佈到即時客戶配置檔案中。 本文檔概述了如何使用查詢服務建立派生屬性，以便與配置檔案資料一起使用。
source-git-commit: 72e157e0a6310ebf2f55205b03b60600a56e3cf6
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 1%

---

# 派生屬性

派生屬性允許您計算常規節奏上的屬性，並根據需要將這些派生屬性作為配置檔案屬性發佈到即時客戶配置檔案中。

對於分析配置檔案資料的各種使用情形，派生屬性（如使用十位資料建立的屬性）是必需的。 使用十位資料，您可以根據段的百分點或給定屬性的等級，從段中建立受眾。 例如，可能的使用案例可能包括：

* 根據頻道收視率確定最低的10%的訂戶。 這將使營銷人員能夠瞄準特定受眾並銷售新的訂戶包。
* 根據飛行里程總和，確定在前10%的傳單中擁有「飛行員」身份的受眾。 這些觀眾可以有選擇地瞄準新信用卡銷售。

## 快速入門

此概述要求您對以下方面有正確的瞭解： [平台API調用](../landing/api-guide.md) 及Adobe Experience Platform的下列組成部分：

* [即時客戶概要資訊概述](../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
* [架構組合的基礎](../xdm/schema/composition.md):介紹經驗資料模型(XDM)架構以及構建架構的構成塊、原則和最佳做法。
* [如何為即時客戶配置檔案啟用方案](../profile/tutorials/add-profile-data.md):本教程概述了將資料添加到即時客戶概要檔案中所需的步驟。

## 對派生屬性的SQL支援

要根據特定維（類別）和相應度量（收入、點數、播放持續時間等）定義十位數的排名，必須設計方案以允許十位數分段。 此架構可用作較大配置式架構的一部分。

### 為配置檔案架構建立標識命名空間 {#identity-namespace}

身分識別命名空間是 [ Identity Service](../identity-service/home.md) 的元件，用途是作為身分識別相關內容的指標。 完全限定的標識包括ID值和命名空間。 當跨配置檔案片段匹配和合併記錄資料時，標識值和命名空間必須匹配。

建立的與身份相關的資料集可以分組為資料組，並有助於維護資料生命週期。 可以使用 [標識服務API](../identity-service/api/create-custom-namespace.md) 或通過UI。 查看 [管理自定義命名空間文檔](../identity-service/namespaces.md#manage-namespaces) 有關如何通過UI執行此操作的指導。

可以將主標識描述符分配給架構UI中的欄位，也可以使用架構註冊表API建立。 有關如何 [在Adobe Experience PlatformUI中定義標識欄位](../xdm/ui/fields/identity.md#define-an-identity-field)，或通過 [架構註冊表API](../xdm/api/descriptors.md#create)。

查詢服務還允許您直接通過SQL為臨時模式資料集欄位設定標識或主標識。 請參閱 [在臨時架構標識中設定輔助標識和主標識](./data-governance/ad-hoc-schema-identities.md) 的子菜單。

## 建立派生屬性

本文檔中提供的示例查詢側重於對大型資料集進行分類並將資料從最高值到最低值排序（反之亦然），並基於時段進行篩選。

### 德基萊 {#deciles}

10是將一組排列的資料分割成10個等分的方法。 當資料被分成十個檔案時，將十個檔案級分配給資料集中的每個行。 這允許資料按降序或升序排序。

10級按從低到高的順序排列資料，並以1到10的比例進行，其中每個連續數對應於增加10個百分點。

Decile時段表示已排名的組數，用於為資料集中的維（類別）分配排名。 該儲存段可以是一個數字或表達式，計算每個分區的正整數值。 儲存桶不能具有空值。

用四分位將分佈除以四，百分位乘以100。

### 為分檔儲存段建立方案 {#create-schema}

為十位儲存桶建立的架構有三個組成部分：資料類型、資料類型的欄位組（每個源資料集）和主標識欄位。

>[!NOTE]
>
>必須先建立標識命名空間，然後才能建立架構。 查看 [標識命名空間](#identity-namespace) 的子菜單。

Adobe提供多個標準（「核心」）XDM類，包括XDM Individual Profile和XDM ExperienceEvent。 除了這些核心類之外，您還可以建立自己的自定義類，以說明組織的更具體的使用案例。 請參閱有關如何 [在UI中建立和編輯架構](../xdm/ui/resources/schemas.md#create) 或使用 [架構註冊表API中的架構終結點](../xdm/api/schemas.md#create) 的子菜單。

正被攝入Experience Platform以供即時客戶配置檔案使用的資料必須符合為配置檔案啟用的經驗資料模型(XDM)架構。 為了為配置檔案啟用架構，它必須實現XDM Individual Profile或XDM ExperienceEvent類。

你可以 [使用架構註冊表API啟用用於即時客戶概要檔案的架構](../xdm/tutorials/create-schema-api.md) 或 [架構編輯器用戶介面](../xdm/tutorials/create-schema-ui.md)。  有關如何為配置檔案啟用架構的詳細說明，請參見其各自的文檔。

### 建立資料類型 {#create-data-type}

資料類型用作類或架構欄位組中的參考型別欄位，並允許一致使用可包含在架構中任何位置的多欄位結構。 建立資料類型是每個沙箱的一次性步驟，因為它可重用於所有與檔案相關的欄位組。

有關如何 [定義自定義資料類型](../xdm/api/data-types.md) 使用 [架構註冊表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。

### 建立十位欄位組 {#create-field-group}

建立欄位組是每個沙盒的一次性步驟。 它還可重用於所有與檔案相關的架構。

有關如何 [通過UI建立檔案組](../xdm/ui/resources/field-groups.md#create)

## 使用查詢服務建立檔案

查詢服務提供了建立包含分類文檔的資料集的理想方法。 然後，可以與分段服務一起使用，以基於屬性排名建立受眾。

只要定義了類別（維）並且度量可用，以下示例中顯示的概念就可以用於建立其他十位數儲存段資料集。 這些示例基於航空公司忠誠計畫的資料。 航空公司忠誠度資料利用「體驗事件」類，其中每個事件是業務交易的記錄， **里程**，貸記或借記，以及成員 **忠誠度** 「傳單」、「常客」、「銀」或「金」。 主標識欄位為 `membershipNumber`。

### 建立查詢模板 {#create-a-query-template}

可以使用UI中的查詢編輯器建立模板，或通過 [查詢服務API](./api/query-templates.md#create-a-query-template)。

將更詳細地檢查下面顯示的查詢模板的各節。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/query-templates \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
         "name": "Airline Loyalty Deciles Insert into profile",
         "sql":
            "WITH summed_miles_1 AS (
                SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
                    _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
                    SUM(_profilefoundationreportingstg.mileage) AS totalMiles
                FROM airline_loyalty_data
                WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
            GROUP BY 1,2
            ),
            summed_miles_3 AS (
                SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
                    _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
                    SUM(_profilefoundationreportingstg.mileage) AS totalMiles
                FROM airline_loyalty_data
                WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 1))
            GROUP BY 1,2
            ),
            summed_miles_6 AS (
                SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
                    _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
                    SUM(_profilefoundationreportingstg.mileage) AS totalMiles
                FROM airline_loyalty_data
                WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 4))
            GROUP BY 1,2
            ),
            rankings_1 AS (
                SELECT membershipNumber,
                    loyaltyStatus,
                    totalMiles,
                    NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
                FROM summed_miles_1
            ),
            rankings_3 AS (
                SELECT membershipNumber,
                    loyaltyStatus,
                    totalMiles,
                    NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
                FROM summed_miles_3
            ),
            rankings_6 AS (
                SELECT membershipNumber,
                    loyaltyStatus,
                    totalMiles,
                    NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
                FROM summed_miles_6
            ),
            map_1 AS (
                SELECT membershipNumber,
                    MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
                FROM rankings_1
                GROUP BY membershipNumber
            ),
            map_3 AS (
                SELECT membershipNumber,
                    MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth3
                FROM rankings_3
                GROUP BY membershipNumber
            ),
            map_6 AS (
                SELECT membershipNumber,
                    MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth6
                FROM rankings_6
                GROUP BY membershipNumber
            ),
            all_memberships AS (
                SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
            )
            SELECT STRUCT(
                    all_memberships.membershipNumber AS membershipNumber,
                    STRUCT(
                            map_1.decileMonth1 AS decileMonth1,
                            map_3.decileMonth3 AS decileMonth3,
                            map_6.decileMonth6 AS decileMonth6
                    ) AS decilesMileage
                ) AS _profilefoundationreportingstg
            FROM all_memberships
                LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
                LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
                LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)"
        }'
```

#### 回溯期間

十位資料類型包含1、3、6、9、12和生命期查找的儲存桶。 查詢使用1、3和6個月的回溯期，因此每個節都將包含一些「重複」查詢，以便為每個回溯期建立臨時表。

>[!NOTE]
>
>如果源資料沒有可用於確定回溯週期的列，則所有十級分類排名都將在 `decileMonthAll`。

#### 彙總

使用公用表表達式(CTE)在建立十位數時段之前將里程聚合在一起。 這提供了特定回顧期的總英里數。 CTE暫時存在，並且僅在較大查詢的範圍內可用。

```sql
summed_miles_1 AS (
    SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
           _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
           SUM(_profilefoundationreportingstg.mileage) AS totalMiles
    FROM airline_loyalty_data
    WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
)
```

塊在模板中重複兩次(`summed_miles_3` 和 `summed_miles_6`)，以便為其他回溯期間生成資料。

請注意查詢的標識、維和度量列(`membershipNumber`。 `loyaltyStatus` 和 `totalMiles` )。

#### 排名

Deciles允許您執行分類分段。 要建立排名編號， `NTILE` 函式與的參數一起使用 `10` 按 `loyaltyStatus` 的子菜單。 這將產生從1到10的排名。 設定 `ORDER BY` 子句 `WINDOW` 至 `DESC` 以確保 `1` 是給 **最大** 維中的度量。

```sql
rankings_1 AS (
    SELECT membershipNumber,
           loyaltyStatus,
           totalMiles,
           NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
    FROM summed_miles_1
)
```

#### 映射聚合

對於多個回溯期間，您需要使用 `MAP_FROM_ARRAYS` 和 `COLLECT_LIST` 的子菜單。 在示例代碼段中， `MAP_FROM_ARRAYS` 使用一對鍵建立映射(`loyaltyStatus`)和值(`decileBucket`)陣列。 `COLLECT_LIST` 返回在指定列中包含所有值的陣列。

```sql
map_1 AS (
    SELECT membershipNumber,
           MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
    FROM rankings_1
    GROUP BY membershipNumber
)
```

>[!NOTE]
>
>如果僅在生存期期間需要分級排序，則不需要映射聚合。

#### 唯一標識

唯一標識清單(`membershipNumber`)是建立所有成員身份的唯一清單所必需的。

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>如果僅在生存期期間需要分級排序，則可以省略此步驟並通過 `membershipNumber` 可以在最後一步中完成。

#### 將所有臨時資料拼接在一起

最後一步是將所有臨時資料縫合成與場組中十字的結構相同的形式。

```sql
SELECT STRUCT(
           all_memberships.membershipNumber AS membershipNumber,
           STRUCT(
                map_1.decileMonth1 AS decileMonth1,
                map_3.decileMonth3 AS decileMonth3,
                map_6.decileMonth6 AS decileMonth6
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM all_memberships
    LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
    LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
    LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
```

如果只有生存期資料可用，則查詢將顯示如下：

```sql
SELECT STRUCT(
           rankings.membershipNumber AS membershipNumber,
           STRUCT(
                MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonthAll
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM rankings
GROUP BY rankings.membershipNumber
```

### 運行查詢模板

查詢可以 [通過UI執行](./ui/user-guide.md#executing-queries) 或 [查詢服務API](./api/queries.md#create-a-query)。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/queries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "dbName": "prod:all",
    "templateId": "{{airline_decile_query_template_id}}",
    "insertIntoParameters": {
        "datasetName": "airline_loyalty_decile"
    }
}'
```

由於使用了十位數，因此在查詢結果中保證了排名數和百分位數之間的相關性。 每個級別等於10%，因此根據前30%的受眾來識別受眾只需將1、2和3級作為目標。

## 後續步驟

Segmentation Service提供用戶介面和REST風格的API，允許您根據這些資料桶生成訪問群。 查看 [分段服務概述](../segmentation/home.md) 有關如何建立、評估和訪問段的資訊。

有關如何在段生成器（分段服務的UI實現）中建立和使用段的詳細資訊，請參閱 [段生成器指南](../segmentation/ui/overview.md)。

有關使用API構建段定義的資訊，請參見上的教程 [使用API建立受眾段](../segmentation/tutorials/create-a-segment.md)。
