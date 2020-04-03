---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud是數位行銷套裝，先前稱為ExactTarget，可讓您為訪客和客戶建構並自訂歷程，以個人化其體驗。
seo-description: Salesforce Marketing Cloud是數位行銷套裝，先前稱為ExactTarget，可讓您為訪客和客戶建構並自訂歷程，以個人化其體驗。
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Salesforce Marketing Cloud

## 概述

[Salesforce Marketing Cloud是數位行銷套件](https://www.salesforce.com/products/marketing-cloud/email-marketing/) ，之前稱為ExactTarget，可讓您為訪客和客戶建構並自訂歷程，以個人化其體驗。

若要傳送區段資料至Salesforce Marketing Cloud，您必須先在 [Adobe Real-time CDP中連接目標](#connect-destination) ，然後從您的儲存位置 [將資料匯入](#import-data-into-salesforce) Salesforce Marketing Cloud。

## 連接目標 {#connect-destination}

1. 在中 **[!UICONTROL Connections > Destinations]**，選取「Salesforce Marketing Cloud」，然後選取 **[!UICONTROL Connect destination]**。

   ![連線至Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. 在此步 **[!UICONTROL Authentication]** 驟中，如果您先前已設定雲端儲存空間目的地的連線，請選取並選 **[!UICONTROL Existing Account]** 取其中一個現有連線。 或者，您可以選 **[!UICONTROL New Account]** 擇設定新連接。 填寫您的帳戶驗證憑證並選取 **[!UICONTROL Connect to destination]**。 對於Salesforce Marketing Cloud，您可以選取和 **[!UICONTROL SFTP with Password]** 之間 **[!UICONTROL SFTP with SSH Key]**。 根據您的連線類型，填寫下列資訊，然後選取 **[!UICONTROL Connect to destination]**。

   對於 **[!UICONTROL SFTP with Password]** 連接，必須提供域、埠、用戶名和密碼。
對於 **[!UICONTROL SFTP with SSH Key]** 連接，必須提供域、埠、用戶名和SSH密鑰。

   ![填寫Salesforce資訊](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. 在步驟 **[!UICONTROL Setup]** 中，請填寫您目的地的相關資訊，如下所示：
   * **[!UICONTROL Name]**:為目的地選擇相關名稱。
   * **[!UICONTROL Description]**:輸入目標的說明。
   * **[!UICONTROL Folder Path]**:在儲存位置中提供路徑，即時CDP會將導出資料儲存為CSV或Tab分隔檔案。
   * **[!UICONTROL File Format]**:或 **[!UICONTROL CSV]** 者 **[!UICONTROL TAB_DELIMITED]**。 選擇要導出到儲存位置的檔案格式。
   ![Salesforce基本資訊](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. 填寫 **[!UICONTROL Create destination]** 上述欄位後按一下。 您的目標現在已連線，您可 [以啟動區段](/help/rtcdp/destinations/activate-destinations.md) 至目標。

## 目標屬性 {#destination-attributes}

在啟 [動區段](/help/rtcdp/destinations/activate-destinations.md) 至Salesforce Marketing Cloud目標時，我們建議您從聯合架構中選取唯 [一識別碼](../../profile/home.md#profile-fragments-and-union-schemas)。 選擇唯一標識符以及要導出到目標的任何其它XDM欄位。 如需詳細資訊，請參 [閱「電子郵件行銷目標」中，選取要在匯出檔案中當做目標屬性使用的架構欄位](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。

## 設定資料匯入至Salesforce Marketing Cloud {#import-data-into-salesforce}

在將即時CDP連接至您的Amazon S3或SFTP儲存空間後，您必須將資料從儲存位置匯入Salesforce Marketing Cloud。 如要瞭解如何完成此作業，請 [參閱Salesforce說明中心的「從檔案將訂閱者匯入Marketing Cloud](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) 」。