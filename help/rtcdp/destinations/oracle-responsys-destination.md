---
title: Oracle Responsys目標
seo-title: Oracle Responsys目標
description: Responsys是Oracle針對跨通道行銷宣傳提供的企業電子郵件行銷工具，可個人化電子郵件、行動裝置、展示廣告和社交媒體之間的互動。
seo-description: Responsys是Oracle針對跨通道行銷宣傳提供的企業電子郵件行銷工具，可個人化電子郵件、行動裝置、展示廣告和社交媒體之間的互動。
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Responsys

## 概述

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) 是Oracle針對跨通道行銷宣傳提供的企業電子郵件行銷工具，可個人化電子郵件、行動裝置、展示廣告和社交媒體之間的互動。

要將段資料發送到Oracle Responsys，您必須先在 [Adobe Real-time Customer Data Platform中連接目標](#connect-destination) ，然後 [](#import-data-into-responsys) 設定從儲存位置將資料導入到Oracle Responsys。

## 連接目標 {#connect-destination}

1. 在「連 **[!UICONTROL 接」>「目標]**」中，選擇「Oracle Responsys」，然後選擇「連 **[!UICONTROL 接目標」]**。

   ![連線至Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

1. 在連接目標嚮導中，選擇存 **[!UICONTROL 儲位置的連接類型]** 。 對於Oracle Responsys，可以在 **SFTP with Password和** SSH Key之間選擇 ****。 根據您的連線類型，填寫下列資訊，然後選取「連 **[!UICONTROL 線」]**。

   ![設定Responsys精靈](/help/rtcdp/destinations/assets/responsys-wizard.png)

   對於 **具有密碼連接的SFTP** ，必須提供域、埠、用戶名和密碼。
對於 **具有SSH密鑰連接的SFTP** ，必須提供域、埠、用戶名和SSH密鑰。

   ![填寫Responsys資訊](/help/rtcdp/destinations/assets/responsys-step2.png)

1. 在基 **本資訊**，填寫您目的地的相關資訊，如下所示：
   * **名稱**:為目的地選擇相關名稱。
   * **說明**:輸入目標的說明。
   * **資料夾路徑**:在儲存位置中提供路徑，即時CDP會將導出資料儲存為CSV或Tab分隔檔案。
   * **檔案格式**: **CSV****或TAB_DELIMITED**。 選擇要導出到儲存位置的檔案格式。
   ![Responsys基本資訊](/help/rtcdp/destinations/assets/responsys-basic-information.png)

1. 填寫 **基本** 「資訊」欄位後，按一 **下建立**。 您的目標現在已連線，您可 [以啟動區段](/help/rtcdp/destinations/activate-destinations.md) 至目標。

## 目標屬性 {#destination-attributes}

在將 [段激活到](/help/rtcdp/destinations/activate-destinations.md) Oracle Responsys目標時，建議您從聯合方案中選擇一個唯 [一標識符](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)。 選擇唯一標識符以及要導出到目標的任何其它XDM欄位。 如需詳細資訊，請參 [閱「電子郵件行銷目標」中，選取要在匯出檔案中當做目標屬性使用的架構欄位](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。

## 設定資料導入到Oracle Responsys {#import-data-into-responsys}

將即時CDP連接到Amazon S3或SFTP儲存後，您必須設定從儲存位置將資料導入到Oracle Responsys。 要瞭解如何完成此操作，請參 [閱Oracle Responsys幫助中心的](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) 「導入聯繫人或帳戶」。