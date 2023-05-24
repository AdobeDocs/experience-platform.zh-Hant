---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 同意處理在Adobe Experience Platform
description: 瞭解如何使用Adobe2.0標準在Adobe Experience Platform處理客戶同意信號。
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---

# Adobe Experience Platform的同意處理

Adobe Experience Platform允許您處理從客戶收集的同意資料並將其整合到儲存的客戶配置檔案中。 然後，下游流程可以使用此資料來確定是否針對特定客戶收集資料，或者其配置檔案是否用於特定目的。 例如，特定配置檔案的同意資料可以確定它是否可以包括在導出的受眾段中，或者它是否可以參與特定的營銷渠道，如電子郵件、文本消息或推送通知。

本文檔概述了如何配置平台資料操作以接收由同意管理平台(CMP)生成的客戶同意資料，並將這些資料整合到客戶配置檔案中以用於下游使用案例。

>[!NOTE]
>
>本文檔重點介紹使用Adobe標準處理同意資料。 如果您是按照IAB透明度和同意框架(TCF)2.0處理同意資料，請參閱上面的指南 [TCF 2.0支援Adobe Real-time Customer Data Platform](../iab/overview.md)。

## 先決條件

本指南要求對處理同意資料所涉及的各種Experience Platform服務進行工作理解：

* [體驗資料模型(XDM)](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
* [Adobe Experience Platform身份服務](../../../../identity-service/home.md):通過跨設備和系統橋接身份，解決客戶體驗資料碎片化帶來的根本難題。
* [即時客戶配置檔案](../../../../profile/home.md):使用 [!DNL Identity Service] 能夠從您的資料集中即時建立詳細的客戶配置檔案。 即時客戶配置檔案從資料湖中提取資料，並將客戶配置檔案保留在其自己的單獨資料儲存中。
* [Adobe Experience PlatformWeb SDK](../../../../edge/home.md):客戶端JavaScript庫，允許您將各種平台服務整合到面向客戶的網站中。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md):本指南中所示的與同意相關的SDK命令的用例概述。
* [Adobe Experience Platform分段服務](../../../../segmentation/home.md):允許您將即時客戶概要資訊資料分成具有相似特性且響應類似市場營銷策略的一組個人。

## 同意處理流程摘要 {#summary}

下面介紹了在正確配置系統後如何處理同意資料：

1. 客戶通過您網站上的對話框為資料收集提供其同意首選項。
1. 在每個頁面載入（或當CMP檢測到同意首選項的更改時），站點上的自定義指令碼會將當前首選項映射到標準XDM對象。 然後，此對象將傳遞給平台Web SDK `setConsent` 的子菜單。
1. 當 `setConsent` 稱為「平台Web SDK」，它檢查許可值是否與上次接收的許可值不同。 如果這些值不同（或沒有以前的值），則將結構化同意/偏好資料發送到Adobe Experience Platform。
1. 將同意/偏好資料攝入到 [!DNL Profile]-enabled資料集，其架構包含同意/首選項欄位。

除了由CMP同意更改掛接觸發的SDK命令外，同意資料還可以通過任何由客戶生成的XDM資料流入Experience Platform，這些資料直接上傳到 [!DNL Profile]-enabled dataset。

### 同意執行

在當前版本的同意處理支援平台中，只有資料收集權限(`collect.val`)由平台Web SDK自動強制執行。 雖然可以收集更精細的同意和首選項並將其保留在客戶配置檔案中，但必須在您自己的下游流程中手動強制執行這些附加信號。

>[!NOTE]
>
>有關上述XDM同意欄位結構的詳細資訊，請參閱 [[!UICONTROL 同意和首選項] 資料類型](../../../../xdm/data-types/consents.md)。

系統配置完畢後，平台Web SDK將解釋當前用戶的資料收集同意值，以確定資料應該發送到Adobe Experience Platform邊緣網路、從客戶端刪除還是保留，直到資料收集權限設定為是或否。

## 確定如何在CMP中生成客戶同意資料 {#consent-data}

由於每個CMP系統都是唯一的，因此您必須確定允許客戶在與您的服務交互時提供同意的最佳方式。 實現此目的的常見方法是使用Cookie同意對話框，類似於以下示例：

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

此對話框應允許客戶選擇加入或退出針對其資料的特定市場營銷和個性化使用案例。 這些同意和首選項應符合您為 [!DNL Profile]-enabled dataset在下一步中。

## 將標準化同意欄位添加到 [!DNL Profile]已啟用的資料集 {#dataset}

必須將客戶同意資料發送到 [!DNL Profile]-enabled資料集，其架構包含同意欄位。 這些欄位必須包含在用於捕獲有關單個客戶的屬性資訊的相同架構和資料集中。

