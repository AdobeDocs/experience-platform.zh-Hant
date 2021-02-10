---
keywords: email;Email;e-mail;email destinations;oracle exorca;oracle
title: Oracle Evolca連接
description: Oracle Exvola是Oracle為行銷自動化提供的軟體即服務(SaaS)平台，旨在幫助B2B行銷人員和組織管理營銷活動和銷售線索生成。
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# [!DNL Oracle Eloqua] 連接

[[!DNL Oracle Eloqua]](https://www.oracle.com/marketingcloud/products/marketing-automation/) 是由B2B行銷人員和組織提供的行銷自動化軟體即服務(SaaS) [!DNL Oracle] 平台，旨在協助B2B行銷人員和組織管理行銷活動和銷售機會開發。

若要傳送區段資料至[!DNL Oracle Eloqua]，您必須先[連接Adobe Experience Platform中的目標](#connect-destination)，然後[設定從儲存位置匯入](#import-data-into-eloqua)的資料。[!DNL Oracle Eloqua]

## 導出類型{#export-type}

**基於描述檔** -您要匯出區段的所有成員，以及所要的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](../../ui/activate-destinations.md#select-attributes)。

## 連接到目標{#connect-destination}

在&#x200B;**[!UICONTROL 連接]** > **[!UICONTROL 目標]**&#x200B;中，選擇[!DNL Oracle Eloqua] ，然後選擇&#x200B;**[!UICONTROL 連接目標]**。

[連線Exola](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟中，如果您先前已設定到雲儲存目標的連接，請選擇&#x200B;**[!UICONTROL Existing Account]**&#x200B;並選擇一個現有連接。 或者，您可以選擇&#x200B;**[!UICONTROL 新帳戶]**&#x200B;來設定新連接。 填寫您的帳戶驗證憑證，然後選擇&#x200B;**[!UICONTROL 連接到目標]**。 對於[!DNL Oracle Eloqua]，可以在&#x200B;**[!UICONTROL 使用密碼]**&#x200B;的SFTP和&#x200B;**[!UICONTROL 使用SSH密鑰]**&#x200B;的SFTP之間進行選擇。 根據您的連接類型填寫以下資訊，然後選擇&#x200B;**[!UICONTROL 連接到目標]**。

對於具有Password ]**連接的**[!UICONTROL SFTP，必須提供域、埠、用戶名和密碼。
對於具有SSH密鑰]**連接的**[!UICONTROL  SFTP，必須提供域、埠、用戶名和SSH密鑰。

![設定Exola精靈](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

在&#x200B;**[!UICONTROL Setup]**&#x200B;步驟中，填寫目標的相關資訊，如下所示：
- **[!UICONTROL 名稱]**:為目的地選擇相關名稱。
- **[!UICONTROL 說明]**:輸入目標的說明。
- **[!UICONTROL 資料夾路徑]**:在您的儲存位置提供路徑，讓Platform將匯出資料儲存為CSV或Tab分隔檔案。
- **[!UICONTROL 檔案格式]**: **CSV** 或 **TAB_DELIMITED**。選擇要導出到儲存位置的檔案格式。

![雄辯基本資訊](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

填寫上述欄位後，按一下「建立目標」。 ****&#x200B;您的目標現在已建立，您可以[啟用區段](../../ui/activate-destinations.md)至目標。

## 啟用區段{#activate-segments}

如需區段啟動工作流程的相關資訊，請參閱[啟用設定檔和區段至目標](../../ui/activate-destinations.md)。

## 目標屬性{#destination-attributes}

當[啟用區段](../../ui/activate-destinations.md)至[!DNL Oracle Eloqua]目標時，我們建議您從[union架構](../../../profile/home.md#profile-fragments-and-union-schemas)中選取唯一識別碼。 選擇要導出到目標的唯一標識符和任何其他XDM欄位。 如需詳細資訊，請參閱「電子郵件行銷目標」中的[選取要在匯出檔案](./overview.md#destination-attributes)中當做目標屬性的架構欄位。

## 導出資料{#exported-data}

對於[!DNL Oracle Eloqua]目標，平台會在您提供的儲存位置中建立以定位點分隔的`.txt`或`.csv`檔案。 如需檔案的詳細資訊，請參閱區段啟動教學課程中的[電子郵件行銷目標和雲端儲存目標](../../ui/activate-destinations.md#esp-and-cloud-storage)。

## 將資料導入設定為[!DNL Oracle Eloqua] {#import-data-into-eloqua}

將平台連接到Amazon S3或SFTP儲存後，您必須將資料從儲存位置導入[!DNL Oracle Eloqua]。 要瞭解如何完成此操作，請參閱[!DNL Oracle Eloqua Help Center]中的[導入聯繫人或帳戶](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm)。