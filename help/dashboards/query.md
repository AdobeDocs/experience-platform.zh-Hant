---
solution: Experience Platform
title: 使用查詢服務來探索、驗證及處理控制面板資料集
type: Documentation
description: 瞭解如何使用查詢服務來探索及處理原始資料集，以便在Experience Platform中強化設定檔、受眾和目的地儀表板。
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# 使用[!DNL Query Service]探索、驗證及處理儀表板資料集

Adobe Experience Platform透過Experience PlatformUI中提供的控制面板，提供您組織設定檔、對象和目的地資料的重要資訊。 您可以使用Adobe Experience Platform [!DNL Query Service]來探索、驗證及處理原始資料集，以便在資料湖中支援這些儀表板。

## 快速入門：[!DNL Query Service]

Adobe Experience Platform [!DNL Query Service]可讓行銷人員使用標準SQL在Data Lake中查詢資料，藉此支援他們取得資料的深入分析。 [!DNL Query Service]提供使用者介面和API，可用來聯結資料湖中的任何資料集，以及將查詢結果擷取為新資料集，以用於報表、機器學習或內嵌至Real-Time Customer Profile。

若要進一步瞭解[!DNL Query Service]及其在Experience Platform中的角色，請先閱讀[[!DNL Query Service] 總覽](../query-service/home.md)。

## 存取可用的資料集

您可以使用[!DNL Query Service]來查詢設定檔、對象和目的地儀表板的原始資料集。 若要檢視您的可用資料集，請在Experience PlatformUI中，選取左側導覽中的&#x200B;**資料集**&#x200B;以開啟資料集儀表板。 控制面板會列出貴組織的所有可用資料集。 系統會顯示每個列出資料集的詳細資料，包括其名稱、資料集所遵守的結構描述，以及最近一次擷取執行的狀態。

![左側導覽中反白顯示「資料集」索引標籤的資料集瀏覽儀表板。](./images/query/browse-datasets.png)

### 系統產生的資料集 {#system-generated-datasets}

>[!IMPORTANT]
>
>預設會隱藏系統產生的資料集。 依預設，[!UICONTROL 瀏覽]索引標籤只會顯示您已擷取資料的資料集。

若要檢視系統產生的資料集，請選取篩選圖示(![篩選圖示。](/help/images/icons/filter.png))位於搜尋列左側。

![資料集瀏覽索引標籤中反白顯示篩選圖示。](./images/query/filter-datasets.png)

側邊欄會顯示兩個切換： [!UICONTROL 包含在設定檔]中，以及[!UICONTROL 顯示系統資料集]。 選取[!UICONTROL 顯示系統資料集]的切換按鈕，將系統產生的資料集納入資料集的可瀏覽清單中。

![反白顯示[顯示系統資料集]切換的[資料集瀏覽]索引標籤。](./images/query/show-system-datasets.png)

### 設定檔屬性資料集 {#profile-attribute-datasets}

設定檔儀表板分析會繫結至貴組織所定義的合併原則。 對於每個使用中的合併原則，資料湖中都會有一個可用的設定檔屬性資料集。

這些資料集的命名慣例是&#x200B;**Profile-Snapshot-Export**，後面接著系統產生的隨機英數字值。 例如： `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`。

若要瞭解每個設定檔快照集匯出資料集的完整結構描述，您可以在Experience PlatformUI中使用資料集檢視器](../catalog/datasets/user-guide.md)來預覽及探索資料集[。

![設定檔快照集匯出資料集的預覽。](images/query/profile-attribute.png)

#### 將設定檔屬性資料集對應到合併原則ID

指派給每個系統產生之設定檔屬性資料集的英數字元值是一個隨機字串，可對應至您的組織所建立的其中一個合併原則ID。 在`adwh_dim_merge_policies`資料集中維持每個合併原則ID與其相關設定檔屬性資料集字串的對應。

`adwh_dim_merge_policies`資料集包含下列欄位：

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

您可以在Experience Platform中使用查詢編輯器UI探索此資料集。 若要進一步瞭解如何使用查詢編輯器，請參閱[查詢編輯器UI指南](../query-service/ui/user-guide.md)。

### 對象中繼資料資料集

資料湖中有可用的對象中繼資料資料集，其中包含您組織的每個對象的中繼資料。

此資料集的命名慣例是&#x200B;**Segmentdefinition-Snapshot-Export**，後面接著英數字值。 例如︰`Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

若要瞭解每個區段定義快照匯出資料集的完整結構描述，您可以在Experience PlatformUI中使用資料集檢視器](../catalog/datasets/user-guide.md)來預覽及探索資料集[。

### 目的地中繼資料資料集

貴組織所有已啟用目的地的中繼資料都可在Data Lake中作為原始資料集使用。

此資料集的命名慣例是&#x200B;**DIM_Destination**。

若要瞭解DIM目的地資料集的完整結構描述，您可以在Experience PlatformUI中使用資料集檢視器](../catalog/datasets/user-guide.md)預覽及探索資料集[。

![DIM_Destination資料集的預覽。](images/query/destinations-metadata.png)

## 客戶資料平台(CDP)前瞻分析報表

CDP分析資料模型功能會公開SQL，為各種設定檔、目的地和分段Widget提供深入分析。 您可以自訂這些SQl查詢範本，為您的行銷和KPI使用案例建立CDP報告。

CDP報告可提供您個人檔案資料及其與受眾和目的地關係的深入分析。 請參閱CDP見解資料模型檔案，以取得如何[將CDP見解資料模型套用至您的特定KPI使用案例](./data-models/cdp-insights-data-model-b2c.md)的詳細資訊。

## 範例查詢

下列範例查詢包含可以在[!DNL Query Service]中使用的範例SQL，以探索、驗證及處理支援您儀表板的原始資料集。

### 依身分割槽分的設定檔計數

此設定檔分析提供資料集中所有合併設定檔的身分劃分。

>[!NOTE]
>
>依身分割槽分的設定檔總數（也就是將每個名稱空間顯示的值相加）可能會高於合併的設定檔總數，因為一個設定檔可能會有多個相關聯的名稱空間。 例如，如果客戶在多個頻道上與您的品牌互動，則多個名稱空間會與該個別客戶相關聯。

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

### 依受眾區分的設定檔計數

此對象分析提供資料集中每個對象內的合併設定檔總數。 此數字是將對象合併原則套用至您的設定檔資料，以將設定檔片段合併在一起，為對象中的每個人形成單一設定檔的結果。

```sql
Select          
        concat_ws('-', key, source_namespace) audience_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Audiencemembership)
                  from
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      audience_id
```

## 後續步驟

閱讀本指南後，您現在可以使用[!DNL Query Service]執行數個查詢，以探索及處理原始資料集，為您的設定檔、對象和目的地儀表板提供支援。

若要深入瞭解每個儀表板及其量度，請從檔案導覽的可用儀表板清單中選取儀表板。
