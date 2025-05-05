---
title: （公司） LinkedIn連線
description: 使用此目標來啟用 Account-Based Marketing (ABM) 使用案例的帳戶客群。根據雜湊電子郵件，為您的LinkedIn行銷活動啟用設定檔，以用於對象目標定位、個人化和隱藏。
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hant#rtcdp-editions newtab=true"
badgeB2P: label="B2P版本" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hant#rtcdp-editions newtab=true"
exl-id: 68d2cca3-952b-49d0-8ea2-e776a233b752
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 5%

---

# （公司） LinkedIn比對受眾連線 {#companies-linkedin}

>[!AVAILABILITY]
>
>針對（公司） LinkedIn目的地啟用帳戶對象的功能，適用於購買[企業對企業](/help/rtcdp/overview.md#rtcdp-b2b)和[企業對個人](/help/rtcdp/overview.md#rtcdp-b2p)版Real-Time Customer Data Platform的公司。

使用此目的地為Account-Based Marketing (ABM)使用案例啟用您的[帳戶對象](/help/segmentation/types/account-audiences.md)。 透過&#x200B;**[!UICONTROL （公司） LinkedIn]**&#x200B;企業對企業目的地，向目標帳戶中的相關角色和角色做廣告。 瀏覽LinkedIn檔案，以[進一步瞭解LinkedIn平台上的帳戶目標定位](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting)。

>[!TIP]
>
>若是個別層級（或企業對消費者）的使用案例，Adobe建議您使用[LinkedIn相符對象](/help/destinations/catalog/social/linkedin.md)目的地。

在Experience Platform UI中顯示的![LinkedIn帳戶目的地。](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | X | 對象[從CSV檔案匯入](../../../segmentation/ui/overview.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-and-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|--------------|-----------|---------------------------|
| 匯出型別 | 對象匯出 | 所有對象成員將會匯出包含金鑰識別碼，例如姓名、電話號碼等。 |
| 頻率 | 串流 | 「隨時待命」API型連線。 設定檔變更後，更新會立即傳送到下游。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

確認您符合下列必要條件，即可將帳戶對象匯出至LinkedIn：

### LinkedIn帳戶必要條件 {#LinkedIn-account-prerequisites}

使用[!UICONTROL （公司） LinkedIn相符對象]目的地之前，請先確定您的[!DNL LinkedIn Campaign Manager]帳戶具有[!DNL Creative Manager]或更高的許可權層級。

若要瞭解如何編輯您的[!DNL LinkedIn Campaign Manager]使用者許可權，請參閱LinkedIn檔案中的[新增、編輯及移除Advertising帳戶的使用者許可權](https://www.linkedin.com/help/lms/answer/5753)。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

1. 在目的地目錄中尋找[!DNL (Companies) LinkedIn Matched Audiences]目的地，並選取&#x200B;**[!UICONTROL 設定]**。
2. 選取&#x200B;**[!UICONTROL 連線到目的地]**。
   ![驗證LinkedIn](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. 輸入您的LinkedIn認證並選取&#x200B;**登入**。

使用LinkedIn完成登入程式後，您可以繼續進行下一個步驟。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 帳戶識別碼]**：您的[!DNL LinkedIn Campaign Manager Account ID]。 您可以在您的[!DNL LinkedIn Campaign Manager]帳戶中找到此ID。

您現在已準備好在LinkedIn中啟用帳戶對象。

## 啟動此目標的客群 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用帳戶的對象到目的地。](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的帳戶對象。"){width="100" zoomable="yes"}

閱讀[啟用帳戶對象](/help/destinations/ui/activate-account-audiences.md)以取得啟用此目的地的帳戶對象的指示。

## 啟用帳戶對象至&#x200B;**[!UICONTROL （公司） LinkedIn相符對象]**&#x200B;目的地時，對應步驟中所需的對應配對 {#required-mappings}

將帳戶對象啟用至&#x200B;**[!UICONTROL （公司） LinkedIn相符對象]**&#x200B;目的地時，請注意，若要成功匯出資料，下列兩個對應配對是必要的：

![LinkedIn對應必要欄位。](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| 來源欄位 | 目標欄位 |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` （選取&#x200B;**[!UICONTROL 目標欄位]**&#x200B;時，在&#x200B;**[!UICONTROL 選取身分識別名稱空間]**&#x200B;檢視中選取此欄位）。<br> ![選取工作流程中反白的身分名稱空間，以啟用帳戶的對象到目的地。](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的帳戶對象。"){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## 匯出的資料 {#exported-data}

成功啟用意味著[!DNL LinkedIn]自訂對象是以程式設計方式在[[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login)中建立。 當使用者符合或不符合啟用的受眾的資格時，會調整受眾成員資格。
