---
keywords: email;Email;e-mail;email destinations;adobe campaign;campaign
title: Adobe Campaign連線
description: Adobe Campaign是一套解決方案，可協助您跨所有線上及線下通道個人化並傳遞宣傳活動。
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 0%

---


# Adobe Campaign連線

Adobe Campaign是一套解決方案，可協助您跨所有線上及線下通道個人化並傳遞宣傳活動。 如需詳細資訊，請參閱[關於Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html)。

若要傳送區段資料至Adobe Campaign，您必須先[連接Adobe Experience Platform中的目標](#connect-destination)，然後[設定從儲存位置匯入](#import-data-into-campaign)的資料。

## 導出類型{#export-type}

**基於描述檔** -您要匯出區段的所有成員，以及所要的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](../../ui/activate-destinations.md#select-attributes)。

## 連接目標{#connect-destination}

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，選擇Adobe Campaign，然後選擇&#x200B;**[!UICONTROL Connect destination]**。

![連線至Adobe Campaign](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

在連接目標工作流中，為儲存位置選擇&#x200B;**[!UICONTROL 連接類型]**。 對於Adobe Campaign，您可以選擇&#x200B;**[!UICONTROL Amazon S3]**、**[!UICONTROL SFTP with Password]**、**[!UICONTROL SFTP with SSH Key]**&#x200B;和&#x200B;**[!UICONTROL Azure Blob]**。 根據您的連接類型填寫以下資訊，然後選擇&#x200B;**[!UICONTROL Connect]**。

![設定促銷活動精靈](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- 對於&#x200B;**[!UICONTROL Amazon S3]**&#x200B;連接，您必須提供您的訪問密鑰ID和秘密訪問密鑰。
- 對於具有Password ]**連接的**[!UICONTROL  SFTP，必須提供域、埠、用戶名和密碼。
- 對於具有SSH密鑰&#x200B;]**連接的**[!UICONTROL  SFTP，必須提供域、埠、用戶名和SSH密鑰。
- 對於&#x200B;**[!UICONTROL Azure Blob]**&#x200B;連接，必須提供連接字串。

或者，您可以將RSA格式的公鑰附加到&#x200B;**[!UICONTROL 密鑰]**&#x200B;部分下的導出檔案中，以添加PGP/GPG加密。 請注意，此公共密鑰&#x200B;**必須**&#x200B;寫入為Base64編碼字串。

![填寫促銷活動資訊](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

在&#x200B;**[!UICONTROL 基本資訊]**&#x200B;中，填寫您目的地的相關資訊，如下所示：
- **[!UICONTROL 名稱]**:為目的地選擇相關名稱。
- **[!UICONTROL 說明]**:輸入目標的說明。
- **[!UICONTROL 貯體名稱]**: *適用於S3連線*。輸入S3儲存貯體的位置，平台會將匯出資料儲存為CSV或Tab分隔檔案。
- **[!UICONTROL 資料夾路徑]**:在您的儲存位置提供路徑，讓Platform將匯出資料儲存為CSV或Tab分隔檔案。
- **[!UICONTROL 容器]**: *用於Blob連接*。保存資料夾路徑所在的Blob的容器。
- **[!UICONTROL 檔案格式]**: **CSV** 或 **TAB_DELIMITED**。選擇要導出到儲存位置的檔案格式。
- **[!UICONTROL 行銷動作]**:行銷動作會指出將資料匯出至目的地的方式。您可以從Adobe定義的行銷動作中選擇，也可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱Adobe Experience Platform中的[資料治理](../../../data-governance/policies/overview.md)頁面。 如需個別Adobe定義之行銷動作的詳細資訊，請參閱[資料使用政策概觀](../../../data-governance/policies/overview.md)。

![促銷活動基本資訊](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

填寫上述欄位後，按一下「建立」。 ****&#x200B;您的目標現在已連線，您可以[啟動區段](../../ui/activate-destinations.md)至目標。

## 啟用區段{#activate-segments}

如需區段啟動工作流程的相關資訊，請參閱[啟用設定檔和區段至目標](../../ui/activate-destinations.md)。

## 目標屬性{#destination-attributes}

當[啟用區段](../../ui/activate-destinations.md)至Adobe Campaign目標時，建議您從[union架構](../../../profile/home.md#profile-fragments-and-union-schemas)中選取唯一識別碼。 選擇要導出到目標的唯一標識符和任何其他XDM欄位。 如需詳細資訊，請參閱電子郵件行銷目標檔案中的[選擇要在匯出檔案](./overview.md#destination-attributes)中當做目標屬性的架構欄位。

## 導出資料{#exported-data}

對於[!DNL Adobe Campaign]目標，平台會在您提供的儲存位置中建立以定位點分隔的`.txt`或`.csv`檔案。 如需檔案的詳細資訊，請參閱區段啟動教學課程中的[電子郵件行銷目標和雲端儲存目標](../../ui/activate-destinations.md#esp-and-cloud-storage)。

## 設定資料匯入至Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>- 執行此項整合時，請記住SFTP儲存限制、資料庫儲存限制和作用中的設定檔限制。
>- 您必須使用[!DNL Campaign]工作流程，在Adobe Campaign中排程、匯入和對應匯出的區段。 請參閱Adobe Campaign檔案中的「設定循環匯入」。[](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows)



將平台連接至您的[!DNL Amazon S3]或SFTP儲存空間後，您必須設定從儲存位置匯入資料至Adobe Campaign的資料。 如要瞭解如何完成此作業，請參閱Adobe Campaign檔案中的[匯入資料](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html)。