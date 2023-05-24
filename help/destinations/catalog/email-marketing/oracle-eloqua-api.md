---
title: (API)OracleEloqua連接
description: (API)OracleEloca目標允許您導出帳戶資料並在OracleEloca中激活它，以滿足您的業務需要。
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: 3d54b89ab5f956710ad595a0e8d3567e1e773d0a
workflow-type: tm+mt
source-wordcount: '2125'
ht-degree: 3%

---


# [!DNL (API) Oracle Eloqua] 連接

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 使營銷商能夠計畫和執行市場活動，同時為潛在客戶提供個性化的客戶體驗。 通過整合的銷售線索管理和輕鬆的促銷活動建立，它可以幫助營銷人員在購買者旅途中的適當時間與適當的受眾接觸，並優雅地擴展，以跨電子郵件、顯示搜索、視頻和移動等渠道訪問受眾。 銷售團隊可以更快速地完成更多交易，通過即時洞察提高營銷ROI。

此 [!DNL Adobe Experience Platform] [目標](/help/destinations/home.md) 利用 [更新聯繫人](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) 操作 [!DNL Oracle Eloqua] REST API，它允許您 **更新身份** 段至 [!DNL Oracle Eloqua]。

[!DNL Oracle Eloqua] 使用 [基本身份驗證](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) 與 [!DNL Oracle Eloqua] REST API。 驗證到您 [!DNL Oracle Eloqua] 下面是實例， [驗證到目標](#authenticate) 的子菜單。

## 使用案例 {#use-cases}

一個線上平台的營銷部門希望向策劃的銷售線索受眾廣播基於電子郵件的營銷活動。 該平台的營銷團隊可以通過Adobe Experience Platform更新現有的銷售線索資訊，從自己的離線資料構建資料段，並將這些資料段發送到 [!DNL Oracle Eloqua]，然後可用於發送營銷活動電子郵件。

## 先決條件 {#prerequisites}

### Experience Platform先決條件 {#prerequisites-in-experience-platform}

在將資料激活到 [!DNL Oracle Eloqua] 目標，您必須 [架構](/help/xdm/schema/composition.md)的 [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), [段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立 [!DNL Experience Platform]。

請參閱Experience Platform文檔，瞭解 [段成員身份詳細資訊架構欄位組](/help/xdm/field-groups/profile/segmentation.md) 如果需要有關段狀態的指導。

### [!DNL Oracle Eloqua] 先決條件 {#prerequisites-destination}

為了將資料從平台導出到 [!DNL Oracle Eloqua] 你需要的帳戶 [!DNL Oracle Eloqua] 帳戶。

此外，您至少需要 *&quot;高級用戶 — 市場營銷權限&quot;* 為 [!DNL Oracle Eloqua] 實例。 請參閱 *&quot;安全組&quot;* 的 [安全的用戶訪問](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) 的子菜單。 目標需要以寫程式方式訪問 [確定基URL](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) 調用 [!DNL Oracle Eloqua] API。

#### 收集 [!DNL Oracle Eloqua] 憑據 {#gather-credentials}

在驗證到 [!DNL Oracle Eloqua] 目標：

| 憑據 | 說明 |
| --- | --- |
| `Company Name` | 與您的 [!DNL Oracle Eloqua] 帳戶。 <br>您稍後將使用 `Company Name` 和 [!DNL Oracle Eloqua] `Username` 作為要用作 **[!UICONTROL 用戶名]** 何時 [向目的地驗證](#authenticate)。 |
| `Username` | 您的用戶名 [!DNL Oracle Eloqua] 帳戶。 |
| `Password` | 您的密碼 [!DNL Oracle Eloqua] 帳戶。 |
| `Pod` | [!DNL Oracle Eloqua] 支援多個資料中心，每個資料中心都具有唯一的域名。 [!DNL Oracle Eloqua] 將這些稱為&quot;莢果&quot;，目前總共有7個 — p01、p02、p03、p04、p06、p07和p08。 要獲取您所在的POD，請登錄 [!DNL Oracle Eloqua] 並在成功登錄後在瀏覽器中記錄URL。 例如，如果瀏覽器URL為 `secure.p01.eloqua.com` 你 `pod` 是 `p01`。 請參閱 [確定POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) 的子菜單。 |

請參閱 [登錄到 [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) 的上界。

## 護欄 {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] 自定義聯繫人欄位是使用在 **[!UICONTROL 選擇段]** 的子菜單。


* [!DNL Oracle Eloqua] 最多限制為250個自定義聯繫欄位。
* 在導出新段之前，請確保平台段的數量和 [!DNL Oracle Eloqua] 不要超過此限制。
* 如果超出此限制，您將在Experience Platform中遇到錯誤。 這是因為 [!DNL Oracle Eloqua] API無法驗證請求，並以 —  *400:驗證錯誤*  — 描述問題的錯誤消息。
* 如果已達到上面指定的限制，則需要從目標中刪除現有映射並刪除目標中相應的自定義聯繫人欄位 [!DNL Oracle Eloqua] 帳戶，然後才能導出更多段。

* 請參閱 [[!DNL Oracle Eloqua] 建立聯繫人欄位](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) 的子菜單。

## 支援的身份 {#supported-identities}

[!DNL Oracle Eloqua] 支援更新下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 必要 |
|---|---|---|
| `EloquaId` | 聯繫人的唯一標識符。 | 是 |

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | <ul><li>您正在導出段的所有成員以及所需的架構欄位 *(例如：電子郵件地址、電話號碼、姓氏)*，根據您的欄位映射。</li><li> 對於平台中的每個選定段， [!DNL Oracle Eloqua] 段狀態將從平台更新為其段狀態。</li></ul> |
| 導出頻率 | **[!UICONTROL 流]** | <ul><li>流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。</li></ul> |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

在 **[!UICONTROL 目標]** > **[!UICONTROL 目錄]** 搜索 [!DNL (API) Oracle Eloqua]。 或者，可將其定位在 **[!UICONTROL 電子郵件營銷]** 的子菜單。

### 驗證到目標 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="公司名稱\使用者名稱"
>abstract="在此欄位中填寫 `{COMPANY_NAME}\{USERNAME}` 表單中來自 Oracle Eloqua 的公司名稱和使用者名稱"

填寫下面的必填欄位。 請參閱 [收集 [!DNL Oracle Eloqua] 憑據](#gather-credentials) 的雙曲餘切值。
* **[!UICONTROL 密碼]**:您的密碼 [!DNL Oracle Eloqua] 帳戶。
* **[!UICONTROL 用戶名]**:由您的 [!DNL Oracle Eloqua] 公司名稱和 [!DNL Oracle Eloqua] 用戶名。<br>級連值的形式為 `{COMPANY_NAME}\{USERNAME}`。<br> 注意，不要使用任何大括弧或空格並保留 `\`。 <br>例如，如果 [!DNL Oracle Eloqua] 公司名稱為 `MyCompany` 和 [!DNL Oracle Eloqua] 用戶名為 `Username`，將在 **[!UICONTROL 用戶名]** 欄位 `MyCompany\Username`。

要驗證到目標，請選擇 **[!UICONTROL 連接到目標]**。
![平台UI螢幕快照，顯示如何進行身份驗證。](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

如果提供的詳細資訊有效，UI將顯示 **[!UICONTROL 已連接]** 狀態為綠色複選標籤。 然後，可以繼續下一步。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="若要尋找您的 Pod 編號，請登入 Oracle Eloqua。成功登入後，記下瀏覽器中的 URL。 "
>additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle 知識庫 - 找出您的 Pod 編號"

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。
![顯示目標詳細資訊的平台UI螢幕快照。](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 莢]**:要獲得 `pod` 您正在登錄，登錄 [!DNL Oracle Eloqua] 並在成功登錄後在瀏覽器中記錄URL。 例如，如果瀏覽器URL為 `secure.p01.eloqua.com` 這樣 `pod` 需要選擇的值是 `p01`。 請參閱 [收集 [!DNL Oracle Eloqua] 憑據](#gather-credentials) 的下界。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
>
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

### 映射注意事項和示例 {#mapping-considerations-example}

正確將您的受眾資料從Adobe Experience Platform發送到 [!DNL Oracle Eloqua] 目標，您需要完成欄位映射步驟。 映射包括在您的平台帳戶中的「體驗資料模型」(XDM)架構欄位與目標目標中對應的欄位之間建立連結。

將XDM欄位映射到 [!DNL Oracle Eloqua] 目標欄位，請執行以下步驟：

1. 在 **[!UICONTROL 映射]** 步驟，選擇 **[!UICONTROL 添加新映射]**。 螢幕上將顯示新的映射行。
1. 在 **[!UICONTROL 選擇源欄位]** ，選擇 **[!UICONTROL 選擇屬性]** 類別，然後選擇XDM屬性或 **[!UICONTROL 選擇標識命名空間]** 並選擇標識。
1. 在 **[!UICONTROL 選擇目標欄位]** 窗口，選擇 **[!UICONTROL 選擇標識命名空間]** 選擇標識，或 **[!UICONTROL 選擇自定義屬性]** 並在 **[!UICONTROL 屬性名稱]** 的子菜單。 您提供的屬性名稱應與中的現有聯繫人屬性匹配 [!DNL Oracle Eloqua]。 請參閱 [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) 用於的準確屬性名 [!DNL Oracle Eloqua]。
   * 重複這些步驟，在XDM配置檔案架構和 [!DNL Oracle Eloqua]: |源欄位 |目標欄位 |強制 | |—|—| |`IdentityMap: Eid`|`Identity: EloquaId`|是 | |`xdm: personalEmail.address`|`Attribute: emailAddress`|是 | |`xdm: personName.firstName`|`Attribute: firstName`| | |`xdm: personName.lastName`|`Attribute: lastName`| | |`xdm: workAddress.street1`|`Attribute: address1`| | |`xdm: workAddress.street2`|`Attribute: address2`| | |`xdm: workAddress.street3`|`Attribute: address3`| | |`xdm: workAddress.postalCode`|`Attribute: postalCode`| | |`xdm: workAddress.country`|`Attribute: country`| | |`xdm: workAddress.city`|`Attribute: city`| |

   * 下面顯示了具有上述映射的示例：
      ![平台UI螢幕快照示例，包含屬性映射。](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* 在 **[!UICONTROL 目標欄位]** 應與中指定的名稱完全相同 [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) 因為這些屬性將形成請求正文。
>* 在 **[!UICONTROL 源欄位]** 不要遵守任何此類限制。 您可以根據需要對其進行映射，但是，如果資料格式在推入到 [!DNL Oracle Eloqua] 會導致錯誤。 例如，可以映射 **[!UICONTROL 源欄位]** 標識命名空間 `contact key`。 `ABC ID` 等。 至 **[!UICONTROL 目標欄位]** : `EloquaId` 確保ID值與接受的格式匹配後 [!DNL Oracle Eloqua]。
>* 的 `EloquaID` 必須進行映射才能更新與標識對應的屬性。
>* 的 `emailAddress` 需要映射。 如果沒有它，API將引發以下錯誤：
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

完成為目標連接提供映射後，選擇 **[!UICONTROL 下一個]**。

>[!NOTE]
>
>當將聯繫人欄位資訊發送到 [!DNL Oracle Eloqua]。 這可確保與段名稱對應的聯繫人欄位名稱不重疊。 請參閱 [驗證資料導出](#exported-data) 節截圖示例 [!DNL Oracle Eloqua] 「聯繫人詳細資訊」頁，其中包含使用段名稱建立的自定義聯繫人欄位。

## 驗證資料導出 {#exported-data}

要驗證您是否正確設定了目標，請執行以下步驟：

1. 選擇 **[!UICONTROL 目標]** > **[!UICONTROL 瀏覽]** 導航到目標清單。
1. 接下來，選擇目標並切換到 **[!UICONTROL 激活資料]** ，然後選擇段名稱。
   ![平台UI螢幕快照示例，顯示目標激活資料。](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. 監視段摘要並確保配置檔案的計數與段內的計數相對應。
   ![平台UI螢幕抓圖示例顯示「段」。](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. 登錄到 [!DNL Oracle Eloqua] ，然後導航到 **[!UICONTROL 聯繫人概述]** 的子菜單。 要查看段狀態，請追溯至 **[!UICONTROL 聯繫人詳細資訊]** 並檢查是否已建立以選定段名稱為前置詞的聯繫人欄位。

![OracleEloqua UI螢幕快照，顯示「聯繫人詳細資訊」頁，其中包含使用段名稱建立的自定義聯繫人欄位。](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。

## 錯誤和故障排除 {#errors-and-troubleshooting}

建立目標時，可能會收到以下錯誤消息之一： `400: There was a validation error` 或 `400 BAD_REQUEST`。 如果超過250個自定義聯繫欄位限制，則會發生這種情況，如 [護欄](#guardrails) 的子菜單。 要修復此錯誤，請確保您未超過中的自定義聯繫人欄位限制 [!DNL Oracle Eloqua]。
![顯示錯誤的平台UI螢幕快照。](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

請參閱 [[!DNL Oracle Eloqua] HTTP狀態代碼](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) 和 [[!DNL Oracle Eloqua] 驗證錯誤](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) 頁面，列出狀態和錯誤代碼及說明。

## 其他資源 {#additional-resources}

有關其他詳細資訊，請參閱 [!DNL Oracle Eloqua] 文檔：

* [OracleEloqua營銷自動化](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [用於OracleEloquaMarketing Cloud服務的REST API](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### 更改日誌

本節將捕獲對此目標連接器進行的功能和重要文檔更新。

+++ 查看更改日誌

| 發放月 | 更新類型 | 說明 |
|---|---|---|
| 2023 年 4 月 | 文檔更新 | <ul><li>我們更新了 [用例](#use-cases) 部分中提供了一個更清晰的示例，說明客戶何時可以從使用此目標中獲益。</li> <li>我們更新了 [映射](#mapping-considerations-example) 部分，其中包含強制映射和可選映射的明確示例。</li> <li>我們更新了 [連接到目標](#connect) 節中關於如何為 **[!UICONTROL 用戶名]** 欄位 [!DNL Oracle Eloqua] 公司名稱和 [!DNL Oracle Eloqua] 用戶名。 (PLATIR-28343)</li><li>我們更新了 [收集 [!DNL Oracle Eloqua] 憑據](#gather-credentials) 和 [填寫目標詳細資訊](#destination-details) 帶有指導的部分 [!DNL Oracle Eloqua] **[!UICONTROL 莢]** 的子菜單。 的 *&quot;Pod&quot;* 目標使用值來構造API調用的基URL。 的 [[!DNL Oracle Eloqua] 先決條件](#prerequisites-destination) 部分還更新了有關分配的指導 *&quot;高級用戶 — 市場營銷權限&quot;* 按要求 *&quot;安全組&quot;* 為 [!DNL Oracle Eloqua] 實例。</li></ul> |
| 2023 年 3 月 | 首次發行 | 初始目標版本和文檔發佈。 |

{style="table-layout:auto"}

+++