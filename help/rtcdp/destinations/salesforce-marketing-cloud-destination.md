---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud是數位行銷套裝，先前稱為ExactTarget，可讓您為訪客和客戶建構並自訂歷程，以個人化其體驗。
seo-description: Salesforce Marketing Cloud是數位行銷套裝，先前稱為ExactTarget，可讓您為訪客和客戶建構並自訂歷程，以個人化其體驗。
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Salesforce Marketing Cloud

## 概述

[Salesforce Marketing Cloud是數位行銷套件](https://www.salesforce.com/products/marketing-cloud/email-marketing/) ，之前稱為ExactTarget，可讓您為訪客和客戶建構並自訂歷程，以個人化其體驗。

若要傳送區段資料至Salesforce Marketing Cloud，您必須先在 [Adobe Real-time CDP中連接目標](#connect-destination) ，然後從您的儲存位置 [將資料匯入](#import-data-into-salesforce) Salesforce Marketing Cloud。

## 連接目標 {#connect-destination}

1. 在中 **[!UICONTROL Connections > Destinations]**，選取「Salesforce Marketing Cloud」，然後選取 **[!UICONTROL Connect destination]**。

   ![連線至Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. 在連接目標嚮導中，選擇 **[!UICONTROL Connection type]** 儲存位置。 對於Salesforce Marketing Cloud，您可以在 **SFTP與Password** , **SFTP與SSH金鑰之間選擇**。 根據您的連線類型，填寫下列資訊，然後選取 **[!UICONTROL Connect]**。

   ![設定Salesforce精靈](/help/rtcdp/destinations/assets/salesforce-step1.png)

   對於 **具有密碼連接的SFTP** ，必須提供域、埠、用戶名和密碼。
對於 **具有SSH密鑰連接的SFTP** ，必須提供域、埠、用戶名和SSH密鑰。

   ![填寫Salesforce資訊](/help/rtcdp/destinations/assets/salesforce-wizard.png)

1. 在基 **本資訊**，填寫您目的地的相關資訊，如下所示：
   * **名稱**:為目的地選擇相關名稱。
   * **說明**:輸入目標的說明。
   * **資料夾路徑**:在儲存位置中提供路徑，即時CDP會將導出資料儲存為CSV或Tab分隔檔案。
   * **檔案格式**: **CSV****或TAB_DELIMITED**。 選擇要導出到儲存位置的檔案格式。
   ![Salesforce基本資訊](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. 填寫 **基本** 「資訊」欄位後，按一 **下建立**。 您的目標現在已連線，您可 [以啟動區段](/help/rtcdp/destinations/activate-destinations.md) 至目標。

## 目標屬性 {#destination-attributes}

在啟 [動區段](/help/rtcdp/destinations/activate-destinations.md) 至Salesforce Marketing Cloud目標時，我們建議您從聯合架構中選取唯 [一識別碼](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)。 選擇唯一標識符和要導出到目標的任何其他XDM欄位。 如需詳細資訊，請參 [閱「電子郵件行銷目標」中，選取要在匯出檔案中當做目標屬性使用的架構欄位](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。

## 設定資料匯入至Salesforce Marketing Cloud {#import-data-into-salesforce}

在將即時CDP連接至您的Amazon S3或SFTP儲存空間後，您必須將資料從儲存位置匯入Salesforce Marketing Cloud。 如要瞭解如何完成此作業，請 [參閱Salesforce說明中心的「從檔案將訂閱者匯入Marketing Cloud](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) 」。