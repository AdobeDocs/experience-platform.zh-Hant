---
title: 測試並提交您的Source
description: 以下檔案提供如何使用Flow Service API測試及驗證新來源，以及透過Self-Serve Sources (Streaming SDK)整合新來源的步驟。
exl-id: 2ae0c3ad-1501-42ab-aaaa-319acea94ec2
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# 測試並提交您的來源

>[!NOTE]
>
>自助來源串流SDK為測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

使用自助式來源（串流SDK）將新來源整合到Adobe Experience Platform的最後步驟，是測試並提交您的新來源。 當您完成連線規格並更新串流流程規格後，您就可以開始透過API或UI測試來源的功能。 成功後，您可以連絡您的Adobe代表以提交新的來源。

以下檔案提供如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)測試及偵錯來源的步驟。

## 快速入門

* 如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../landing/api-guide.md)的指南。
* 如需如何產生Platform API認證的詳細資訊，請參閱有關[驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md)的教學課程。
* 如需如何設定Platform API [!DNL Postman]的相關資訊，請參閱[設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md)上的教學課程。
* 若要協助您的測試和偵錯程式，請在此下載[自助來源驗證集合和環境](../assets/sdk-verification.zip)，並遵循下列步驟。

## 使用API測試您的來源

若要使用API測試您的來源，您必須在[!DNL Postman]上執行[自助來源驗證集合和環境](../assets/sdk-verification.zip)，同時提供與您的來源相關的適當環境變數。

若要開始測試，您必須先在[!DNL Postman]上設定集合和環境。 接著，指定您要測試的連線規格ID。

>[!NOTE]
>
>以下所有範例變數都是您必須更新的預留位置值，`flowSpecificationId`和`targetConnectionSpecId`除外，它們是固定值。

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `x-api-key` | 用於驗證對Experience Platform API的呼叫的唯一識別碼。 如需如何擷取`x-api-key`的詳細資訊，請參閱[驗證及存取Experience PlatformAPI](../../../landing/api-authentication.md)的教學課程。 | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 企業實體，可以擁有或授權產品及服務並允許存取其成員。 如需如何擷取`x-gw-ims-org-id`資訊的說明，請參閱[設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md)的教學課程。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | 完成對Experience Platform API的呼叫所需的授權權杖。 如需如何擷取`authorizationToken`的詳細資訊，請參閱[驗證及存取Experience PlatformAPI](../../../landing/api-authentication.md)的教學課程。 | `Bearer authorizationToken` |
| `schemaId` | 為了在Platform中使用來源資料，必須建立目標結構描述，以根據您的需求來建構來源資料。 如需有關如何建立目標XDM結構描述的詳細步驟，請參閱有關使用API [建立結構描述的教學課程](../../../xdm/api/schemas.md)。 | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 與您的結構描述對應的唯一版本。 | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 建立新結構描述時與`schemaId`一併傳回的`meta:altId`。 | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 如需有關如何建立目標資料集的詳細步驟，請參閱有關[使用API建立資料集](../../../catalog/api/create-dataset.md)的教學課程。 | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 對應集可用來定義來源結構描述中的資料如何對應到目的地結構描述的資料。 如需有關如何建立對應的詳細步驟，請參閱有關[使用API建立對應集的教學課程](../../../data-prep/api/mapping-set.md)。 | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 與對應集對應的唯一ID。 | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 與您的來源對應的連線規格ID。 這是您在[建立新連線規格](./create.md)後產生的ID。 | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | `GenericStreamingAEP`的流程規格識別碼。 **這是固定值**。 | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | 擷取的資料著陸所在資料湖的目標連線ID。 **這是固定值**。 | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 檢查流程執行的完成時要遵循的指定時間間隔。 | `40` |
| `startTime` | 為資料流指定的開始時間。 開始時間的格式必須是unix時間。 | `1597784298` |

提供所有環境變數後，您就可以使用[!DNL Postman]介面開始執行集合。 在[!DNL Postman]介面中，選取[!DNL Sources SSSs Verification Collection]旁的省略符號(**...**)，然後選取&#x200B;**執行集合**。

![執行者](../assets/runner.png)

[!DNL Runner]介面會出現，可讓您設定資料流的執行順序。 選取&#x200B;**執行SSS驗證集合**&#x200B;以執行集合。

>[!NOTE]
>
>如果您偏好使用Platform UI中的來源監視儀表板，可以停用執行訂單檢查清單中的&#x200B;**刪除流程**。 不過，一旦完成測試，您必須確保已刪除測試流程。

![run-collection](../assets/run-collection.png)

## 使用UI測試您的來源

若要在UI中測試您的來源，請前往Platform UI中您組織沙箱的來源目錄。 從這裡，您應該會看到新來源出現在&#x200B;*串流*&#x200B;類別下。

由於您的沙箱中現在有您的新來源，您必須遵循來源工作流程以測試功能。 若要開始，請選取&#x200B;**[!UICONTROL 設定]**。

![顯示新串流來源的來源目錄。](../assets/testing/catalog-test.png)

[!UICONTROL 新增資料]步驟隨即顯示。 若要測試您的來源是否可以串流資料，請使用介面的左側來上傳[範例JSON資料](../assets/testing/raw.json.zip)。 上傳資料後，介面的右側會更新為資料的檔案階層預覽。 選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

![來源工作流程中的新增資料步驟，您可以在其中上傳資料並在擷取之前預覽。](../assets/testing/add-data-test.png)

[!UICONTROL 資料流詳細資料]頁面可讓您選取要使用現有資料集還是新資料集。 在此程式中，您也可以設定要擷取至設定檔的資料，並啟用[!UICONTROL 錯誤診斷]和[!UICONTROL 部分擷取]之類的設定。

若要進行測試，請選取&#x200B;**[!UICONTROL 新資料集]**，並提供輸出資料集名稱。 在此步驟中，您也可以提供選用的說明，將更多資訊新增至資料集。 接下來，使用[!UICONTROL 進階搜尋]選項，或捲動下拉式選單中的現有結構描述清單，選取要對應的結構描述。 選取結構描述後，請為資料流提供名稱和說明。

完成後，選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程中的資料流詳細資料步驟。](../assets/testing/dataflow-details-test.png)

[!UICONTROL 對應]步驟出現，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

Platform會根據您選取的目標結構或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以根據自己的需求，選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算或計算的值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱[資料準備UI指南](../../../data-prep/ui/mapping.md)

成功對應來源資料後，請選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的對應步驟。](../assets/testing/mapping-test.png)

**[!UICONTROL 檢閱]**&#x200B;步驟隨即顯示，可讓您在建立新資料流之前先檢閱該資料流。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示您的帳戶名稱、來源型別，以及您所使用串流雲端儲存空間來源的其他特定資訊。
* **[!UICONTROL 指派資料集和對應欄位]**：顯示您用於資料流的目標資料集和結構描述。

檢閱您的資料流後，請選取&#x200B;**[!UICONTROL 完成]**，並等待一些時間來建立資料流。

![來源工作流程的稽核步驟。](../assets/testing/review-test.png)

最後，您必須擷取資料流的串流端點。 此端點將用於訂閱您的webhook，允許您的串流來源與Experience Platform通訊。 若要擷取您的串流端點，請移至您剛建立之資料流的[!UICONTROL 資料流活動]頁面，並從[!UICONTROL 屬性]面板底部複製端點。

![資料流活動中的串流端點。](../assets/testing/endpoint-test.png)

## 提交您的來源

您的來源能夠完成整個工作流程後，您可以繼續聯絡您的Adobe代表，並提交您的來源，以跨其他Experience Platform組織整合。
