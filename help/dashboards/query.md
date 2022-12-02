---
solution: Experience Platform
title: 使用Query Service探索、驗證及處理控制面板資料集
type: Documentation
description: 了解如何使用Query Service探索及處理原始資料集，在Experience Platform中支援設定檔、區段和目的地控制面板。
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: 4826731682bcaf5a43c7ce047220c1805d97243a
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---

# 探索、驗證和處理控制面板資料集，使用 [!DNL Query Service]

Adobe Experience Platform可透過Experience PlatformUI中的控制面板，提供貴組織的設定檔、區段和目的地資料的重要資訊。 然後您就可以使用Adobe Experience Platform [!DNL Query Service] 探索、驗證和處理資料湖中支援這些控制面板的原始資料集。

## 開始使用 [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] 支援行銷人員運用標準SQL在資料湖中查詢資料，從其資料中獲得深入分析。 [!DNL Query Service] 提供使用者介面和API，可用來加入資料湖中的任何資料集，並將查詢結果擷取為新資料集，以用於報表、機器學習或內嵌至即時客戶設定檔。

若要深入了解 [!DNL Query Service] 及其在Experience Platform中的作用，請先閱讀 [[!DNL Query Service] 概述](../query-service/home.md).

## 存取可用的資料集

您可以使用 [!DNL Query Service] 查詢設定檔、區段和目的地控制面板的原始資料集。 若要檢視可用的資料集，請在Experience PlatformUI中選取 **資料集** 在左側導覽中，開啟「資料集」控制面板。 控制面板會列出貴組織的所有可用資料集。 系統會顯示每個列出資料集的詳細資訊，包括其名稱、資料集所遵守的結構，以及最新擷取執行的狀態。

![「資料集瀏覽」控制面板，左側導覽中強調顯示「資料集」索引標籤。](./images/query/browse-datasets.png)

### 系統產生的資料集

>[!IMPORTANT]
>
>系統產生的資料集預設為隱藏。 依預設， [!UICONTROL 瀏覽] 索引標籤只會顯示您已將資料匯入的資料集。

若要檢視系統產生的資料集，請選取篩選圖示(![篩選圖示。](./images/query/filter.png))。

![反白顯示篩選圖示的「資料集瀏覽」標籤。](./images/query/filter-datasets.png)

邊欄隨即出現，其中包含兩個切換 [!UICONTROL 包含在設定檔中] 和 [!UICONTROL 顯示系統資料集]. 選取切換 [!UICONTROL 顯示系統資料集] 將系統產生的資料集納入資料集的可瀏覽清單中。

![「資料集瀏覽」索引標籤中，「顯示系統資料集」會切換為反白顯示。](./images/query/show-system-datasets.png)

### 設定檔屬性資料集

設定檔控制面板分析會與貴組織已定義的合併原則系結。 對於每個活動的合併策略，資料湖中都有一個可用的配置檔案屬性資料集。

這些資料集的命名慣例為 **配置檔案快照導出** 隨後是系統產生的隨機英數字值。 例如: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

若要了解每個設定檔快照匯出資料集的完整結構，您可以預覽和探索資料集 [使用資料集檢視器](../catalog/datasets/user-guide.md) 在Experience PlatformUI中。

![設定檔快照導出資料集的預覽。](images/query/profile-attribute.png)

#### 將配置檔案屬性資料集映射到合併策略ID

分配給每個系統生成的配置檔案屬性資料集的字母數字值是隨機字串，它映射到貴組織建立的其中一個合併策略的合併策略ID。 每個合併策略ID與其相關配置檔案屬性資料集字串的映射在 `adwh_dim_merge_policies` 資料集。

此 `adwh_dim_merge_policies` 資料集包含下列欄位：

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

您可以在Experience Platform中使用查詢編輯器UI來探索此資料集。 若要進一步了解使用查詢編輯器，請參閱 [查詢編輯器UI指南](../query-service/ui/user-guide.md).

### 區段中繼資料資料集

資料湖中有可用的區段中繼資料資料集，內含組織每個區段的中繼資料。

此資料集的命名慣例為 **Segmentdefinition-Snapshot-Export** 後接英數字元值。 例如︰`Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

若要了解每個區段定義快照匯出資料集的完整結構，您可以預覽和探索資料集 [使用資料集檢視器](../catalog/datasets/user-guide.md) 在Experience PlatformUI中。

![Segmentdefinition-Snapshot-Export資料集的預覽。](images/query/segment-metadata.png)

### 目的地中繼資料資料集

您組織所有啟動目的地的中繼資料都可作為資料湖的原始資料集使用。

此資料集的命名慣例為 **DIM_Destination**.

若要了解DIM目標資料集的完整結構，您可以預覽和探索資料集 [使用資料集檢視器](../catalog/datasets/user-guide.md) 在Experience PlatformUI中。

![DIM_Destination資料集的預覽。](images/query/destinations-metadata.png)

## （測試版）客戶資料平台(CDP)深入分析報表

>[!IMPORTANT]
>
>CDP Insights Data Models功能正在測試中。 其功能和檔案可能會有所變更。

CDP Insights Data Models功能可公開SQL，為各種設定檔、目標和細分小工具提供深入分析。 您可以自定義這些SQl查詢模板，以為您的市場營銷和KPI使用案例建立CDP報告。

CDP報告可深入分析您的設定檔資料及其與區段和目的地的關係。 如需如何取得的詳細資訊，請參閱CDP Insights資料模型檔案 [將CDP Insights資料模型套用至您的特定KPI使用案例](./cdp-insights-data-model.md).

## 範例查詢

下列範例查詢包含可用於 [!DNL Query Service] 探索、驗證及處理可支援控制面板的原始資料集。

### 依身分的設定檔計數

此設定檔分析可提供資料集中所有合併設定檔的身分劃分。

>[!NOTE]
>
>依身分劃分的設定檔總數（換句話說，將每個命名空間顯示的值加總）可能高於合併的設定檔總數，因為一個設定檔可能有多個相關聯的命名空間。 例如，如果客戶在多個管道上與您的品牌互動，則多個命名空間將會與該個別客戶相關聯。

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
              Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
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
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      segment_id
```

## 後續步驟

閱讀本指南後，您現在可以使用 [!DNL Query Service] 若要執行數個查詢，以探索及處理支援設定檔、區段和目的地控制面板的原始資料集。

若要進一步了解每個控制面板及其量度，請在檔案導覽中，從可用控制面板清單中選取控制面板。
