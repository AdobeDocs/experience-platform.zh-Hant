---
title: 從Real-Time CDP匯出陣列、地圖和物件
type: Tutorial
description: 瞭解如何從Real-Time CDP將陣列、地圖和物件匯出至雲端儲存空間目標。
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 13%

---

# 從Real-Time CDP匯出陣列、地圖和物件 {#export-arrays-cloud-storage}

>[!AVAILABILITY]
>
>將陣列和其他複雜物件匯出至雲端儲存空間的功能通常適用於下列目的地： [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)、[[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)、[[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)、[[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md)、[[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md)、[[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md)。
>
>此外，您可以將對應型別欄位匯出至下列目的地： [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)、[HTTP API](/help/destinations/catalog/streaming/http-destination.md)、[Azure事件中樞](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)、[Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)。


瞭解如何從Real-Time CDP將陣列、地圖和物件匯出至[雲端儲存空間目的地](/help/destinations/catalog/cloud-storage/overview.md)。 此外，您可以將對應型別欄位匯出至[企業目的地](/help/destinations/destination-types.md#advanced-enterprise-destinations)和有限的[邊緣個人化目的地](/help/destinations/destination-types.md#edge-personalization-destinations)。 請參閱本檔案以瞭解匯出工作流程、此功能啟用的使用案例和已知限制。 檢視下表以瞭解每種目的地型別可用的功能。

| 目的地型別 | 可匯出陣列、地圖和其他自訂物件 |
|---|---|
| Adobe編寫的雲端儲存空間目標(Amazon S3、Azure Blob、Azure Data Lake Storage Gen2、資料登陸區、Google雲端儲存空間、SFTP) | 可以，在設定目的地連線時，啟用陣列、地圖和物件的匯出切換功能會開啟。 |
| 檔案式電子郵件行銷目的地(Adobe Campaign、Oracle Eloqua、Oracle Responsys、Salesforce Marketing Cloud) | 無 |
| 現有自訂合作夥伴建置的雲端儲存空間目的地(透過Destination SDK建置的自訂檔案型目的地) | 無 |
| 企業目的地(Amazon Kinesis、Azure事件中樞、HTTP API) | 部分。 您可以在啟動工作流程的對應步驟中選取和匯出對應型別物件。 |
| 串流目的地(例如：Facebook、Braze、Google Customer Match等) | 無 |
| Edge個人化目標(Adobe Target) | 部分。 您可以在啟動工作流程的對應步驟中選取和匯出對應型別物件。 |

{style="table-layout:auto"}

請考量此頁面，您可以前往想瞭解如何從Experience Platform匯出陣列、地圖和其他物件型別的任何位置。

## 底線在前面

取得本節中有關功能的最重要資訊，然後繼續參閱檔案中的其他章節，以取得詳細資訊。

* 對於雲端儲存空間目的地，匯出陣列、地圖和物件的功能取決於您選取的&#x200B;**匯出陣列、地圖、物件**&#x200B;切換。 請在頁面](#export-arrays-maps-objects-toggle)的下一頁閱讀更多相關資訊[。
* 您可以匯出陣列、地圖和物件至`JSON`和`Parquet`檔案中的雲端儲存體目的地。 對於Enterprise和Edge個人化目的地，匯出的資料型別為`JSON`。 支援人員和潛在客戶對象，但不支援帳戶對象。
* 針對以檔案為基礎的雲端儲存目的地，您&#x200B;*可以*&#x200B;將陣列、對應和物件匯出至CSV檔案，但僅透過使用計算欄位功能並使用`array_to_string`功能將它們串連到字串中。

## Experience Platform中的陣列和其他物件型別 {#arrays-strings-other-objects}

在Experience Platform中，您可以使用[XDM結構描述](/help/xdm/home.md)來管理不同的欄位型別。 在新增支援陣列匯出功能之前，您能夠將簡單的索引鍵/值組型別欄位（例如字串）從Experience Platform匯出至您想要的目的地。 先前支援匯出的欄位範例為`personalEmail.address`：`johndoe@acme.org`。

Experience Platform中的其他欄位型別包含陣列欄位。 深入瞭解[如何在Experience Platform UI](/help/xdm/ui/fields/array.md)中管理陣列欄位。 您現在可以匯出陣列物件，例如下列範例。

```
organizations = [{
  id: 123,
  orgName: "Acme Inc",
  founded: 1990,
  latestInteraction: "2024-02-16"
}, {
  id: 456,
  orgName: "Superstar Inc",
  founded: 2004,
  latestInteraction: "2023-08-25"
}, {
  id: 789,
  orgName: 'Energy Corp',
  founded: 2021,
  latestInteraction: "2024-09-08"
}]
```

除了陣列之外，您也可以從Experience Platform將地圖和物件匯出至您想要的雲端儲存空間目的地。 深入瞭解Experience Platform中的[對應](/help/xdm/ui/fields/map.md)和[物件](/help/xdm/ui/fields/object.md)。

## 先決條件 {#prerequisites}

[連線](/help/destinations/ui/connect-destination.md)至所需的雲端儲存空間目的地，完成雲端儲存空間目的地的[啟動步驟](/help/destinations/ui/activate-batch-profile-destinations.md)並到達[對應](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)步驟。 連線到所需的雲端目的地時，您必須選取&#x200B;**[!UICONTROL 匯出陣列、對應、物件]**&#x200B;切換開啟。 如需詳細資訊，請參閱以下章節。

>[!NOTE]
>
>對於企業和邊緣個人化目的地，無需選取&#x200B;**[!UICONTROL 匯出陣列、對應、物件]**&#x200B;切換即可使用對映型別欄位的匯出支援。 連線到這些型別的目的地時，無法使用或需要此切換按鈕。

## 匯出陣列、對應及物件的切換開關 {#export-arrays-maps-objects-toggle}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_maps_objects"
>title="匯出陣列、對應及物件"
>abstract="<p> 將此設定切換為<b>開啟</b>，便可以將陣列、對應及物件匯出至 JSON 或 Parquet 檔案。您可以在對應步驟的來源欄位視圖中選取這些物件類型。在切換為開啟的情況下，您無法在對應步驟中使用計算欄位選項。</p><p>將這項設定切換為<b>關閉</b>後，即可使用計算欄位選項並在啟動客群時套用各種資料轉換函數。但是，您<i>不能</i>將陣列、對應和物件匯出至 JSON 或 Parquet 檔案，並且必須設定不同的目的地才能達成該目的。</p>"

連線到以檔案為基礎的雲端儲存空間目的地時，您可以設定&#x200B;**[!UICONTROL 匯出陣列、地圖、物件]**&#x200B;的開啟或關閉。

![以開啟或關閉設定以及反白彈出視窗來顯示匯出陣列、地圖、物件切換。](/help/destinations/assets/ui/export-arrays-calculated-fields/export-objects-toggle.gif)

將此設定切換為&#x200B;**開啟**，便可以將陣列、對應及物件匯出至 JSON 或 Parquet 檔案。啟用受眾至雲端儲存空間目的地時，您可以在[對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)的來源欄位檢視中選取這些物件型別。 不過，若開啟此設定，您就無法於啟用時使用計算欄位選項來轉換資料。

將這項設定切換為&#x200B;**關閉**&#x200B;後，即可使用計算欄位選項並在啟動客群時套用各種資料轉換函數。不過，您無法將陣列、地圖和物件匯出至JSON或Parquet檔案，且必須為此設定個別的目的地。

## 匯出陣列、地圖、物件切換&#x200B;*開啟* {#export-arrays-maps-objects-toggle-on}

開啟此設定後，您可以透過啟動工作流程對應步驟中的來源欄位選取器來選取物件，以匯出整個物件（例如`person.name`）和陣列。

![透過啟動工作流程對應步驟中的來源欄位選擇器選取物件。](/help/destinations/assets/ui/export-arrays-calculated-fields/select-object.gif)

選取此選項後，使用者介面會封鎖使用者無法使用計算欄位，而且&#x200B;**[!UICONTROL 新增計算欄位]**&#x200B;控制項已停用，如下所示。 若要使用計算欄位進行資料轉換，請在關閉切換功能的情況下設定目的地連線。

![已停用計算欄位控制項。](/help/destinations/assets/ui/export-arrays-calculated-fields/calculated-fields-disabled.png)

## 匯出陣列、地圖、物件切換&#x200B;*關閉* {#export-arrays-maps-objects-toggle-off}

此選項設為&#x200B;*off*&#x200B;時，您可以使用計算欄位選項並在啟用對象時套用各種資料轉換函式。 不過，您無法將陣列、地圖和物件匯出至JSON或Parquet檔案，且必須為此設定個別的目的地。

您可以&#x200B;*使用計算欄位功能，將陣列、對應和物件*&#x200B;匯出至CSV檔案，並使用`array_to_string`函式將它們串連至字串。 [閱讀有關使用該函式的詳細資訊](#array-to-string-function-export-arrays)。

深入瞭解如何使用計算欄位，以[對匯出至雲端儲存空間目的地的資料執行轉換](/help/destinations/ui/data-transformations-calculated-fields.md)。

## 匯出檔案範例 {#sample-exported-files}

透過使用此功能，您可以匯出Parquet和JSON檔案，其中的資料會保留Experience Platform中的結構。 檢視匯出的JSON檔案範例下方。

+++ 選取以檢視匯出的JSON檔案。

```json
{
  "person_name_firstName": "John",
  "person_name_lastName": "Smith",
  "_acmeinc_customer_hs_main_address_scalar": "Oak Avenue No 12",
  "_acmeinc_customer_hs_locations_array": [
    "home address 12",
    "office address 12"
  ],
  "_acmeinc_customer_hs_date_array": [
    "2024-11-14",
    "2024-11-15"
  ],
  "_acmeinc_customer_hs_customer_obj_emails_array0": "john.smith@example.com",
  "_acmeinc_customer_hs_customer_obj": {
    "emails_array": [
      "john.smith@example.com",
      "j.smith@example.com"
    ],
    "name_scalar": "John Smith"
  },
  "_acmeinc_customer_hs_addresses_array_obj": [
    {
      "is_primary": true,
      "streetName_scalar": "Maple Street",
      "streetNo_int": 12
    },
    {
      "is_primary": false,
      "streetName_scalar": "Pine Road",
      "streetNo_int": 45
    }
  ],
  "_acmeinc_customer_hs_addresses_array_obj0": {
    "is_primary": true,
    "streetName_scalar": "Maple Street",
    "streetNo_int": 12
  }
}
```

+++