請參閱上的教程 [配置用於捕獲同意資料的資料集](./dataset.md) 有關如何將這些必填欄位添加到 [!DNL Profile]在繼續使用本指南之前，啟用資料集。

## 更新 [!DNL Profile] 合併策略包括同意資料 {#merge-policies}

建立 [!DNL Profile]-enabled dataset用於處理同意資料，您必須確保您的合併策略已配置為始終在每個客戶配置檔案中包含同意欄位。 這涉及設定資料集優先順序，以便您的同意資料集優先順序高於其他可能衝突的資料集。

>[!NOTE]
>
>如果沒有任何衝突的資料集，則應為合併策略設定時間戳優先順序。 這有助於確保客戶指定的最新同意是使用的同意設定。

有關如何使用合併策略的詳細資訊，請首先閱讀 [合併策略概述](../../../../profile/merge-policies/overview.md)。 設定合併策略時，必須確保配置檔案包含由 [!UICONTROL 同意和首選項] 架構欄位組，如上的指南中所述 [資料集制備](./dataset.md)。

## 將同意資料引入平台

一旦您擁有了資料集並合併策略以表示客戶配置檔案中所需的同意欄位，下一步就是將同意資料本身納入平台。

主要是，您應該使用Adobe Experience PlatformWeb SDK在CMP檢測到同意更改事件時將同意資料發送到平台。 如果您正在移動平台上收集同意資料，則應使用Adobe Experience Platform移動軟體開發工具包。 您也可以選擇直接接收收集的同意資料，方法是將其映射到同意資料集的XDM架構，然後通過批處理接收將其發送到平台。

以下各小節提供了每種方法的詳細資訊。

### 配置Experience PlatformWeb SDK以處理同意資料 {#web-sdk}

一旦將CMP配置為偵聽網站上的同意更改事件，您就可以整合Experience PlatformWeb SDK以接收更新的同意設定，並在每頁載入時以及每當發生同意更改事件時將其發送到平台。 請參閱上的指南 [配置Web SDK以處理客戶同意資料](../sdk.md) 的子菜單。

### 配置Experience Platform移動SDK以處理同意資料 {#mobile-sdk}

如果您的移動應用程式需要客戶同意首選項，則可以整合Experience Platform移動SDK以檢索和更新同意設定，並在調用同意API時將其發送到平台。

請參閱Mobile SDK文檔 [配置「同意」移動擴展](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network) 和 [使用Conness API](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network/api-reference)。 有關如何使用移動SDK處理隱私問題的詳細資訊，請參閱一節 [隱私和GDPR](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr)。

### 直接接收符合XDM的同意資料 {#batch}

您可以使用批處理接收從CSV檔案接收符合XDM的同意資料。 如果您積壓了以前收集的同意資料，但尚未整合到客戶配置檔案中，則此功能非常有用。

按照本教程 [將CSV檔案映射到XDM](../../../../ingestion/tutorials/map-csv/overview.md) 瞭解如何將資料欄位轉換為XDM並將其轉換為平台。 選擇 [!UICONTROL 目標] 對於映射，請確保選擇 **[!UICONTROL 使用現有資料集]** 選項 [!DNL Profile]-enabled concense dataset，您以前建立的。

## Test您的實施 {#test-implementation}

在您將客戶同意資料 [!DNL Profile]-enabled dataset，您可以檢查更新的配置檔案，以查看它們是否包含同意屬性。

>[!IMPORTANT]
>
>要查看UI中現有配置檔案的屬性，必須至少知道與該配置檔案關聯的一個標識值（及其相應的命名空間）。
>
>如果您無權訪問此資訊，則可以選擇接收您自己的test同意資料，並將其與您知道的身份值/命名空間關聯。

請參閱 [按身份瀏覽配置檔案](../../../../profile/ui/user-guide.md#browse) 的 [!DNL Profile] 有關如何查找配置檔案詳細資訊的特定步驟的UI指南。

預設情況下，新的同意屬性不會出現在配置檔案的儀表板上。 因此，必須導航到 **[!UICONTROL 屬性]** 的子菜單。 請參閱 [配置檔案儀表板](../../../../profile/ui/profile-dashboard.md) 瞭解如何根據您的需要自定義儀表板。

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## 後續步驟

本指南介紹了如何配置平台操作以使用Adobe標準處理客戶同意資料，並使這些屬性在客戶配置檔案中表示。 您現在可以將客戶同意偏好作為細分資格和其它下游使用案例中的決定性因素進行整合。

有關Experience Platform隱私相關功能的詳細資訊，請參閱 [平台中的治理、隱私和安全](../../overview.md)。
