---
title: Test並提交源
description: 以下文檔提供了如何使用流服務APItest和驗證新源並通過自服務源（流SDK）整合新源的步驟。
hide: true
hidefromtoc: true
exl-id: 2ae0c3ad-1501-42ab-aaaa-319acea94ec2
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 0%

---

# Test並提交源

使用自助源（流式SDK）將新源整合到Adobe Experience Platform的最後步驟是test並提交新源。 完成連接規範並更新流流規範後，可以通過API或UI開始測試源的功能。 成功後，您可以聯繫Adobe代表來提交新來源。

以下文檔提供了有關如何使用test和調試源的步驟 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

* 有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../landing/api-guide.md)。
* 有關如何為平台API生成憑據的資訊，請參見上的教程 [驗證和訪問Experience PlatformAPI](../../../landing/api-authentication.md)。
* 有關如何設定的資訊 [!DNL Postman] 有關平台API，請參見上的教程 [設定開發人員控制台和 [!DNL Postman]](../../../landing/postman.md)。
* 要幫助測試和調試過程，請下載 [此處的自助源驗證收集和環境](../assets/sdk-verification.zip) 並按照下面介紹的步驟操作。

## 使用APItest源

要使用APItest源，必須運行 [自助源驗證收集和環境](../assets/sdk-verification.zip) 上 [!DNL Postman] 同時提供與源相關的相應環境變數。

要開始測試，必須先在 [!DNL Postman]。 接下來，指定要test的連接規範ID。

>[!NOTE]
>
>下面的所有示例變數都是必須更新的佔位符值， `flowSpecificationId` 和 `targetConnectionSpecId`，它們是固定值。

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `x-api-key` | 用於驗證對Experience PlatformAPI的調用的唯一標識符。 請參閱上的教程 [驗證和訪問Experience PlatformAPI](../../../landing/api-authentication.md) 有關如何檢索 `x-api-key`。 | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 擁有或許可產品和服務並允許訪問其成員的公司實體。 請參閱上的教程 [設定開發人員控制台和 [!DNL Postman]](../../../landing/postman.md) 有關如何檢索 `x-gw-ims-org-id` 的下界。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | 完成對Experience PlatformAPI的調用所需的授權令牌。 請參閱上的教程 [驗證和訪問Experience PlatformAPI](../../../landing/api-authentication.md) 有關如何檢索 `authorizationToken`。 | `Bearer authorizationToken` |
| `schemaId` | 為了在平台中使用源資料，必須建立目標架構以根據您的需要來構造源資料。 有關如何建立目標XDM架構的詳細步驟，請參見上的教程 [使用API建立架構](../../../xdm/api/schemas.md)。 | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 與架構對應的唯一版本。 | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 的 `meta:altId` 在它旁邊  `schemaId` 建立新架構時。 | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 有關如何建立目標資料集的詳細步驟，請參見上的教程 [使用API建立資料集](../../../catalog/api/create-dataset.md)。 | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 映射集可用於定義源模式中的資料如何映射到目標模式的資料。 有關如何建立映射的詳細步驟，請參見上的教程 [使用API建立映射集](../../../data-prep/api/mapping-set.md)。 | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 與映射集對應的唯一ID。 | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 與源對應的連接規範ID。 這是您在 [建立新連接規範](./create.md)。 | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | 流規範ID `GenericStreamingAEP`。 **這是一個固定值**。 | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | 所接收資料到達的資料湖的目標連接ID。 **這是一個固定值**。 | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 檢查流運行是否完成時要遵循的指定時間間隔。 | `40` |
| `startTime` | 資料流的指定開始時間。 開始時間必須在unix時間中格式化。 | `1597784298` |

提供所有環境變數後，可以使用 [!DNL Postman] 。 在 [!DNL Postman] 介面，選取橢圓(**...**) [!DNL Sources SSSs Verification Collection] ，然後選擇 **運行集合**。

