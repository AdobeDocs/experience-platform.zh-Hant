---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Adobe Experience Platform中的同意處理
topic-legacy: getting started
description: 了解如何使用Adobe2.0標準，在Adobe Experience Platform中處理客戶同意訊號。
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---

# Adobe Experience Platform中的同意處理

Adobe Experience Platform可讓您處理從客戶收集到的同意資料，並將其整合至您儲存的客戶設定檔中。 下遊程式接著便可使用此資料來判斷資料收集是否針對特定客戶進行，或其設定檔是否用於特定用途。 例如，特定設定檔的同意資料可判斷其是否可納入匯出的受眾區段，或是否可參與特定行銷管道，例如電子郵件、簡訊或推播通知。

本檔案概述如何設定您的Platform資料操作，以內嵌同意管理平台(CMP)產生的客戶同意資料，並將該資料整合至下游使用案例的客戶設定檔中。

>[!NOTE]
>
>本檔案著重於使用Adobe標準處理同意資料。 若您是依照IAB透明與同意架構(TCF)2.0處理同意資料，請參閱 [Adobe Real-time Customer Data Platform的TCF 2.0支援](../iab/overview.md).

## 先決條件

本指南需要妥善了解處理同意資料所涉及的各種Experience Platform服務：

* [Experience Data Model(XDM)](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md):通過跨裝置和系統橋接身分，解決客戶體驗資料分散帶來的根本難題。
* [即時客戶個人檔案](../../../../profile/home.md):使用 [!DNL Identity Service] 功能，即時從資料集建立詳細的客戶設定檔。 即時客戶設定檔會從資料湖提取資料，並將客戶設定檔保存在其自己的個別資料存放區。
* [Adobe Experience Platform Web SDK](../../../../edge/home.md):用戶端JavaScript程式庫，可讓您將各種平台服務整合至您面向客戶的網站。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md):本指南中所示同意相關SDK命令的使用案例概述。
* [Adobe Experience Platform區段服務](../../../../segmentation/home.md):可讓您將即時客戶設定檔資料分割為具有類似特徵且會對行銷策略採取類似回應的個人群組。

## 同意處理流程摘要 {#summary}

以下說明在正確設定系統後，如何處理同意資料：

1. 客戶會透過您網站上的對話方塊，提供資料收集的同意偏好設定。
1. 在每次載入頁面時（或當CMP偵測到同意偏好設定的變更時），網站上的自訂指令碼會將目前偏好設定對應至標準XDM物件。 此物件隨後會傳遞至Platform Web SDK `setConsent` 命令。
1. 當 `setConsent` 即為呼叫，Platform Web SDK會檢查同意值與上次收到的值是否不同。 如果值不同（或沒有先前的值），則結構化同意/偏好設定資料會傳送至Adobe Experience Platform。
1. 同意/偏好設定資料會擷取至 [!DNL Profile] — 啟用的資料集，其架構包含同意/偏好設定欄位。

除了CMP同意變更鈎點所觸發的SDK命令外，同意資料也可透過任何客戶產生的XDM資料流入Experience Platform，這些資料會直接上傳至 [!DNL Profile] — 已啟用的資料集。

### 同意強制執行

在目前版本的Platform同意處理支援中，僅有資料收集權限(`collect.val`)會由Platform Web SDK自動執行。 雖然可以收集更詳細的同意和偏好設定並保留在客戶設定檔中，但您必須在自己的下遊程式中手動強制執行這些額外訊號。

>[!NOTE]
>
>如需上述XDM同意欄位結構的詳細資訊，請參閱 [[!UICONTROL 同意和偏好設定] 資料類型](../../../../xdm/data-types/consents.md).

完成系統設定後，Platform Web SDK會解譯目前使用者的資料收集同意值，以判斷資料應該傳送至Adobe Experience Platform邊緣網路、從用戶端刪除或保存，直到資料收集權限設為是或否為止。

## 決定如何在CMP中產生客戶同意資料 {#consent-data}

由於每個CMP系統都是獨一無二的，因此您必須決定讓客戶在與您的服務互動時提供同意的最佳方式。 達成此目的的常見方式是使用類似下列範例的Cookie同意對話方塊：

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

此對話方塊應可讓客戶選擇加入或退出其資料的特定行銷和個人化使用案例。 這些同意和偏好應符合您為 [!DNL Profile]啟用資料集。

## 將標準化同意欄位新增至 [!DNL Profile]啟用的資料集 {#dataset}

客戶同意資料必須傳送至 [!DNL Profile] — 啟用的資料集，其架構包含同意欄位。 這些欄位必須包含在您用來擷取個別客戶屬性資訊的相同結構和資料集中。

