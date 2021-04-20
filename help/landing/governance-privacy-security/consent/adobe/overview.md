---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Adobe Experience Platform的許可處理
topic: getting started
description: 瞭解如何使用Adobe2.0標準處理Adobe Experience Platform的客戶同意信號。
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
translation-type: tm+mt
source-git-commit: a0f585e4aaeecb968a9fc9f408630946e1c30b2b
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 0%

---

# Adobe Experience Platform的許可處理

Adobe Experience Platform允許您處理從客戶收集到的許可資料，並將其整合到儲存的客戶個人檔案中。 然後下游流程可使用此資料來判斷資料收集是否針對特定客戶進行，或是其個人檔案是否用於特定用途。 例如，特定描述檔的同意資料可決定其是否可納入匯出的觀眾區隔，或是可以參與特定行銷管道，例如電子郵件、簡訊或推播通知。

本檔案概述如何設定您的平台資料作業，以吸收由許可管理平台(CMP)產生的客戶同意資料，並將該資料整合至下游使用案例的客戶個人檔案。

>[!NOTE]
>
>本檔案著重於使用Adobe標準處理同意資料。 如果您是遵照IAB透明與同意框架(TCF)2.0處理同意資料，請參閱「即時客戶資料平台」中[TCF 2.0支援指南](../iab/overview.md)。

## 先決條件

本指南要求對處理同意資料時涉及的各種Experience Platform服務有工作上的瞭解：

* [體驗資料模型(XDM)](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
* [Adobe Experience Platform身分服務](../../../../identity-service/home.md):透過跨裝置和系統橋接身分，解決客戶體驗資料分散所帶來的根本挑戰。
* [即時客戶個人檔案](../../../../profile/home.md):使用 [!DNL Identity Service] 功能，從資料集即時建立詳細的客戶個人檔案。即時客戶個人檔案會從資料湖提取資料，並將客戶個人檔案保留在其個別的資料儲存中。
* [Adobe Experience Platform網頁SDK](../../../../edge/home.md):用戶端JavaScript程式庫，可讓您將各種平台服務整合至您的客戶導向網站。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md):本指南中所示同意相關SDK命令的使用案例概述。
* [Adobe Experience Platform區段服務](../../../../segmentation/home.md):可讓您將即時客戶個人檔案資料分割為具有類似特性且回應類似行銷策略的個人群組。

## 許可處理流程摘要{#summary}

以下說明在正確配置系統後如何處理許可資料：

1. 客戶會透過您網站上的對話方塊提供其資料收集的同意偏好設定。
1. 在每次載入頁面時（或當CMP偵測到同意偏好的變更時），您網站上的自訂指令碼會將目前偏好對應至標準XDM物件。 然後，此物件會傳遞至平台網頁SDK `setConsent`命令。
1. 當呼叫`setConsent`時，平台網頁SDK會檢查同意值是否與上次收到的值不同。 如果這些值不同（或沒有先前的值），則結構化同意／偏好資料會傳送至Adobe Experience Platform。
1. 許可／偏好資料被吸收到[!DNL Profile]啟用的資料集中，其模式包含許可／偏好欄位。

除了由CMP同意變更勾點觸發的SDK命令外，同意資料也可以透過任何客戶產生的XDM資料流入Experience Platform，這些資料會直接上傳至啟用[!DNL Profile]的資料集。

### 許可執行

在目前版本的「平台」同意處理支援中，「平台網頁SDK」只會自動執行資料收集權限(`collect.val`)。 雖然可以收集更詳細的同意和偏好設定並保留在客戶個人檔案中，但這些額外訊號必須在您自己的下遊程式中手動強制執行。

>[!NOTE]
>
>有關上述XDM許可欄位結構的詳細資訊，請參閱[同意與首選項資料類型](../../../../xdm/data-types/consents.md)上的指南。

在系統設定完成後，平台網頁SDK會解譯目前使用者的資料收集同意值，以判斷資料應傳送至Adobe Experience Platform邊緣網路、從用戶端移除或保留，直到資料收集權限設為yes或no。

## 確定如何在CMP中生成客戶許可資料{#consent-data}

由於每個CMP系統都是獨一無二的，因此您必須確定在客戶與您的服務互動時允許他們提供許可的最佳方式。 要達成此目的，常見的方式是使用類似下列範例的Cookie同意對話方塊：

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

此對話方塊應允許客戶針對其資料選擇加入或退出特定的行銷和個人化使用案例。 這些同意和偏好應符合您在下個步驟中為[!DNL Profile]啟用資料集所定義的資料模型。

## 將標準化同意欄位新增至[!DNL Profile]啟用的資料集{#dataset}

客戶同意資料必須傳送至[!DNL Profile]啟用的資料集，其架構包含同意欄位。 這些欄位必須包含在您用來擷取個別客戶屬性資訊的相同架構和資料集中。

