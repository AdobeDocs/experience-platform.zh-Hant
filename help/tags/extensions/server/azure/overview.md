---
title: Microsoft Azure擴充功能概述
description: 了解Adobe Experience Platform中用於事件轉送的Microsoft Azure擴充功能。
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
source-git-commit: 8b972841c8412d510fce4c970a09d9c1eecd401e
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 4%

---

# [!DNL Microsoft Azure] 擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

在 [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) 是高度可擴展的即時資料入口服務，允許您處理和分析由連接的設備和應用程式生成的海量資料。 資料收集到事件中心後，即可使用任何即時分析提供者或批次處理/儲存轉接器來轉換和儲存資料。

此 [!DNL Microsoft Azure] [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能可運用 [!DNL Event Hubs] 從Adobe Experience Platform邊緣網路將事件傳送至 [!DNL Azure] 供進一步處理。 本指南說明如何安裝擴充功能，並在事件轉送規則中運用其功能。

## 先決條件

若要使用此擴充功能，您必須具備有效 [!DNL Azure] 有權存取的帳戶 [!DNL Event Hubs]. 您也必須 [使用 [!DNL Azure] 入口](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) 執行下列步驟之前。

## 安裝擴充功能

安裝Microsoft [!DNL Azure] 擴充功能，請導覽至資料收集UI或Experience PlatformUI，然後選取 **[!UICONTROL 事件轉送]** 從左側導覽。 從此處，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需屬性後，請選取 **[!UICONTROL 擴充功能]** 在左側導覽器中，選取 **[!UICONTROL 目錄]** 標籤。 搜尋 [!UICONTROL Microsoft Azure] 卡片，然後選取 **[!UICONTROL 安裝]**.

![此 [!UICONTROL 安裝] 按鈕 [!UICONTROL Microsoft Azure] 擴充功能。](../../../images/extensions/server/azure/install.png)

由於擴充功能沒有任何設定屬性，因此會立即將其新增至已安裝擴充功能的清單中。 您現在可以開始使用 [!DNL Event Hub] 設定事件轉送規則時的動作類型。

## 設定事件轉送規則 {#rule}

開始建立新的事件轉送規則，並視需要設定其條件。 選取規則的動作時，請選取 **[!UICONTROL Microsoft Azure]** 對於擴充功能，請選取 **[!UICONTROL 將資料發送到事件中心]** （針對動作類型）。

![此 [!UICONTROL 將資料發送到事件中心] 在資料收集UI中為規則選取的動作類型。](../../../images/extensions/server/azure/select-action-type.png)

右側面板會更新，顯示應如何傳送資料的設定選項。 具體來說，您必須指派 [資料元素](../../../ui/managing-resources/data-elements.md) 到代表您 [!DNL Event Hub] 設定。

![的設定選項 [!UICONTROL 將資料發送到事件中心] UI中顯示的動作類型。](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL 事件中心詳細資訊]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 命名空間] | 的名稱 [!DNL Event Hubs] 您在 [設定事件中心](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL 名稱] | 事件中心的名稱。 |
| [!UICONTROL SAS授權規則名稱] | 整個共用訪問授權規則的名稱 [!DNL Event Hubs] 命名空間或您要傳送資料的特定事件中樞例項。 請參閱附錄一節 [獲取SAS授權值](#sas) 以取得更多資訊。 |
| [!UICONTROL SAS訪問密鑰] | 共用訪問授權規則的主密鑰 [!DNL Event Hubs] 命名空間或您要傳送資料的特定事件中樞例項。 請參閱附錄一節 [獲取SAS授權值](#sas) 以取得更多資訊。 |
| [!UICONTROL 分區ID] | [!DNL Event Hubs] 可讓您 [將事件直接發送到特定分區](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). 要利用此功能，請提供要接收事件的分區的ID。 |

{style=&quot;table-layout:auto&quot;}

**資料**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 裝載] | 此欄位包含要轉送至 [!DNL Event Hubs]. 資料可以是JSON物件、字串或資料元素。 |

{style=&quot;table-layout:auto&quot;}

完成後，請選取 **[!UICONTROL 保留變更]** 將動作新增至規則設定。 對規則感到滿意時，請選取 **[!UICONTROL 儲存至程式庫]**.

最後，發佈新的事件轉送 [建置](../../../ui/publishing/builds.md) 啟用程式庫的變更。

## 後續步驟

本指南說明如何將資料傳送至 [!DNL Event Hubs] 使用 [!DNL Microsoft Azure] 事件轉送擴充功能。 如需Experience Platform中事件轉送功能的詳細資訊，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).

## 附錄：獲取SAS授權值 {#sas}

外部應用程式可訪問 [!DNL Event Hubs] through [共用訪問簽名(SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). 每個 [!DNL Event Hubs] 命名空間和事件中心實例在建立時自動分配了預設的SAS授權規則，但您也可以為每個資源建立其他策略（如果希望）。

當 [配置事件轉發規則](#rule) 使用 [!DNL Azure] 擴充功能時，您必須針對管理命名空間或您要傳送資料的特定事件中心的授權規則，提供名稱和主要金鑰。 如需如何從 [!DNL Azure] 入口網站，請參閱 [!DNL Azure] 檔案：

* [獲取 [!DNL Event Hubs] 命名空間](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [獲取命名空間中特定事件中心的SAS值](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

擁有所需值後，授權規則名稱可直接在設定輸入中以字串形式提供，或者您可以建立字串類型資料元素來參照。 但是，必須先將主要金鑰包含在事件轉送機密內，才能在規則設定中提供主要金鑰，以保護您的資料安全。

在事件轉送UI中， [建立新機密](../../../ui/event-forwarding/secrets.md) 選取 **[!UICONTROL 代號]** 作為機密類型。 對於代號值本身，請提供您先前複製的主索引鍵。 建立機密後，請建立包含類型的資料元素 **[!UICONTROL 機密]** ，然後選取 [!DNL Event Hubs] 清單中的機密。 設定機密資料元素後，即可在 **[!UICONTROL SAS訪問密鑰]** 欄位。
