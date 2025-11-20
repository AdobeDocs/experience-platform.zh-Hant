---
title: (API) Oracle Eloqua連線
description: (API) Oracle Eloqua目的地可讓您匯出帳戶資料，並在Oracle Eloqua中根據您的業務需求加以啟用。
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 4%

---


# [!DNL (API) Oracle Eloqua] 連線

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 它讓行銷人員能夠規劃並執行活動，同時為潛在客戶提供個人化的顧客體驗。 透過整合的潛在客戶管理與簡易的活動創建，它幫助行銷人員在買家旅程中於正確時間吸引正確的受眾，並優雅地擴展至電子郵件、展示搜尋、影片及行動裝置等管道中觸及受眾。 銷售團隊能以更快速度完成更多交易，透過即時洞察提升行銷投資報酬率。

此[!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md)利用[ REST API中的](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html)更新連絡人[!DNL Oracle Eloqua]作業，可讓您&#x200B;**將對象內的身分識別**&#x200B;更新為[!DNL Oracle Eloqua]。

[!DNL Oracle Eloqua]使用[基本驗證](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html)與[!DNL Oracle Eloqua] REST API通訊。 [!DNL Oracle Eloqua]向目的地驗證[區段中進一步說明如何向您的](#authenticate)執行個體進行驗證。

## 使用案例 {#use-cases}

線上平台的行銷部門想要將電子郵件行銷活動廣播給已組織的潛在客戶受眾。 平台的行銷團隊可以透過Adobe Experience Platform更新現有的潛在客戶資訊、從自己的離線資料建立對象，並將這些對象傳送至[!DNL Oracle Eloqua]，接著便可以用這些對象來傳送行銷活動電子郵件。

## 先決條件 {#prerequisites}

### Experience Platform必要條件 {#prerequisites-in-experience-platform}

在啟用資料到[!DNL Oracle Eloqua]目的地之前，您必須在[中建立](/help/xdm/schema/composition.md)結構描述[、](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)資料集[和](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)區段[!DNL Experience Platform]。

如果您需要對象狀態的指引，請參閱[對象成員資格詳細資料結構描述欄位群組](/help/xdm/field-groups/profile/segmentation.md)的Experience Platform檔案。

### [!DNL Oracle Eloqua]必要條件 {#prerequisites-destination}

若要將資料從Experience Platform匯出至您的[!DNL Oracle Eloqua]帳戶，您需要有[!DNL Oracle Eloqua]帳戶。

此外，你至少需要為你的&#x200B;*實例取得*「進階使用者 - 行銷權限」。[!DNL Oracle Eloqua]請參閱&#x200B;*安全使用者存取*&#x200B;頁面的[「安全群組」](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm)區塊以獲得指引。存取權限是目的地在呼叫 [ API 時](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html)，程式化決定你的基礎網址[!DNL Oracle Eloqua]所必需的。

#### 收集[!DNL Oracle Eloqua]認證 {#gather-credentials}

在驗證[!DNL Oracle Eloqua]目的地之前，請記下以下專案：

| 認證 | 說明 |
| --- | --- |
| `Company Name` | 與您的[!DNL Oracle Eloqua]帳戶相關聯的公司名稱。 <br>之後你會將 和 `Company Name` [!DNL Oracle Eloqua] `Username` 作為串接字串，作為驗證目的地&#x200B;**[!UICONTROL Username]**&#x200B;時使用的 。[ ](#authenticate) |
| `Username` | 你 [!DNL Oracle Eloqua] 帳號的使用者名稱。 |
| `Password` | 你 [!DNL Oracle Eloqua] 帳號的密碼。 |
| `Pod` | [!DNL Oracle Eloqua] 支援多個資料中心，每個中心擁有獨特的網域名稱。 [!DNL Oracle Eloqua] 這些稱為「艙」，目前共有七個——P01、P02、P03、P04、P06、P07和P08。 要知道你使用的 POD，請 [!DNL Oracle Eloqua] 在成功登入後，在瀏覽器中記錄網址。 例如，如果瀏覽器URL為`secure.p01.eloqua.com`，則`pod`為`p01`。 如需其他指南，請參閱[決定您的POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua)頁面。 |

如需指引，請參閱[登入 [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing)。

## 護欄 {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua]自訂連絡人欄位是使用在&#x200B;**[!UICONTROL Select segments]**&#x200B;步驟期間選取的對象名稱自動建立。

* [!DNL Oracle Eloqua]的最大限製為250個自訂連絡人欄位。
* 在匯出新對象之前，請確保[!DNL Oracle Eloqua]內的Experience Platform對象數量和現有對象數量不超過此限制。
* 若超過此限制，體驗平台會出現錯誤。 這是因為 [!DNL Oracle Eloqua] API 未能驗證請求，並回應 - *400：有驗證錯誤* - 錯誤訊息描述問題。
* 如果你已經達到上述限制，你需要先從目的地移除現有的映射，並刪除帳戶中相應的自訂聯絡欄位 [!DNL Oracle Eloqua] ，才能匯出更多分段。

* 請參閱[[!DNL Oracle Eloqua] 建立連絡人欄位](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm)頁面，瞭解其他限制的相關資訊。

## 支援的身分 {#supported-identities}

[!DNL Oracle Eloqua] 支援下表中描述的身份更新。 了解更多關於 [身份的](/help/identity-service/features/namespaces.md)資訊。

| 目標身份 | 說明 | 命令的 |
|---|---|---|
| `EloquaId` | 聯絡人的唯一識別碼。 | 是 |

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL Profile-based]** | <ul><li>您正在匯出區段的所有成員，以及所需的結構描述欄位&#x200B;*（例如：電子郵件地址、電話號碼、姓氏）* （根據您的欄位對應）。</li><li> 針對Experience Platform中每個選取的對象，相對應的[!DNL Oracle Eloqua]區段狀態會從Experience Platform更新其對象狀態。</li></ul> |
| 匯出頻率 | **[!UICONTROL Streaming]** | <ul><li>串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 閱讀更多關於串流平台的[資訊](/help/destinations/destination-types.md#streaming-destinations)。</li></ul> |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>要連接目的地，你需要取得&#x200B;**[!UICONTROL View Destinations]**&#x200B;存取&#x200B;**[!UICONTROL Manage Destinations]**[&#x200B;控制權限](/help/access-control/home.md#permissions)。請閱讀 [存取控制概述](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需權限。

要連接此目的地，請依照目的地設定教學[中的](../../ui/connect-destination.md)步驟操作。在設定目的地工作流程中，請填寫下方兩個章節列出的欄位。

在 **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** 搜尋 [!DNL (API) Oracle Eloqua]。 或者，您可以在&#x200B;**[!UICONTROL Email Marketing]**&#x200B;類別下找到它。

### 驗證目標 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="公司名稱\使用者名稱"
>abstract="在此欄位中填寫 `{COMPANY_NAME}\{USERNAME}` 表單中來自 Oracle Eloqua 的公司名稱和使用者名稱"

請填寫下方必填欄位。 請參閱 [「蒐集 [!DNL Oracle Eloqua] 憑證](#gather-credentials) 」章節以獲得相關指引。

* **[!UICONTROL Password]**：您[!DNL Oracle Eloqua]帳戶的密碼。
* **[!UICONTROL Username]**：由您的[!DNL Oracle Eloqua]公司名稱和[!DNL Oracle Eloqua]使用者名稱組成的串連字串。<br>串連值採用`{COMPANY_NAME}\{USERNAME}`的形式。<br>注意，請勿使用任何大括弧或空格並保留`\`。 <br>例如，若您的[!DNL Oracle Eloqua]公司名稱是`MyCompany`，[!DNL Oracle Eloqua]使用者名稱是`Username`，則您將在&#x200B;**[!UICONTROL Username]**&#x200B;欄位中使用的串連值為`MyCompany\Username`。

若要驗證到目的地，請選取&#x200B;**[!UICONTROL Connect to destination]**。
![Experience Platform UI熒幕擷圖顯示如何驗證。](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

如果提供的詳細資料有效，UI會顯示帶有綠色勾號的&#x200B;**[!UICONTROL Connected]**&#x200B;狀態。 然後您可以繼續下一步驟。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="若要尋找您的 Pod 編號，請登入 Oracle Eloqua。成功登入後，記下瀏覽器中的 URL。 "

<!-- >additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle Knowledge base - find out your Pod number" -->

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。
![Experience Platform UI 截圖顯示目的地細節。](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Name]**：一個你未來會認出這個目的地的名字。
* **[!UICONTROL Description]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Pod]**：若要取得您所在的`pod`，請登入[!DNL Oracle Eloqua]，並在您成功登入後，在瀏覽器中記下該URL。 例如，如果您的瀏覽器URL為`secure.p01.eloqua.com`，則需要選取的`pod`值為`p01`。 如需其他指南，請參閱[收集 [!DNL Oracle Eloqua] 認證](#gather-credentials)區段。

### 啟用警示 {#enable-alerts}

你可以啟用警示，接收資料流狀態通知到目的地。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將對象資料從Adobe Experience Platform正確傳送至[!DNL Oracle Eloqua]目的地，您必須完成欄位對應步驟。 映射是指在你的體驗平台帳號中，建立經驗資料模型（XDM）架構欄位與其對應的目標目的地對應欄位之間的連結。

要將 XDM 欄位對應到 [!DNL Oracle Eloqua] 目的地欄位，請依照以下步驟操作：

1. 在&#x200B;**[!UICONTROL Mapping]**&#x200B;步驟中，選取&#x200B;**[!UICONTROL Add new mapping]**。 您會在畫面上看到新的對應列。
1. 在&#x200B;**[!UICONTROL Select source field]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL Select attributes]**&#x200B;類別並選取XDM屬性，或選擇&#x200B;**[!UICONTROL Select identity namespace]**&#x200B;並選取身分。
1. 在&#x200B;**[!UICONTROL Select target field]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL Select identity namespace]**&#x200B;並選取身分，或選擇&#x200B;**[!UICONTROL Select custom attributes]**&#x200B;並在&#x200B;**[!UICONTROL Attribute name]**&#x200B;欄位中輸入所需的屬性名稱。 您提供的屬性名稱應符合[!DNL Oracle Eloqua]中現有的連絡人屬性。 請參考 [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) 你可以在 中使用的 [!DNL Oracle Eloqua]精確屬性名稱。

   * 重複這些步驟，加入所需的及任何屬性映射，連接你的 XDM 設定檔結構與 [!DNL Oracle Eloqua]：

     | 來源欄位 | 目標欄位 | 命令的 |
     |---|---|---|
     | `IdentityMap: Eid` | `Identity: EloquaId` | 是 |
     | `xdm: personalEmail.address` | `Attribute: emailAddress` | 是 |
     | `xdm: personName.firstName` | `Attribute: firstName` | |
     | `xdm: personName.lastName` | `Attribute: lastName` | |
     | `xdm: workAddress.street1` | `Attribute: address1` | |
     | `xdm: workAddress.street2` | `Attribute: address2` | |
     | `xdm: workAddress.street3` | `Attribute: address3` | |
     | `xdm: workAddress.postalCode` | `Attribute: postalCode` | |
     | `xdm: workAddress.country` | `Attribute: country` | |
     | `xdm: workAddress.city` | `Attribute: city` | |

   * 具有上述對應的範例如下所示：
     ![具有屬性對應的Experience Platform UI熒幕擷圖範例。](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* 在&#x200B;**[!UICONTROL Target field]**&#x200B;中指定的屬性應該與[[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html)中指定的屬性完全相同，因為這些屬性會形成要求內文。
>* **[!UICONTROL Source field]**&#x200B;中指定的屬性未遵循任何此類限制。 您可以視需要加以對應，但如果資料格式在推送至[!DNL Oracle Eloqua]時不正確，則會導致錯誤。 例如，您可以對應&#x200B;**[!UICONTROL Source field]**&#x200B;身分名稱空間`contact key`、`ABC ID`等。 至&#x200B;**[!UICONTROL Target field]** ：在確認ID值符合`EloquaId`接受的格式之後[!DNL Oracle Eloqua]。
>* `EloquaID`對應是更新與識別相對應的屬性的必要專案。
>* 需要`emailAddress`對應。 若未包含API，API會擲回錯誤，如下所示：
>
>```json
>{
>     "type":"ObjectValidationError",
>     "container":{
>           "type":"ObjectKey",
>           "objectType":"Contact"
>     },
>     "property":"emailAddress",
>     "requirement":{
>           "type":"EmailAddressRequirement"
>     },
>     "value":"<null>"
>}
>```

當您完成提供目的地連線的對應時，請選取&#x200B;**[!UICONTROL Next]**。

>[!NOTE]
>
>傳送連絡人欄位資訊給[!DNL Oracle Eloqua]時，目的地會在每次執行時，自動將唯一的識別碼尾碼加到選取的對象名稱。 這樣可以確保與受眾名稱對應的聯絡欄位名稱不會重疊。 請參考 [「驗證資料匯出](#exported-data) 」部分截圖範例，該 [!DNL Oracle Eloqua] 頁面包含使用受眾名稱建立的自訂聯絡欄位。

## 驗證資料匯出 {#exported-data}

為了確認你已正確設定目的地，請遵循以下步驟：

1. 選擇 **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** 並導航到目的地清單。
1. 接著，選擇目的地並切換到 **[!UICONTROL Activation data]** 分頁，然後選擇受眾名稱。
   ![顯示目的地啟用資料的Experience Platform UI熒幕擷圖範例。](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. 監控對象摘要，並確保設定檔計數與區段中的計數相對應。
   ![Experience Platform UI熒幕擷圖範例，顯示區段。](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. [!DNL Oracle Eloqua]登入網站，然後前往&#x200B;**[!UICONTROL Contacts Overview]**&#x200B;頁面查看是否有新增受眾的個人檔案。要查看受眾狀態，請 **[!UICONTROL Contact Detail]** 深入頁面，檢查已建立以所選受眾名稱為前綴的聯絡欄位。

![Oracle Eloqua UI 截圖顯示「聯絡詳情」頁面，並以受眾名稱自訂建立聯絡欄位。](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。

## 錯誤與疑難排解 {#errors-and-troubleshooting}

建立目的地時，您可能會收到下列其中一個錯誤訊息： `400: There was a validation error`或`400 BAD_REQUEST`。 如[護欄](#guardrails)區段所述，當您超過250個自訂連絡人欄位限制時，就會發生這種情況。 若要修正此錯誤，請確定您在[!DNL Oracle Eloqua]中未超過自訂連絡人欄位限制。
![Experience Platform UI熒幕擷圖顯示錯誤。](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

請參閱[[!DNL Oracle Eloqua] HTTP狀態碼](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html)和[[!DNL Oracle Eloqua] 驗證錯誤](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html)頁面，以取得包含說明的狀態和錯誤碼的完整清單。

## 其他資源 {#additional-resources}

更多細節請參閱文件：[!DNL Oracle Eloqua]

* [Oracle Eloqua 行銷自動化](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [REST API for Oracle Eloqua Marketing Cloud Service](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### 更新日誌

本節擷取此目的地聯結器的功能和重要檔案更新。

+++ 檢視變更記錄檔

| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2023 年 4 月 | 文件更新 | <ul><li>我們已更新[使用案例](#use-cases)區段，針對客戶何時可受益於使用此目的地提供更清楚的範例。</li> <li>我們已更新[對應](#mapping-considerations-example)區段，其中包含強制和選用對應的明確範例。</li> <li>我們已更新[連線至目的地](#connect)區段，並提供如何使用&#x200B;**[!UICONTROL Username]**&#x200B;公司名稱和[!DNL Oracle Eloqua]使用者名稱來建構[!DNL Oracle Eloqua]欄位的串連值的範例。 (PLATIR-28343)</li><li>我們已更新[收集 [!DNL Oracle Eloqua] 認證](#gather-credentials)及[填寫目的地詳細資料](#destination-details)區段，其中包含有關[!DNL Oracle Eloqua] **[!UICONTROL Pod]**&#x200B;選擇的指引。 目的地使用&#x200B;*&quot;Pod&quot;*&#x200B;值來建構API呼叫的基本URL。 [[!DNL Oracle Eloqua] 必要條件](#prerequisites-destination)區段也已更新，其中包含指派&#x200B;*「進階使用者 — 行銷許可權」*&#x200B;為您&#x200B;*執行個體的必要*「安全性群組」[!DNL Oracle Eloqua]的指引。</li></ul> |
| 2023 年 3 月 | 首次發行 | 初始目的地版本和檔案發佈。 |

{style="table-layout:auto"}

+++
