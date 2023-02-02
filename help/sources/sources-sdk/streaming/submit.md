---
title: 測試並提交源
description: 以下檔案提供如何使用流量服務API測試和驗證新來源，以及透過自助來源（串流SDK）整合新來源的步驟。
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 0%

---

# 測試並提交源

使用自助來源（串流SDK）將新來源整合至Adobe Experience Platform的最後步驟，是測試並提交您的新來源。 完成連接規範並更新流流規範後，您就可以開始通過API或UI測試源的功能。 成功後，您可以聯絡Adobe代表，提交新來源。

以下檔案提供如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

* 如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../landing/api-guide.md).
* 如需如何產生Platform API認證的詳細資訊，請參閱 [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md).
* 有關如何設定的資訊 [!DNL Postman] 若為Platform API，請參閱以下的教學課程： [設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md).
* 若要協助您進行測試和偵錯程式，請下載 [此處的自助源驗證收集和環境](../assets/sdk-verification.zip) 並遵循下列步驟。

## 使用API測試您的來源

若要使用API測試來源，您必須執行 [自助源驗證收集和環境](../assets/sdk-verification.zip) on [!DNL Postman] 同時提供與源相關的適當環境變數。

若要開始測試，您必須先在上設定集合和環境 [!DNL Postman]. 接下來，指定要測試的連接規範ID。

>[!NOTE]
>
>下列所有範例變數都是您必須更新的預留位置值，但 `flowSpecificationId` 和 `targetConnectionSpecId`，即固定值。

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `x-api-key` | 用來驗證對Experience PlatformAPI呼叫的唯一識別碼。 請參閱 [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以了解如何擷取 `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 擁有或許可產品和服務並允許訪問其成員的公司實體。 請參閱 [設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md) 有關如何檢索 `x-gw-ims-org-id` 資訊。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | 完成對Experience PlatformAPI的呼叫所需的授權Token。 請參閱 [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以了解如何擷取 `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | 為了在Platform中使用來源資料，必須建立目標架構，以根據您的需求來建構來源資料。 如需建立Target XDM結構的詳細步驟，請參閱 [使用API建立結構](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 與您的架構對應的唯一版本。 | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 此 `meta:altId` 與  `schemaId` 建立新結構時。 | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 如需如何建立目標資料集的詳細步驟，請參閱 [使用API建立資料集](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 映射集可用於定義源架構中的資料如何映射到目標架構的資料。 如需如何建立對應的詳細步驟，請參閱 [使用API建立對應集](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 與您的對應集對應的唯一ID。 | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 與源對應的連接規範ID。 這是您在 [建立新的連接規範](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | 流規範ID為 `GenericStreamingAEP`. **這是固定值**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | 擷取的資料登陸所在資料湖的目標連線ID。 **這是固定值**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 檢查流運行是否完成時要遵循的指定時間間隔。 | `40` |
| `startTime` | 資料流的指定開始時間。 開始時間必須採用unix時間格式。 | `1597784298` |

提供所有環境變數後，您就可以開始使用 [!DNL Postman] 介面。 在 [!DNL Postman] 介面，選取點(**...**)旁邊 [!DNL Sources SSSs Verification Collection] 然後選取 **執行集合**.

![跑道](../assets/runner.png)

此 [!DNL Runner] 介面出現，允許您配置資料流的運行順序。 選擇 **運行SSS驗證集合** 來執行集合。

>[!NOTE]
>
>您可以停用 **刪除流量** 如果您偏好在Platform UI中使用來源監控控制面板，請從執行順序檢查清單中選取。 不過，完成測試後，您必須確定已刪除測試流程。

![執行集合](../assets/run-collection.png)

## 使用UI測試您的來源

若要在UI中測試您的來源，請前往Platform UI中貴組織沙箱的來源目錄。 從這裡，您應該會看到新來源顯示在 *串流* 類別。

在沙箱中提供新來源後，您必須依照來源工作流程來測試功能。 若要開始，請選取 **[!UICONTROL 設定]**.

![顯示新流源的源目錄。](../assets/testing/catalog-test.png)

此 [!UICONTROL 新增資料] 步驟。 若要測試您的來源是否可串流資料，請使用介面的左側來上傳 [範例JSON資料](../assets/testing/raw.json.zip). 上傳資料後，介面的右側會更新為資料的檔案階層預覽。 選擇 **[!UICONTROL 下一個]** 繼續。

![在來源工作流程中新增資料步驟，您可在擷取前先上傳和預覽資料。](../assets/testing/add-data-test.png)

此 [!UICONTROL 資料流詳細資訊] 頁面可讓您選取要使用現有資料集或新資料集。 在此程式中，您也可以設定要擷取至設定檔的資料，並啟用下列設定： [!UICONTROL 錯誤診斷] 和 [!UICONTROL 部分擷取].

若要測試，請選取 **[!UICONTROL 新資料集]** 和提供輸出資料集名稱。 在此步驟中，您也可以提供選用說明，以新增更多資訊至資料集。 接下來，使用 [!UICONTROL 進階搜尋] 選項，或透過捲動下拉式選單中的現有結構清單來執行。 選擇架構後，請為資料流提供名稱和說明。

完成後，請選取 **[!UICONTROL 下一個]**.

![源工作流中的資料流詳細步驟。](../assets/testing/dataflow-details-test.png)

此 [!UICONTROL 對應] 步驟，提供您一個介面，將來源架構的來源欄位對應至目標架構中適當的目標XDM欄位。

Platform會根據您選取的目標結構或資料集，為自動對應欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以視需要選擇直接映射欄位，或使用資料準備函式來轉換源資料，以導出計算值或計算值。 有關使用映射器介面和計算欄位的完整步驟，請參閱 [資料準備UI指南](../../../data-prep/ui/mapping.md)

成功映射源資料後，請選擇 **[!UICONTROL 下一個]**.

![源工作流的映射步驟。](../assets/testing/mapping-test.png)

此 **[!UICONTROL 檢閱]** 步驟顯示，允許您在建立新資料流之前對其進行查看。 詳細資料會分組為下列類別：

* **[!UICONTROL 連線]**:顯示您的帳戶名稱、來源類型，以及您所使用串流雲端儲存空間來源的其他特定資訊。
* **[!UICONTROL 指派資料集和對應欄位]**:顯示您用於資料流的目標資料集和架構。

審核資料流後，請選擇 **[!UICONTROL 完成]** 並允許建立資料流的時間。

![來源工作流的審核步驟。](../assets/testing/review-test.png)

最後，您必須檢索資料流的流終結點。 此端點將用於訂閱您的Webhook，讓您的串流來源可與Experience Platform通訊。 若要擷取串流端點，請前往 [!UICONTROL 資料流活動] 資料流的頁，並從資料流的底部複製端點 [!UICONTROL 屬性] 中。

![資料流活動中的流終結點。](../assets/testing/endpoint-test.png)

## 提交您的來源

在您的來源能夠完成整個工作流程後，您可以繼續聯絡您的Adobe代表，並提交您的來源，以便整合其他Experience Platform組織。
