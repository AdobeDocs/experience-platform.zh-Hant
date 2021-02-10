---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目標；salesforce;salesforce目標
title: Salesforce Marketing Cloud連線
seo-description: Salesforce Marketing Cloud是數位行銷套裝，先前稱為ExactTarget，可讓您為訪客和客戶建構並自訂歷程，以個人化其體驗。
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud] 連接

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 是數位行銷套裝，先前稱為ExactTarget，可讓您為訪客和客戶建立和自訂歷程，以個人化其體驗。

若要將區段資料傳送至[!DNL Salesforce Marketing Cloud]，您必須先在「平台」中連接目標](#connect-destination)，然後[設定從儲存位置匯入[!DNL Salesforce Marketing Cloud]的資料。[](#import-data-into-salesforce)

## 導出類型{#export-type}

**基於描述檔** -您要匯出區段的所有成員，以及所要的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](../../ui/activate-destinations.md#select-attributes)。

## 連接目標{#connect-destination}

在&#x200B;**[!UICONTROL 連接]** > **[!UICONTROL 目標]**&#x200B;中，選擇[!DNL Salesforce Marketing Cloud] ，然後選擇&#x200B;**[!UICONTROL 連接目標]**。

![連線至Salesforce](../../assets/catalog/email-marketing/salesforce/catalog.png)

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟中，如果您先前已設定到雲儲存目標的連接，請選擇&#x200B;**[!UICONTROL Existing Account]**&#x200B;並選擇一個現有連接。 或者，您可以選擇&#x200B;**[!UICONTROL 新帳戶]**&#x200B;來設定新連接。 填寫您的帳戶驗證憑證，然後選擇&#x200B;**[!UICONTROL 連接到目標]**。 對於[!DNL Salesforce Marketing Cloud]，可以在&#x200B;**[!UICONTROL 使用密碼]**&#x200B;的SFTP和&#x200B;**[!UICONTROL 使用SSH密鑰]**&#x200B;的SFTP之間進行選擇。 根據您的連接類型填寫以下資訊，然後選擇&#x200B;**[!UICONTROL 連接到目標]**。

對於具有Password ]**連接的**[!UICONTROL  SFTP，必須提供域、埠、用戶名和密碼。

對於具有SSH密鑰&#x200B;]**連接的**[!UICONTROL  SFTP，必須提供域、埠、用戶名和SSH密鑰。

![填寫Salesforce資訊](../../assets/catalog/email-marketing/salesforce/account-info.png)

在&#x200B;**[!UICONTROL Setup]**&#x200B;步驟中，填寫目標的相關資訊，如下所示：
- **[!UICONTROL 名稱]**:為目的地選擇相關名稱。
- **[!UICONTROL 說明]**:輸入目標的說明。
- **[!UICONTROL 資料夾路徑]**:在您的儲存位置提供路徑，讓Platform將匯出資料儲存為CSV或Tab分隔檔案。
- **[!UICONTROL 檔案格式]**: **[!UICONTROL CSV]** 或 **[!UICONTROL TAB_DELIMITED]**。選擇要導出到儲存位置的檔案格式。

![Salesforce基本資訊](../../assets/catalog/email-marketing/salesforce/basic-information.png)

填寫上述欄位後，按一下「建立目標」。 ****&#x200B;您的目標現在已連線，您可以[啟動區段](../../ui/activate-destinations.md)至目標。

## 啟用區段{#activate-segments}

如需區段啟動工作流程的相關資訊，請參閱[啟用設定檔和區段至目標](../../ui/activate-destinations.md)。

## 目標屬性{#destination-attributes}

當[啟用區段](../../ui/activate-destinations.md)至[!DNL Salesforce Marketing Cloud]目標時，我們建議您從[union架構](../../../profile/home.md#profile-fragments-and-union-schemas)中選取唯一識別碼。 選擇要導出到目標的唯一標識符和任何其他XDM欄位。 如需詳細資訊，請參閱「電子郵件行銷目標」中的[選取要在匯出檔案](./overview.md#destination-attributes)中當做目標屬性的架構欄位。

## 導出資料{#exported-data}

對於[!DNL Salesforce Marketing Cloud]目標，平台會在您提供的儲存位置中建立以定位點分隔的`.txt`或`.csv`檔案。 如需檔案的詳細資訊，請參閱區段啟動教學課程中的[電子郵件行銷目標和雲端儲存目標](../../ui/activate-destinations.md#esp-and-cloud-storage)。

## 將資料導入設定為[!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

將平台連接到[!DNL Amazon S3]或SFTP儲存後，必須將資料從儲存位置導入[!DNL Salesforce Marketing Cloud]。 如要瞭解如何完成此作業，請參閱[!DNL Salesforce Help Center]中的「從檔案](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5)將訂閱者匯入Marketing Cloud」。[