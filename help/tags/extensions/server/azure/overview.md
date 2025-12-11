---
title: Microsoft Azure擴充功能概觀
description: 瞭解Adobe Experience Platform中用於事件轉送的Microsoft Azure擴充功能。
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# [!DNL Microsoft Azure]擴充功能概觀

在[!DNL Microsoft Azure]中，[[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview)是高度可擴充的即時資料匯入服務，可讓您處理和分析連線的裝置和應用程式所產生的大量資料。 資料收集到事件中樞後，即可使用任何即時分析提供者或批次/儲存配接卡進行轉換和儲存。

[!DNL Microsoft Azure] [事件轉送](../../../ui/event-forwarding/overview.md)擴充功能運用[!DNL Event Hubs]將事件從Adobe Experience Platform Edge Network傳送至[!DNL Azure]以進行進一步處理。 本指南說明如何安裝擴充功能，以及在事件轉送規則中運用其功能。

## 先決條件

若要使用此擴充功能，您必須擁有可存取[!DNL Azure]的有效[!DNL Event Hubs]帳戶。 在執行以下步驟之前，您也必須使用[入口網站 [!DNL Azure] 來](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create)建立事件中樞。

## 安裝擴充功能

若要安裝Microsoft [!DNL Azure]擴充功能，請導覽至資料收集UI或Experience Platform UI，然後從左側導覽中選取&#x200B;**[!UICONTROL Event Forwarding]**。 從這裡，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需的屬性後，在左側導覽中選取「**[!UICONTROL Extensions]**」，然後選取「**[!UICONTROL Catalog]**」標籤。 搜尋[!UICONTROL Microsoft Azure]卡片，然後選取&#x200B;**[!UICONTROL Install]**。

![正在資料收集UI中為[!UICONTROL Install]擴充功能選取[!UICONTROL Microsoft Azure]按鈕。](../../../images/extensions/server/azure/install.png)

由於擴充功能沒有任何設定屬性，因此會立即將其新增至已安裝的擴充功能清單中。 您現在可以在設定事件轉送規則時開始使用[!DNL Event Hub]動作型別。

## 設定事件轉送規則 {#rule}

開始建立新的事件轉送規則，並視需要設定其條件。 選取規則的動作時，請選取擴充功能的&#x200B;**[!UICONTROL Microsoft Azure]**，然後選取動作型別的&#x200B;**[!UICONTROL Send Data to Event Hubs]**。

![正在資料收集UI中為規則選取的[!UICONTROL Send Data to Event Hubs]動作型別。](../../../images/extensions/server/azure/select-action-type.png)

右側面板會更新，以顯示資料傳送方式的設定選項。 具體來說，您必須將[資料元素](../../../ui/managing-resources/data-elements.md)指派給代表您[!DNL Event Hub]組態的各種屬性。

![在UI中顯示的[!UICONTROL Send Data to Event Hubs]動作型別的組態選項。](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Event Hub Details]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL Namespace] | 您在[!DNL Event Hubs]設定事件中心[時所建立的](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)名稱空間名稱。 |
| [!UICONTROL Name] | 事件中樞的名稱。 |
| [!UICONTROL SAS Authorization Rule Name] | 您整個[!DNL Event Hubs]名稱空間或您要傳送資料的特定事件中樞執行個體的共用存取授權規則名稱。 如需詳細資訊，請參閱[取得SAS授權值](#sas)的附錄一節。 |
| [!UICONTROL SAS Access Key] | 您整個[!DNL Event Hubs]名稱空間或您要傳送資料的特定事件中樞執行個體的共用存取授權規則主索引鍵。 如需詳細資訊，請參閱[取得SAS授權值](#sas)的附錄一節。 |
| [!UICONTROL Partition ID] | [!DNL Event Hubs]可讓您[將事件直接傳送給特定分割區](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka)。 若要使用此功能，請提供您要接收事件的分割識別碼。 |

{style="table-layout:auto"}

**資料**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL Payload] | 此欄位包含將轉送至[!DNL Event Hubs]的資料。 資料可以是JSON物件、字串或資料元素。 |

{style="table-layout:auto"}

完成後，選取&#x200B;**[!UICONTROL Keep Changes]**&#x200B;將動作新增至規則設定。 當您對規則感到滿意時，請選取&#x200B;**[!UICONTROL Save to Library]**。

最後，發佈新的事件轉送[組建](../../../ui/publishing/builds.md)，以啟用程式庫的變更。

## 後續步驟

本指南說明如何使用[!DNL Event Hubs]事件轉送擴充功能將資料傳送至[!DNL Microsoft Azure]。 如需Experience Platform中事件轉送功能的詳細資訊，請參閱[事件轉送概觀](../../../ui/event-forwarding/overview.md)。

## 附錄：取得SAS授權值 {#sas}

外部應用程式已透過[!DNL Event Hubs]共用存取簽章(SAS)[被授與](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature)的存取權。 每個[!DNL Event Hubs]名稱空間和事件中心執行個體在建立時自動指派預設SAS授權規則，但如有需要，您也可以為每個資源建立其他原則。

使用[擴充功能](#rule)設定事件轉送規則[!DNL Azure]時，您必須提供管理您要傳送資料的名稱空間或特定事件中樞之授權規則的名稱和主索引鍵。 如需有關如何從[!DNL Azure]入口網站取得這些值的詳細資訊，請參閱[!DNL Azure]檔案中的下列章節：

* [取得 [!DNL Event Hubs] 名稱空間的SAS值](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [取得名稱空間](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)中特定事件中樞的SAS值

當您擁有必要的值後，授權規則名稱可以直接提供為設定輸入中的字串，或者您可以建立字串型別資料元素來參照它。 然而，主要金鑰必須先包含在事件轉送密碼中，才能在規則設定中提供該金鑰，以保護您的資料安全性。

在事件轉送UI中，[建立新密碼](../../../ui/event-forwarding/secrets.md)並選取&#x200B;**[!UICONTROL Token]**&#x200B;作為密碼型別。 針對權杖值本身，提供您先前複製的主要金鑰。 建立密碼之後，請建立型別為&#x200B;**[!UICONTROL Secret]**&#x200B;的資料元素，並從清單中選取[!DNL Event Hubs]密碼。 設定機密資料元素後，您可以在&#x200B;**[!UICONTROL SAS Access Key]**&#x200B;欄位中參考該資料元素。
