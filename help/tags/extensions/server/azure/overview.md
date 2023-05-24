---
title: MicrosoftAzure擴展概述
description: 瞭解MicrosoftAzure擴展，以在Adobe Experience Platform轉發事件。
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 3%

---

# [!DNL Microsoft Azure] 擴展概述

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

在 [!DNL Microsoft Azure]。 [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) 是一種高度可擴展的即時資料入口服務，允許您處理和分析您所連接的設備和應用程式所產生的海量資料。 一旦資料被收集到事件中心，就可以使用任何即時分析提供程式或批處理/儲存適配器來轉換和儲存資料。

的 [!DNL Microsoft Azure] [事件轉發](../../../ui/event-forwarding/overview.md) 擴展 [!DNL Event Hubs] 將事件從Adobe Experience Platform邊緣網路發送到 [!DNL Azure] 進行進一步處理。 本指南介紹如何安裝擴展並在事件轉發規則中使用其功能。

## 先決條件

要使用此副檔名，您必須具有 [!DNL Azure] 有權訪問的帳戶 [!DNL Event Hubs]。 您還必須 [使用 [!DNL Azure] 門戶](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) 執行以下步驟之前。

## 安裝擴展

安裝Microsoft [!DNL Azure] 擴展，導航到資料收集UI或Experience PlatformUI並選擇 **[!UICONTROL 事件轉發]** 的上界。 在此處，選擇要向其添加副檔名的屬性，或改為建立新屬性。

選擇或建立所需屬性後，選擇 **[!UICONTROL 擴展]** 在左側導航中，選擇 **[!UICONTROL 目錄]** 頁籤。 搜索 [!UICONTROL MicrosoftAzure] 卡，然後選擇 **[!UICONTROL 安裝]**。

![的 [!UICONTROL 安裝] 按鈕 [!UICONTROL MicrosoftAzure] 資料收集UI中的擴展。](../../../images/extensions/server/azure/install.png)

由於擴展沒有任何配置屬性，因此它會立即添加到已安裝的擴展清單中。 現在可以開始使用 [!DNL Event Hub] 配置事件轉發規則時的操作類型。

## 配置事件轉發規則 {#rule}

開始建立新事件轉發規則並根據需要配置其條件。 為規則選擇操作時，選擇 **[!UICONTROL MicrosoftAzure]** ，然後選擇 **[!UICONTROL 將資料發送到事件中心]** 按鈕。

![的 [!UICONTROL 將資料發送到事件中心] 正在為資料收集UI中的規則選擇操作類型。](../../../images/extensions/server/azure/select-action-type.png)

右面板將更新，以顯示應如何發送資料的配置選項。 具體來說，您必須 [資料元素](../../../ui/managing-resources/data-elements.md) 到代表您 [!DNL Event Hub] 配置。

![的配置選項 [!UICONTROL 將資料發送到事件中心] UI中顯示的操作類型。](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL 事件中心詳細資訊]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 命名空間] | 名稱 [!DNL Event Hubs] 建立的命名空間 [設定事件中心](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)。 |
| [!UICONTROL 名稱] | 事件中心的名稱。 |
| [!UICONTROL SAS授權規則名稱] | 整個共用訪問授權規則的名稱 [!DNL Event Hubs] 命名空間或要向其發送資料的特定事件中心實例。 請參閱附錄部分， [獲取SAS授權值](#sas) 的子菜單。 |
| [!UICONTROL SAS訪問密鑰] | 整個共用訪問授權規則的主鍵 [!DNL Event Hubs] 命名空間或要向其發送資料的特定事件中心實例。 請參閱附錄部分， [獲取SAS授權值](#sas) 的子菜單。 |
| [!UICONTROL 分區ID] | [!DNL Event Hubs] 允許您 [將事件直接發送到特定分區](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka)。 要利用此功能，請提供要接收事件的分區的ID。 |

{style="table-layout:auto"}

**資料**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 負載] | 此欄位包含將轉發到 [!DNL Event Hubs]。 資料可以是JSON對象、字串或資料元素。 |

{style="table-layout:auto"}

完成後，選擇 **[!UICONTROL 保留更改]** 將操作添加到規則配置。 對規則滿意後，選擇 **[!UICONTROL 保存到庫]**。

最後，發佈新事件轉發 [構建](../../../ui/publishing/builds.md) 以啟用對庫的更改。

## 後續步驟

本指南介紹了如何將資料發送到 [!DNL Event Hubs] 使用 [!DNL Microsoft Azure] 事件轉發擴展。 有關Experience Platform中事件轉發功能的詳細資訊，請參閱 [事件轉發概述](../../../ui/event-forwarding/overview.md)。

## 附錄：獲取SAS授權值 {#sas}

授予外部應用程式訪問權限 [!DNL Event Hubs] 通 [共用訪問簽名(SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature)。 每個 [!DNL Event Hubs] 命名空間和事件中心實例在建立時具有自動分配的預設SAS授權規則，但是，如果需要，您也可以為每個資源建立其他策略。

當 [配置事件轉發規則](#rule) 使用 [!DNL Azure] 擴展，必須為管理要向其發送資料的命名空間或特定事件中心的授權規則提供名稱和主鍵。 有關如何從 [!DNL Azure] portal，請參閱 [!DNL Azure] 文檔：

* [獲取SAS值 [!DNL Event Hubs] 命名空間](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [獲取命名空間中特定事件集線器的SAS值](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

一旦具有所需值，則可以直接在配置輸入中將授權規則名稱作為字串提供，也可以建立字串類型資料元素來引用它。 但是，在規則配置中提供主密鑰之前，必須先將其包含在事件轉發機密中，以保護資料安全。

在事件轉發UI中， [建立新秘密](../../../ui/event-forwarding/secrets.md) 選擇 **[!UICONTROL 令牌]** 作為機密類型。 對於令牌值本身，請提供先前複製的主鍵。 建立機密後，建立具有該類型的資料元素 **[!UICONTROL 秘密]** 的 [!DNL Event Hubs] 名單上的秘密。 一旦設定了機密資料元素，您就可以在 **[!UICONTROL SAS訪問密鑰]** 的子菜單。
