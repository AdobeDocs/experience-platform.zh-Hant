---
keywords: email;Email;e-mail;email destinations;oracle eloqua;oracle
title: Oracle Exolca目標
seo-title: Oracle Exolca目標
description: Oracle Exvola是Oracle為行銷自動化提供的軟體即服務(SaaS)平台，旨在幫助B2B行銷人員和組織管理營銷活動和銷售線索生成。
seo-description: Oracle Exvola是Oracle為行銷自動化提供的軟體即服務(SaaS)平台，旨在幫助B2B行銷人員和組織管理營銷活動和銷售線索生成。
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# [!DNL Oracle Eloqua]

## 概述

[[!DNL Oracle Eloqua]](https://www.oracle.com/marketingcloud/products/marketing-automation/) 是由B2B行銷人員和組織提供的行銷自動化軟體即服務(SaaS)平 [!DNL Oracle] 台，旨在協助B2B行銷人員和組織管理行銷活動和銷售機會開發。

若要傳送區段資 [!DNL Oracle Eloqua]料至，您必須先在即時 [客戶資料平台中連線目標](#connect-destination) ，然後設 [定從儲存位置匯入資料的方式](#import-data-into-eloqua)[!DNL Oracle Eloqua]。

## 匯出類型 {#export-type}

**基於配置檔案** -您正在導出段的所有成員，以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](../../ui/activate-destinations.md#select-attributes)。

## 連接到目標 {#connect-destination}

在「連 **[!UICONTROL 接]** >目 **[!UICONTROL 的地]**」中，選 [!DNL Oracle Eloqua]擇，然後選 **[!UICONTROL 擇「連接目標]**」。

[連線Exola](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

在「驗 **[!UICONTROL 證]** 」步驟中，如果您先前已設定雲端儲存空間目的地的連線，請選取「現有帳戶 **** 」並選取您現有的連線。 或者，您可以選 **[!UICONTROL 擇「新帳戶]** 」來設定新連線。 填寫您的帳戶驗證憑證，並選取「 **[!UICONTROL 連線至目的地」]**。 對於 [!DNL Oracle Eloqua]，您可以在 **[!UICONTROL SFTP與Password之間選擇]** , **[!UICONTROL SFTP與SSH密鑰之間選擇]**。 根據您的連線類型，填寫下列資訊，然後選取「連 **[!UICONTROL 線至目的地」]**。

對於 **[!UICONTROL 具有密碼連接的SFTP]** ，必須提供域、埠、用戶名和密碼。
對於 **[!UICONTROL 具有SSH密鑰連接的SFTP]** ，必須提供域、埠、用戶名和SSH密鑰。

![設定Exola精靈](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

在「設 **[!UICONTROL 定]** 」步驟中，填入您目的地的相關資訊，如下所示：
- **[!UICONTROL 名稱]**:為目的地選擇相關名稱。
- **[!UICONTROL 說明]**:輸入目標的說明。
- **[!UICONTROL 資料夾路徑]**:在儲存位置中提供路徑，即時CDP會將導出資料儲存為CSV或Tab分隔檔案。
- **[!UICONTROL 檔案格式]**: **CSV** 或 **TAB_DELIMITED**。 選擇要導出到儲存位置的檔案格式。

![雄辯基本資訊](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

填寫 **[!UICONTROL 上述欄位後]** ，按一下「建立目標」。 您的目標現在已建立，您可 [以啟用區段](../../ui/activate-destinations.md) 至目標。

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](../../ui/activate-destinations.md) ，請參閱啟用設定檔和區段至目的地。

## 目標屬性 {#destination-attributes}

在啟 [用區段](../../ui/activate-destinations.md) ，到目 [!DNL Oracle Eloqua] 的地時，建議您從聯合架構中選取唯一 [識別碼](../../../profile/home.md#profile-fragments-and-union-schemas)。 選擇要導出到目標的唯一標識符和任何其他XDM欄位。 如需詳細資訊，請參 [閱「電子郵件行銷目標」中，選取要在匯出檔案中當做目標屬性使用的架構欄位](./overview.md#destination-attributes) 。

## 匯出的資料 {#exported-data}

對於 [!DNL Oracle Eloqua] 目標，即時CDP會在您提供的儲存位置中建立以Tab `.txt` 分隔 `.csv` 的或檔案。 如需檔案的詳細資訊，請參閱區 [段啟動教學課程中的「電子郵件行銷目標](../../ui/activate-destinations.md#esp-and-cloud-storage) 」和「雲端儲存目標」。

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Oracle_Eloqua_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Oracle_Eloqua_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Oracle_Eloqua_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Oracle_Eloqua_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## 設定資料匯入至 [!DNL Oracle Eloqua] {#import-data-into-eloqua}

將即時CDP連接到Amazon S3或SFTP儲存後，您必須將資料從儲存位置導入到中 [!DNL Oracle Eloqua]。 要瞭解如何完成此操作，請參 [閱中的導入聯繫人](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) 或帳戶 [!DNL Oracle Eloqua Help Center]。