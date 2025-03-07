---
title: 使用UI連線Bombora Intent至Experience Platform
description: 瞭解如何將Bombora Intent連結至Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 81a615b9826ed69bb050cae9c074a4e457ba128a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 11%

---

# 使用UI連線[!DNL Bombora Intent]至Experience Platform

閱讀本指南，瞭解如何使用使用者介面將您的[!DNL Bombora Intent]帳戶連結至Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md)： Real-Time CDP B2B edition是專為以B2B服務模式運作的行銷人員所打造。 它將來自多個來源的資料集中在一起，並將其合併成包含人員和帳戶輪廓的單一檢視。這種統一的資料讓行銷人員可以精確地以特定客群為目標，並在所有可用的管道中和這些客群互動。
* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 瀏覽來源目錄

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;*[!UICONTROL B2B]*&#x200B;類別下選取&#x200B;**[!DNL Bombora Intent]**，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 一旦驗證帳戶存在，此選項就會變更為&#x200B;**[!UICONTROL 新增資料]**。



## 使用現有帳戶 {#existing}

## 建立新帳戶 {#create}

## 提供資料流詳細資料 {#provide-dataflow-details}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_domain"
>title="網域來源"
>abstract="雖然Adobe使用XDM accountOrganization.website，但可能有客戶針對個別網站使用自訂欄位。 因此，您必須確定您的網域來源是網域/網站欄位，此欄位會將您的Bombra帳戶記錄與Experience Platform帳戶相符。"

## 排程資料流 {#schedule-dataflow}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_schedule"
>title="排程您的資料流"
>abstract="Bombora每週於週一早上5:00 UTC捨棄資料一次。 因此，您必須在UTC下午5:00之後設定擷取開始時間。 此外，您必須向Bombora確認擷取時間，因為在將檔案拖放至Adobe時，他們可能會變更排程。"


## 檢閱資料流 {#review-dataflow}