![跑](../assets/runner.png)

的 [!DNL Runner] 介面，允許您配置資料流的運行順序。 選擇 **運行SSS驗證收集** 以運行集合。

>[!NOTE]
>
>可以禁用 **刪除流** 從運行訂單核對清單中，如果您希望使用平台UI中的源監視面板。 但是，完成測試後，必須確保刪除test流。

![運行集合](../assets/run-collection.png)

## 使用UItest源

要在UI中test源，請轉到平台UI中組織沙盒的源目錄。 在此處，您應看到新源出現在 *流* 的子菜單。

新源現在可在沙箱中使用，您必須遵循源工作流來test功能。 要開始，請選擇 **[!UICONTROL 設定]**。

![顯示新流源的源目錄。](../assets/testing/catalog-test.png)

的 [!UICONTROL 添加資料] 的上界。 要test源可以流式傳輸資料，請使用介面左側上載 [示例JSON資料](../assets/testing/raw.json.zip)。 上載資料後，介面的右側將更新到資料的檔案層次結構的預覽中。 選擇 **[!UICONTROL 下一個]** 繼續。

![在源工作流中添加資料步驟，您可以在接收之前上載和預覽資料。](../assets/testing/add-data-test.png)

的 [!UICONTROL 資料流詳細資訊] 頁允許您選擇是使用現有資料集還是使用新資料集。 在此過程中，您還可以配置要接收到配置檔案的資料，並啟用設定，如 [!UICONTROL 錯誤診斷] 和 [!UICONTROL 部分攝取]。

要測試，請選擇 **[!UICONTROL 新資料集]** 並提供輸出資料集名稱。 在此步驟中，您還可以提供可選說明，以向資料集添加詳細資訊。 接下來，選擇要映射到的方案 [!UICONTROL 高級搜索] 選項，或通過在下拉菜單中滾動現有架構清單來執行。 選擇架構後，請提供資料流的名稱和說明。

完成後，選擇 **[!UICONTROL 下一個]**。

![源工作流中的資料流詳細資訊步驟。](../assets/testing/dataflow-details-test.png)

的 [!UICONTROL 映射] 步驟，提供一個介面，用於將源欄位從源架構映射到目標架構中相應的目標XDM欄位。

平台根據您選擇的目標架構或資料集為自動映射欄位提供智慧建議。 您可以手動調整映射規則以適合您的使用情形。 根據您的需要，您可以選擇直接映射欄位，或使用資料準備函式轉換源資料以導出計算值或計算值。 有關使用映射器介面和計算欄位的全面步驟，請參見 [資料準備UI指南](../../../data-prep/ui/mapping.md)

成功映射源資料後，選擇 **[!UICONTROL 下一個]**。

![源工作流的映射步驟。](../assets/testing/mapping-test.png)

的 **[!UICONTROL 審閱]** 步驟，允許您在建立新資料流之前查看它。 詳細資訊按以下類別分組：

* **[!UICONTROL 連接]**:顯示您的帳戶名、源類型以及特定於您正在使用的流式雲儲存源的其他雜項資訊。
* **[!UICONTROL 分配資料集和映射欄位]**:顯示您用於資料流的目標資料集和方案。

查看資料流後，選擇 **[!UICONTROL 完成]** 並為建立資料流留出一些時間。

![源工作流的審閱步驟。](../assets/testing/review-test.png)

最後，必須檢索資料流的流終結點。 此終結點將用於訂閱Webhook，允許流源與Experience Platform通信。 要檢索流終結點，請轉到 [!UICONTROL 資料流活動] 剛建立的資料流的頁，並從 [!UICONTROL 屬性] 的子菜單。

![資料流活動中的流終結點。](../assets/testing/endpoint-test.png)

## 提交源

在您的來源能夠完成整個工作流後，您可以繼續與Adobe代表聯繫，並提交您的來源，以便與其他Experience Platform組織整合。