請參閱 [設定資料集以擷取同意資料](./dataset.md) 以取得如何將這些必要欄位新增至 [!DNL Profile]啟用資料集，再繼續使用本指南。

## 更新 [!DNL Profile] 合併原則以包含同意資料 {#merge-policies}

建立 [!DNL Profile]啟用資料集以處理同意資料，您必須確定您的合併原則已設定為一律在每個客戶設定檔中包含同意欄位。 這需要設定資料集優先順序，讓同意資料集優先順序高於其他可能發生衝突的資料集。

>[!NOTE]
>
>如果沒有任何衝突的資料集，則應為合併策略設定時間戳優先順序。 這有助於確保客戶指定的最新同意為使用的同意設定。

有關如何使用合併策略的詳細資訊，請從閱讀 [合併策略概述](../../../../profile/merge-policies/overview.md). 設定合併原則時，您必須確定您的設定檔包含 [!UICONTROL 同意和偏好設定] 方案欄位群組，如 [資料集準備](./dataset.md).

## 將同意資料帶入Platform

取得資料集並合原則以代表客戶設定檔中的必要同意欄位後，下一步就是將同意資料本身匯入Platform。

主要來說，每當CMP偵測到同意變更事件時，您應使用Adobe Experience Platform Web SDK將同意資料傳送至Platform。 如果您是在行動平台上收集同意資料，應使用Adobe Experience Platform Mobile SDK。 您也可以將收集到的同意資料對應至同意資料集的XDM結構，並透過批次內嵌傳送至Platform，以選擇直接內嵌該資料。

以下各小節將提供這些方法的詳細資訊。

### 配置Experience PlatformWeb SDK以處理同意資料 {#web-sdk}

一旦您將CMP設定為監聽網站上的同意變更事件，您就可以整合Experience PlatformWeb SDK以接收更新的同意設定，並在每次載入頁面時以及每當同意變更事件發生時將其傳送至Platform。 請參閱 [設定Web SDK以處理客戶同意資料](../sdk.md) 以取得更多資訊。

### 設定Experience Platform行動SDK以處理同意資料 {#mobile-sdk}

如果您的行動應用程式需要Experience Platform同意偏好設定，您可以整合客戶行動SDK以擷取和更新同意設定，並在呼叫同意API時將其傳送至Platform。

請參閱行動SDK檔案，以取得 [設定「同意」行動擴充功能](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network) 和 [使用同意API](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network/api-reference). 如需如何使用行動SDK處理隱私權疑慮的詳細資訊，請參閱區段 [隱私權與GDPR](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr).

### 直接擷取符合XDM的同意資料 {#batch}

您可以使用批次內嵌，從CSV檔案內嵌符合XDM的同意資料。 如果您先前收集的同意資料積壓，尚未整合至客戶設定檔中，這個功能會很實用。

請依照 [將CSV檔案對應至XDM](../../../../ingestion/tutorials/map-csv/overview.md) 了解如何將資料欄位轉換為XDM，並將其內嵌至Platform。 選取 [!UICONTROL 目的地] 對應時，請確定您選取 **[!UICONTROL 使用現有資料集]** 選項，然後選擇 [!DNL Profile] — 啟用您先前建立的同意資料集。

## 測試您的實作 {#test-implementation}

將客戶同意資料擷取至 [!DNL Profile]啟用資料集，您可以檢查更新的設定檔，以查看它們是否包含同意屬性。

>[!IMPORTANT]
>
>若要在UI中檢視現有設定檔的屬性，您必須知道至少一個與該設定檔相關聯的身分值（及其對應的命名空間）。
>
>如果您無法存取此資訊，可以選擇內嵌自己的測試同意資料，並將其與您所知的身分值/命名空間建立關聯。

請參閱 [依身分瀏覽設定檔](../../../../profile/ui/user-guide.md#browse) 在 [!DNL Profile] 有關如何查詢設定檔詳細資訊的特定步驟的UI指南。

依預設，新的同意屬性不會出現在設定檔的控制面板上。 因此，您必須導覽至 **[!UICONTROL 屬性]** 標籤，以確認其已如預期擷取。 請參閱 [設定檔控制面板](../../../../profile/ui/profile-dashboard.md) 了解如何自訂控制面板以符合您的需求。

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## 後續步驟

本指南說明如何設定您的Platform作業，以使用Adobe標準處理客戶同意資料，並在客戶設定檔中呈現這些屬性。 您現在可以整合客戶同意偏好設定，作為區段資格和其他下游使用案例的決定因素。

如需Experience Platform隱私權相關功能的詳細資訊，請參閱 [Platform中的控管、隱私權和安全性](../../overview.md).
