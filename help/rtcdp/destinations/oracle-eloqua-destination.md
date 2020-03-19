---
title: Oracle Exolca目標
seo-title: Oracle Exolca目標
description: Oracle Exvola是Oracle為行銷自動化提供的軟體即服務(SaaS)平台，旨在幫助B2B行銷人員和組織管理營銷活動和銷售線索生成。
seo-description: Oracle Exvola是Oracle為行銷自動化提供的軟體即服務(SaaS)平台，旨在幫助B2B行銷人員和組織管理營銷活動和銷售線索生成。
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Exovila

## 概述

[Evolca](https://www.oracle.com/marketingcloud/products/marketing-automation/) 是Oracle針對行銷自動化提供的軟體即服務(SaaS)平台，旨在幫助B2B行銷人員和組織管理行銷活動和銷售線索產生。

要將段資料發送到Oracle Exporca，您必須先連接 [Adobe Real-time Customer](#connect-destination) Data Platform中的目標，然後 [](#import-data-into-eloqua) 設定從儲存位置將資料導入Oracle Exporca。

## 連接到目標 {#connect-destination}

1. 在「 **[!UICONTROL 連接」>「目標]**」中，選擇Oracle Exolica，然後選擇「連 **[!UICONTROL 接目標」]**。

   ![連線Exola](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

1. 在連接目標嚮導中，選擇存 **[!UICONTROL 儲位置的連接類型]** 。 對於Oracle Exolca，您可以在 **SFTP with Password和** SSH Key之間選擇 ****。 根據您的連線類型，填寫下列資訊，然後選取「連 **[!UICONTROL 線」]**。

   ![設定Exola精靈](/help/rtcdp/destinations/assets/eloqua-wizard.png)

   對於 **具有密碼連接的SFTP** ，必須提供域、埠、用戶名和密碼。
對於 **具有SSH密鑰連接的SFTP** ，必須提供域、埠、用戶名和SSH密鑰。

   ![填寫雄辯資訊](/help/rtcdp/destinations/assets/eloqua-step2.png)

1. 在基 **本資訊中**，填入您目的地的相關資訊，如下所示：
   * **名稱**:為目的地選擇相關名稱。
   * **說明**:輸入目標的說明。
   * **資料夾路徑**:在儲存位置中提供路徑，即時CDP會將導出資料儲存為CSV或Tab分隔檔案。
   * **檔案格式**: **CSV****或TAB_DELIMITED**。 選擇要導出到儲存位置的檔案格式。
   ![雄辯基本資訊](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

1. 填寫 **基本** 「資訊」欄位後，按一 **下建立**。 您的目標現在已連線，您可 [以啟動區段](/help/rtcdp/destinations/activate-destinations.md) 至目標。

## 目標屬性

在 [激活段](/help/rtcdp/destinations/activate-destinations.md) 到Oracle Exolca目標時 [，我們建議您從聯合方案中選擇唯一](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)標識符。 選擇唯一標識符以及要導出到目標的任何其它XDM欄位。 如需詳細資訊，請參 [閱「電子郵件行銷目標」中，選取要在匯出檔案中當做目標屬性使用的架構欄位](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。

## 設定資料導入到Oracle Exolca {#import-data-into-eloqua}

將即時CDP連接到Amazon S3或SFTP儲存後，您必須設定從儲存位置將資料導入Oracle Exporca。 要瞭解如何完成此操作，請參 [閱Oracle Expolca幫助中心的](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) 「導入聯繫人或帳戶」。