---
keywords: email;Email;e-mail;email destinations;oracle responsys destination
title: Oracle Responsys連接
description: Responsys是Oracle針對跨通道行銷宣傳提供的企業電子郵件行銷工具，可個人化電子郵件、行動裝置、展示廣告和社交媒體之間的互動。
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---


# [!DNL Oracle Responsys] 連接

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) 是企業電子郵件行銷工具，適用於跨通道行銷宣傳， [!DNL Oracle] 可個人化電子郵件、行動裝置、展示廣告和社交媒體的互動。

若要傳送區段資料至[!DNL Oracle Responsys]，您必須先[連線至Adobe Experience Platform中的目標](#connect-destination)，然後[設定從儲存位置匯入](#import-data-into-responsys)至[!DNL Oracle Responsys]的資料。

## 導出類型{#export-type}

**基於描述檔** -您要匯出區段的所有成員，以及所要的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](../../ui/activate-destinations.md#select-attributes)。

## 連接目標{#connect-destination}

在&#x200B;**[!UICONTROL 連接]** > **[!UICONTROL 目標]**&#x200B;中，選擇[!DNL Oracle Responsys] ，然後選擇&#x200B;**[!UICONTROL 連接目標]**。

![連線至Responsys](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟中，如果您先前已設定到雲儲存目標的連接，請選擇&#x200B;**[!UICONTROL Existing Account]**&#x200B;並選擇一個現有連接。 或者，您可以選擇&#x200B;**[!UICONTROL 新帳戶]**&#x200B;來設定新連接。 填寫您的帳戶驗證憑證，然後選擇&#x200B;**[!UICONTROL 連接到目標]**。 對於[!DNL Oracle Responsys]，可以在&#x200B;**[!UICONTROL 使用密碼]**&#x200B;的SFTP和&#x200B;**[!UICONTROL 使用SSH密鑰]**&#x200B;的SFTP之間進行選擇。 根據您的連接類型填寫以下資訊，然後選擇&#x200B;**[!UICONTROL 連接到目標]**。

對於具有Password ]**連接的**[!UICONTROL  SFTP，必須提供域、埠、用戶名和密碼。

對於具有SSH密鑰&#x200B;]**連接的**[!UICONTROL  SFTP，必須提供域、埠、用戶名和SSH密鑰。

![填寫Responsys資訊](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

在&#x200B;**[!UICONTROL Setup]**&#x200B;步驟中，填寫目標的相關資訊，如下所示：
- **[!UICONTROL 名稱]**:為目的地選擇相關名稱。
- **[!UICONTROL 說明]**:輸入目標的說明。
- **[!UICONTROL 貯體名稱]**:您的Amazon S3儲存貯體，Platform將儲存資料匯出。您的輸入長度必須介於3到63個字元之間。 必須以字母或數字開頭和結尾。 只能包含小寫字母、數字或連字型大小(-)。 不得格式化為IP位址（例如192.100.1.1）。
- **[!UICONTROL 資料夾路徑]**:在您的儲存位置提供路徑，讓Platform將匯出資料儲存為CSV或Tab分隔檔案。
- **[!UICONTROL 檔案格式]**: **CSV** 或 **TAB_DELIMITED**。選擇要導出到儲存位置的檔案格式。
- **[!UICONTROL 行銷動作]**:行銷動作會指出將資料匯出至目的地的方式。您可以從Adobe定義的行銷動作中選擇，也可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱Adobe Experience Platform中的[資料治理](../../../data-governance/policies/overview.md)頁面。 如需個別Adobe定義之行銷動作的詳細資訊，請參閱[資料使用政策概觀](../../../data-governance/policies/overview.md)。

![Responsys基本資訊](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

填寫上述欄位後，按一下「建立目標」。 ****&#x200B;您的目標現在已連線，您可以[啟動區段](../../ui/activate-destinations.md)至目標。

## 啟用區段{#activate-segments}

如需區段啟動工作流程的相關資訊，請參閱[啟用設定檔和區段至目標](../../ui/activate-destinations.md)。

## 目標屬性{#destination-attributes}

當[啟用區段](../../ui/activate-destinations.md)至[!DNL Oracle Responsys]目標時，我們建議您從[union架構](../../../profile/home.md#profile-fragments-and-union-schemas)中選取唯一識別碼。 選擇要導出到目標的唯一標識符和任何其他XDM欄位。 如需詳細資訊，請參閱「電子郵件行銷目標」中的[選取要在匯出檔案](./overview.md#destination-attributes)中當做目標屬性的架構欄位。

## 導出資料{#exported-data}

對於[!DNL Oracle Responsys]目標，平台會在您提供的儲存位置中建立以定位點分隔的`.txt`或`.csv`檔案。 如需檔案的詳細資訊，請參閱區段啟動教學課程中的[電子郵件行銷目標和雲端儲存目標](../../ui/activate-destinations.md#esp-and-cloud-storage)。

## 將資料導入設定為[!DNL Oracle Responsys] {#import-data-into-responsys}

將平台連接到[!DNL Amazon S3]或SFTP儲存後，必須將資料從儲存位置導入[!DNL Oracle Responsys]。 要瞭解如何完成此操作，請參閱[!DNL Oracle Responsys Help Center]中的[導入聯繫人或帳戶](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm)。