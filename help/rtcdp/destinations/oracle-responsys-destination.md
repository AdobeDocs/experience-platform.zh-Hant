---
title: Oracle Responsys目標
seo-title: Oracle Responsys目標
description: Responsys是Oracle針對跨通道行銷宣傳提供的企業電子郵件行銷工具，可個人化電子郵件、行動裝置、展示廣告和社交媒體之間的互動。
seo-description: Responsys是Oracle針對跨通道行銷宣傳提供的企業電子郵件行銷工具，可個人化電子郵件、行動裝置、展示廣告和社交媒體之間的互動。
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Oracle Responsys

## 概述

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) 是Oracle針對跨通道行銷宣傳提供的企業電子郵件行銷工具，可個人化電子郵件、行動裝置、展示廣告和社交媒體之間的互動。

要將段資料發送到Oracle Responsys，您必須先連接到 [Adobe Real-time Customer Data Platform中的目標](#connect-destination) ，然後 [](#import-data-into-responsys) 設定從儲存位置將資料導入到Oracle Responsys。

## 連接目標 {#connect-destination}

1. 在中 **[!UICONTROL Connections > Destinations]**，選擇Oracle Responsys，然後選擇 **[!UICONTROL Connect destination]**。

   ![連線至Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. 在此步 **[!UICONTROL Authentication]** 驟中，如果您先前已設定雲端儲存空間目的地的連線，請選取並選 **[!UICONTROL Existing Account]** 取其中一個現有連線。 或者，您可以選 **[!UICONTROL New Account]** 擇設定新連接。 填寫您的帳戶驗證憑證並選取 **[!UICONTROL Connect to destination]**。 對於Oracle Responsys，您可以選擇和之 **[!UICONTROL SFTP with Password]** 間 **[!UICONTROL SFTP with SSH Key]**。 根據您的連線類型，填寫下列資訊，然後選取 **[!UICONTROL Connect to destination]**。

   對於 **[!UICONTROL SFTP with Password]** 連接，必須提供域、埠、用戶名和密碼。
對於 **[!UICONTROL SFTP with SSH Key]** 連接，必須提供域、埠、用戶名和SSH密鑰。

   ![填寫Responsys資訊](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. 在步驟 **[!UICONTROL Setup]** 中，請填寫您目的地的相關資訊，如下所示：
   * **[!UICONTROL Name]**:為目的地選擇相關名稱。
   * **[!UICONTROL Description]**:輸入目標的說明。
   * **[!UICONTROL Folder Path]**:在儲存位置中提供路徑，即時CDP會將導出資料儲存為CSV或Tab分隔檔案。
   * **[!UICONTROL File Format]**: **CSV****或TAB_DELIMITED**。 選擇要導出到儲存位置的檔案格式。
   ![Responsys基本資訊](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. 填寫 **[!UICONTROL Create destination]** 上述欄位後按一下。 您的目標現在已連線，您可 [以啟動區段](/help/rtcdp/destinations/activate-destinations.md) 至目標。

## 目標屬性 {#destination-attributes}

在將 [段激活到](/help/rtcdp/destinations/activate-destinations.md) Oracle Responsys目標時，建議您從聯合方案中選擇一個唯 [一標識符](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)。 選擇唯一標識符和要導出到目標的任何其他XDM欄位。 如需詳細資訊，請參 [閱「電子郵件行銷目標」中，選取要在匯出檔案中當做目標屬性使用的架構欄位](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。

## 設定資料導入到Oracle Responsys {#import-data-into-responsys}

將即時CDP連接到Amazon S3或SFTP儲存後，您必須設定從儲存位置將資料導入到Oracle Responsys。 要瞭解如何完成此操作，請參 [閱Oracle Responsys幫助中心的](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) 「導入聯繫人或帳戶」。