請參閱[設定資料集以擷取同意資料](./dataset.md)的教學課程，以取得如何在繼續使用本指南之前，將這些必要欄位新增至啟用[!DNL Profile]的資料集的詳細步驟。

## 更新[!DNL Profile]合併政策以包含同意資料{#merge-policies}

在您建立[!DNL Profile]啟用的資料集以處理同意資料後，您必須確保您的合併政策已設定為一律在每個客戶個人檔案中包含同意欄位。 這包括設定資料集優先順序，讓您的同意資料集優先順序高於其他可能衝突的資料集。

>[!NOTE]
>
>如果沒有任何衝突的資料集，則應改為設定合併策略的時間戳優先順序。 這有助於確保客戶指定的最新同意是所使用的同意設定。

有關如何使用合併策略的詳細資訊，請參閱[合併策略使用手冊](../../../../profile/ui/merge-policies.md)。 設定合併政策時，您必須確定您的個人檔案包含「同意與偏好」混合檔中提供的所有必要同意屬性，如[資料集準備](./dataset.md)指南中所述。

## 將同意資料匯入平台

一旦您取得資料集並合併原則以代表客戶個人檔案中的必要同意欄位，下一步就是將同意資料本身匯入平台。

主要是，當您的CMP偵測到同意變更事件時，您應使用Adobe Experience Platform網頁SDK將同意資料傳送至平台。 如果您是在行動平台上收集同意資料，則應使用Adobe Experience Platform行動SDK。 您也可以選擇直接將收集到的同意資料對應至您的同意資料集的XDM架構，並透過批次擷取將其傳送至平台，以便直接收錄。

以下各節將提供這些方法的詳細資訊。

### 設定Experience Platform網頁SDK以處理同意資料{#web-sdk}

一旦您將CMP設定為監聽網站上的同意變更事件，您就可整合Experience PlatformWeb SDK以接收更新的同意設定，並在每次載入頁面時及每當發生同意變更事件時，將其傳送至平台。 如需詳細資訊，請參閱[設定Web SDK以處理客戶同意資料的指南](./sdk.md)。

### 設定Experience PlatformMobile SDK以處理同意資料{#mobile-sdk}

如果您的行動應用程式需要客戶同意偏好設定，您可以整合Experience PlatformMobile SDK以擷取和更新同意設定，每當呼叫同意API時，就會將其傳送至平台。

請參閱行動SDK檔案，以取得使用「同意API」設定「同意」行動延伸模組[和「a2/」的相關資訊。 ](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge-consent)[](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge-consent/edge-consent-api-reference)有關如何使用行動SDK處理隱私權顧慮的詳細資訊，請參閱「隱私權與GDPR」一節。[](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/resources/privacy-and-gdpr)

### 直接收錄符合XDM的許可資料{#batch}

您可以使用批次擷取功能，從CSV檔案中擷取符合XDM的同意資料。 如果您有積壓的先前收集的同意資料尚未整合到客戶個人檔案中，這個功能就很有用。

請依照[將CSV檔案對應至XDM](../../../../ingestion/tutorials/map-a-csv-file.md)的教學課程，瞭解如何將資料欄位轉換為XDM並將其內嵌至平台。 為映射選擇[!UICONTROL Destination]時，請確保選擇&#x200B;**[!UICONTROL Use existing dataset]**&#x200B;選項，並選擇您先前建立的[!DNL Profile]啟用的許可資料集。

## 測試您的實作{#test-implementation}

在您將客戶同意資料收錄到啟用[!DNL Profile]的資料集後，您可以檢查更新的個人檔案，以查看他們是否包含同意屬性。

>[!IMPORTANT]
>
>若要檢視UI中現有描述檔的屬性，您必須知道至少一個與該描述檔相關聯的識別值（及其對應的命名空間）。
>
>如果您沒有此資訊的存取權，可以選擇收錄您自己的測試同意資料，並將其與您所知的識別值／命名空間建立關聯。

請參閱[!DNL Profile] UI指南中關於[依身分瀏覽描述檔的章節，以取得如何尋找描述檔詳細資訊的特定步驟。](../../../../profile/ui/user-guide.md#browse)

依預設，新的同意屬性不會出現在描述檔的控制面板上。 因此，您必須導覽至描述檔詳細資訊頁面上的&#x200B;**[!UICONTROL Attributes]**&#x200B;標籤，以確認其已如預期接收。 請參閱[描述檔控制面板](../../../../profile/ui/profile-dashboard.md)上的指南，瞭解如何自訂控制面板以符合您的需求。

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## 後續步驟

本指南介紹如何配置您的平台操作，以使用Adobe標準處理客戶同意資料，並使這些屬性在客戶配置檔案中呈現。 您現在可以將客戶同意偏好整合為區段資格和其他下游使用案例中的決定性因素。

有關Experience Platform的隱私權相關功能的詳細資訊，請參閱Platform](../../overview.md)中的[控管、隱私權與安全性概觀。
