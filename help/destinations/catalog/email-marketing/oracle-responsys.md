---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目標；oracle響應目標
title: OracleResponsys連接
description: Responsys是企業電子郵件行銷工具，可讓Oracle跨通道行銷宣傳，以個人化電子郵件、行動裝置、展示廣告和社交媒體的互動。
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# [!DNL Oracle Responsys] 連接

## 概述 {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/) 是企業電子郵件行銷工具，適用於跨通道行銷宣傳， [!DNL Oracle] 可個人化電子郵件、行動裝置、展示廣告和社交媒體的互動。

若要傳送區段資料至[!DNL Oracle Responsys]，您必須先[連線至Adobe Experience Platform的目的地](#connect-destination)，然後[設定從儲存位置匯入[!DNL Oracle Responsys]的資料。](#import-data-into-responsys)

## 導出類型{#export-type}

**基於描述檔** -您要匯出區段的所有成員，以及所要的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](../../ui/activate-destinations.md#select-attributes)。

## 連接目標{#connect-destination}

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，選擇[!DNL Oracle Responsys]，然後選擇&#x200B;**[!UICONTROL Connect destination]**。

![連線至Responsys](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

在&#x200B;**[!UICONTROL Account]**&#x200B;步驟中，如果您先前已設定到雲儲存目標的連接，請選擇&#x200B;**[!UICONTROL Existing Account]**&#x200B;並選擇一個現有連接。 或者，您可以選擇&#x200B;**[!UICONTROL New Account]**&#x200B;來設定新連接。 填寫您的帳戶驗證憑證，然後選取&#x200B;**[!UICONTROL Connect to destination]**。 對於[!DNL Oracle Responsys]，可以選擇&#x200B;**[!UICONTROL SFTP with Password]**&#x200B;和&#x200B;**[!UICONTROL SFTP with SSH Key]**。

![Connect Responsys帳戶](../../assets/catalog/email-marketing/oracle-responsys/connection-type.png)

根據您的連線類型，填寫下列資訊，然後選取&#x200B;**[!UICONTROL Configure]**。

- 對於&#x200B;**[!UICONTROL SFTP with Password]**&#x200B;連接，必須提供[!UICONTROL Domain]、[!UICONTROL Port]、[!UICONTROL Username]和[!UICONTROL Password]。
- 對於&#x200B;**[!UICONTROL SFTP with SSH Key]**&#x200B;連接，必須提供[!UICONTROL Domain]、[!UICONTROL Port]、[!UICONTROL Username]和[!UICONTROL SSH Key]。

或者，您可以將RSA格式的公鑰附加到&#x200B;**[!UICONTROL Key]**&#x200B;部分下的導出檔案中，以添加PGP/GPG加密。 您的公開金鑰必須寫入為[!DNL Base64]編碼字串。

![填寫Responsys資訊](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟中，填寫目標的相關資訊，如下所示：
- **[!UICONTROL Name]**:為目的地選擇相關名稱。
- **[!UICONTROL Description]**:輸入目標的說明。
- **[!UICONTROL Folder Path]**:在您的儲存位置提供路徑，讓Platform將匯出資料儲存為CSV或Tab分隔檔案。
- **[!UICONTROL File Format]**: **CSV** 或 **TAB_DELIMITED**。選擇要導出到儲存位置的檔案格式。
- **[!UICONTROL Marketing actions]**:行銷動作會指出將資料匯出至目的地的方式。您可以從Adobe定義的行銷動作中選擇，也可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用政策概述](../../../data-governance/policies/overview.md)。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

![Responsys基本資訊](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

填寫上述欄位後，按一下&#x200B;**[!UICONTROL Create destination]**。 您的目標現在已連線，您可以[啟動區段](../../ui/activate-destinations.md)至目標。

## 啟用區段{#activate-segments}

如需區段啟動工作流程的相關資訊，請參閱[啟用設定檔和區段至目標](../../ui/activate-destinations.md)。

## 目標屬性{#destination-attributes}

當[將段](../../ui/activate-destinations.md)激活到[!DNL Oracle Responsys]目標時，Adobe建議您從[union架構](../../../profile/home.md#profile-fragments-and-union-schemas)中選擇唯一標識符。 選擇要導出到目標的唯一標識符和任何其他XDM欄位。 有關詳細資訊，請參閱[選擇在導出檔案中用作目標屬性的架構欄位](./overview.md#destination-attributes)。

## 導出資料{#exported-data}

對於[!DNL Oracle Responsys]目標，平台會在您提供的儲存位置中建立以定位點分隔的`.txt`或`.csv`檔案。 如需檔案的詳細資訊，請參閱區段啟動教學課程中的[電子郵件行銷目標和雲端儲存目標](../../ui/activate-destinations.md#esp-and-cloud-storage)。

## 將資料導入設定為[!DNL Oracle Responsys] {#import-data-into-responsys}

將[!DNL Platform]連接到SFTP儲存後，必須將資料從儲存位置導入[!DNL Oracle Responsys]。 要瞭解如何完成此操作，請參閱[!DNL Oracle Responsys Help Center]中的[導入聯繫人或帳戶](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm)。