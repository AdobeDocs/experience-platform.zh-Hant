---
title: 使用UI將Demandbase意圖連線至Experience Platform
description: 瞭解如何將Demandbase意圖連結至Experience Platform
hide: true
hidefromtoc: true
exl-id: 7dc87067-cdf6-4dde-b077-19666dcb12e2
source-git-commit: 911aad600dd2618ba98d2ccee737aaedea4f2735
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 36%

---

# 使用UI連線[!DNL Demandbase Intent]至Experience Platform

閱讀本指南，瞭解如何使用使用者介面將您的[!DNL Demandbase Intent]帳戶連結至Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md)： Real-Time CDP B2B edition是專為以B2B服務模式運作的行銷人員所打造。 它將來自多個來源的資料集中在一起，並將其合併成包含人員和帳戶輪廓的單一檢視。這種統一的資料讓行銷人員可以精確地以特定客群為目標，並在所有可用的管道中和這些客群互動。
* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 瀏覽來源目錄 {#navigate}

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;*[!UICONTROL B2B]*&#x200B;類別下選取&#x200B;**[!DNL Demandbase Intent]**，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 一旦驗證帳戶存在，此選項就會變更為&#x200B;**[!UICONTROL 新增資料]**。



## 使用現有帳戶 {#existing}

## 建立新帳戶 {#create}

## 提供資料流詳細資訊 {#provide-dataflow-details}

>[!CONTEXTUALHELP]
>id="platform_sources_demandbase_domain"
>title="網域來源"
>abstract="雖然 Adobe 使用 XDM accountOrganization.website，但可能有客戶在其個別網站上使用自訂欄位。因此，您必須確保網域來源為會將您的 Demandbase 帳戶記錄與 Experience Platform 帳戶進行比對的網域/網站欄位。"

## 排程資料流 {#schedule-dataflow}

>[!CONTEXTUALHELP]
>id="platform_sources_demandbase_schedule"
>title="排程您的資料流"
>abstract="Demandbase 每週一早上 (UTC 時間下午 5:00) 卸除資料。因此，您必須將攝取開始時間設定為 UTC 時間下午 5:00 之後。此外，您必須與 Demandbase 確認攝取時間，因為他們可能會在將檔案卸除至 Adobe 時變更其排程。"

## 檢閱資料流 {#review-dataflow}
