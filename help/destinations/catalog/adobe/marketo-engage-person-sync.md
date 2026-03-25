---
title: Marketo Engage人員同步
description: 使用Marketo Engage Person Sync聯結器將個人對象的更新串流至Marketo Engage中的對應記錄。
last-substantial-update: 2025-01-14T00:00:00Z
badgeBeta: label="Beta" type="Informative"
exl-id: 2c909633-b169-4ec8-9f58-276395cb8df2
source-git-commit: 20427c4c8826905a77fac04d055d523b12a6f739
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 6%

---

# Marketo Engage人員同步連線 {#marketo-engage-person-sync}

>[!IMPORTANT]
>
>此目標連接器為測試版，僅供精選客戶使用。如欲請求存取權，請和您的 Adobe 代表聯絡。

>[!IMPORTANT]
>
>**[!UICONTROL Marketo Engage Person Sync]**&#x200B;目的地卡片將於&#x200B;**2025年10月**&#x200B;日淘汰。
>
>若要確保順利轉換至新的&#x200B;**[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)**&#x200B;目的地，請檢閱下列關鍵點和必要的動作：
>
>* 所有使用者必須&#x200B;**停止使用Marketo Engage人員同步處理目的地**，並在2025年10月前移轉至新的&#x200B;**[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)**&#x200B;目的地。
>* **現有的資料流將不會自動移轉。**&#x200B;您必須[設定與新](marketo-engage-connection.md#connect-to-the-destination)目的地的新連線&#x200B;**[!UICONTROL Marketo Engage]**，並在那裡啟用您的對象。


## 概觀 {#overview}

使用Marketo Engage Person Sync聯結器將個人受眾的更新串流至Marketo Engage例項中的對應記錄。

>[!IMPORTANT]
>
>[Marketo V2 Audience Sync Connector](/help/destinations/catalog/adobe/marketo-engage.md)不應在「建立」模式中與設定檔更新同步聯結器搭配使用

## 支援的身分和屬性 {#support-identities-and-attributes}

### 支援的身分 {#supported-identities}

| 目標身分 | 說明 |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 電子郵件 | 代表電子郵件地址的名稱空間。 這種型別的名稱空間通常與單一人員相關聯，因此可跨不同管道識別該人員。 |

{style="table-layout:auto"}

### 支援的屬性 {#supported-attributes}

