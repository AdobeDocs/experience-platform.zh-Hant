---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Microsoft Dynamics或Salesforce來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# 在UI中建立Microsoft Dynamics或Salesforce來源連接器

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的CRM資料。 本教學課程提供使用Platform使用者介面建立Microsoft Dynamics（以下稱為「Dynamics」）或Salesforce來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有Microsoft Dynamics或Salesforce基本連線，則可略過本檔案的其餘部分，並繼續有關設定資料流 [的教學課程](../../dataflow/crm.md)。

### 收集必要的認證

若要存取您的Dynamics平台帳戶，您必須提供服 **務URI**、使 **用者**&#x200B;和 **密碼**。

同樣地，在Platform上存取您的Salesforce帳戶需要您提供環 **境URL****使用者名稱**、密 **碼**，以及 ****&#x200B;安全Token。

## 連接您的Dynamics或Salesforce帳戶

在您的CRM系統認證就緒後，您可以依照下列步驟建立新的傳入基本連線，將您的Dynamics或Salesforce帳戶連結至平台。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選 **取Sources** ，以存取來源工作區。 「目 *錄* 」螢幕顯示各種源，您可以為其建立入站基本連接，而每個源顯示與其關聯的現有基本連接數。

在「 *CRM* 」類別下，選取 **Microsoft Dynamics** 或 **Salesforce** ，以顯示螢幕右側的資訊列。 資訊列提供所選來源的簡短說明，以及檢視其檔案或連線來源的選項。 要建立新的入站基本連接，請按一下「連 **接源」**。

![](../../../../images/tutorials/create/salesforce/sf_sources_catalog.png)

在輸入表單中，提供基本連線以及名稱、選用說明和您的Dynamics或Salesforce認證。 最後，按一下 **Connect** ，然後允許一些時間建立新的基本連接。

![](../../../../images/tutorials/create/salesforce/sf_credentials.png)

建立與CRM系統的基本連線後，您可以繼續下一節，並設定資料流，將CRM資料匯入平台。

## 後續步驟

在本教學課程中，您已建立Dynamics或Salesforce帳戶的基本連線。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/crm.md)。