您可以將屬性從Experience Platform對應至貴組織在Marketo中可存取的任何屬性。 在Marketo中，您可以使用[Describe API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_6)要求來擷取貴組織有權存取的屬性欄位。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
| -------------------- | :-------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 細分服務 | 是 | 透過Experience Platform [細分服務](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/segmentation/home)產生的對象。 |
| 所有其他受眾來源 | 是 | 此類別包含透過[!DNL Segmentation Service]產生的對象以外的所有對象來源。 閱讀[各種對象來源](/help/segmentation/ui/audience-portal.md#customize)。 部分範例包括： <ul><li> 自訂上傳對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform，</li><li> 相似受眾， </li><li> 同盟對象， </li><li> 其他Experience Platform應用程式中產生的對象，例如[!DNL Adobe Journey Optimizer]、 </li><li> 及更多內容。 </li></ul> |

{style="table-layout:auto"}

依受眾資料型別支援的受眾：

| 對象資料型別 | 支援 | 說明 | 使用案例 |
|--------------------|-----------|-------------|-----------|
| [人員對象](/help/segmentation/types/people-audiences.md) | 是 | 根據客戶設定檔，可讓您針對行銷活動的特定人群進行定位。 | 經常購買者、購物車放棄者 |
| [帳戶對象](/help/segmentation/types/account-audiences.md) | 無 | 針對帳戶型行銷策略，鎖定特定組織內的個人。 | B2B行銷 |
| [潛在客戶對象](/help/segmentation/types/prospect-audiences.md) | 無 | 將目標定位為尚未成為客戶但與目標受眾具有相同特性的個人。 | 使用第三方資料進行勘探 |
| [資料集匯出](/help/catalog/datasets/overview.md) | 無 | 儲存在[!DNL Adobe Experience Platform]資料湖中的結構化資料集合。 | 報告、資料科學工作流程 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-and-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
| ---------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 匯出頻率 | 串流 | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 設定目的地 {#set-up-destination}

>[!IMPORTANT]
>
>* 若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。

如果貴公司可存取多個組織，請務必在Marketo Engage和[!DNL Real-Time CDP]中使用相同的組織（您正在其中設定Marketo的目的地聯結器）。  如果您已設定目的地，您可以選取要搭配新設定使用的現有Marketo帳戶。  如果沒有，請按一下「連線至目的地」提示，設定所要目的地的名稱、說明和Marketo Munchkin ID。  您可以在管理員 — >Munchkin功能表中找到您的Marketo執行個體的Munchkin ID。

>[!IMPORTANT]
>
>設定目的地的使用者必須在Marketo執行個體和資料分割中擁有[編輯人員](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions#access-database)許可權。

![連線到目的地](../../assets/catalog/adobe/marketo-engage-person-sync/connect-to-destination.png)

* **[!UICONTROL Name]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL Description]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Munchkin ID]**： Munchkin ID是特定Marketo執行個體的唯一識別碼。
* **[!UICONTROL Partition]**： Marketo Engage中用於依業務關係區分潛在客戶記錄的概念
* **[!UICONTROL First searchable field]**：要取消重複的欄位。 欄位必須出現在輸入的每個潛在客戶記錄中。 預設為電子郵件
* **[!UICONTROL First searchable field]**：要進行重複資料刪除的次要欄位。 欄位必須出現在輸入的每個潛在客戶記錄中。 選填

選取執行個體後，您還需要選取要與組態整合的Lead Partition。 [潛在客戶分割](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/workspaces-and-person-partitions/understanding-workspaces-and-person-partitions)是Marketo Engage中的概念，用於依業務考量（例如品牌或銷售區域）來區分潛在客戶記錄。 如果您的Marketo訂閱沒有工作區與分割區功能，或是您的訂閱中尚未建立其他分割區，則只有預設分割區可用。 單一設定只能更新存在於其設定分割中的潛在客戶記錄。

>[!IMPORTANT]
>
>第一次將對象啟動到Marketo目的地後，在Marketo目的地啟動之前回填對象中已存在的設定檔可能需要&#x200B;*最多24小時*。 此後，每當設定檔新增至對象時，都會立即新增至Marketo。

### 重複資料刪除欄位 {#deduplication-fields}

將更新傳送至Marketo engage時，會根據選取的分割區及一或兩個使用者選取的欄位來選取記錄。 如果您的目的地設定了北美分割區，且電子郵件地址和公司名稱設定為重複資料刪除欄位，則所有三個欄位都必須相符，才能將變更套用至現有記錄。 例如：

* 目的地已設定北美分割區
* Experience Platform中電子郵件為<test@example.com>且公司名稱為Example Inc.的人員符合目的地對象
* 除非Marketo中的北美分割區已存在具有這些值的記錄，否則將會建立新的潛在客戶記錄

如果找不到相符的潛在客戶記錄，則會建立新記錄。

![目的地詳細資料](../../assets/catalog/adobe/marketo-engage-person-sync/destination-details.png)

## 啟用對象 {#activate-audiences}

>[!IMPORTANT]
>
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

閱讀[啟用串流目的地的對象](/help/destinations/ui/activate-segment-streaming-destinations.md)，以取得啟用此目的地對象的指示。

在「啟用對象」步驟中，您將能夠選取您可見的任何個人對象。

![啟用對象](../../assets/catalog/adobe/marketo-engage-person-sync/activate-audiences.png)

## 欄位對應 {#field-mapping}

若要將特定人員屬性的變更傳送至Marketo Engage，該欄位必須從[!DNL Real-Time CDP]欄位對應至Marketo欄位。

![欄位對應](../../assets/catalog/adobe/marketo-engage-person-sync/field-mapping.png)

Experience Platform資料型別和Marketo資料型別可透過下列方式對應：

| Experience Platform資料型別 | Marketo資料型別 |
| ----------------------------- | ------------------------------------ |
| 字串 | 字串、文字區域、Url、電話、電子郵件 |
| 列舉 | 字串 |
| 日期 | 日期 |
| 日期-時間 | 日期時間 |
| 整數 | 整數 |
| 短整數 | 整數 |
| 長整數 | 浮點數 |
| 雙精度 | 貨幣，浮點數，% |
| 布林值 | 布林值 |
| 陣列 | 不支援 |
| 物件 | 不支援 |
| 地圖 | 不支援 |
| 位元組 | 不支援 |

{style="table-layout:auto"}

在某些情況下，最好允許整合功能設定欄位值（如果沒有欄位的話），同時防止整合功能更新已經有值的欄位。  如果您需要防止目的地聯結器覆寫Marketo Engage執行個體中的現有值，可以在Marketo執行個體的「管理員 — >欄位管理」區段中設定欄位以封鎖更新，並切換[!DNL Adobe Experience Platform]來源型別。

![封鎖欄位更新](../../assets/catalog/adobe/marketo-engage-person-sync/block-field-updates.png)

![封鎖欄位更新](../../assets/catalog/adobe/marketo-engage-person-sync/block-field-updates-2.png)

## 資料使用和管理 {#data-usage-and-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。
