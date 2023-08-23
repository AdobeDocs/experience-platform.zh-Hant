---
title: 在UI中建立SugarCRM事件來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立SugarCRM事件來源連線。
exl-id: db346ec0-2c57-4b82-8a39-f15d4cd377d4
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 1%

---

# 建立 [!DNL SugarCRM Events] ui中的來源連線

本教學課程提供建立 [!DNL SugarCRM Events] 使用Adobe Experience Platform使用者介面的來源連線。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。

如果您已有有效的 [!DNL SugarCRM] 帳戶，您可以略過本檔案的其餘部分，並前往上的教學課程 [設定資料流](../../dataflow/crm.md).

### 收集必要的認證

為了連線 [!DNL SugarCRM Events] 至Platform，您必須提供下列連線屬性的值：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| `Host` | 來源連線到的SugarCRM API端點。 | `developer.salesfusion.com` |
| `Username` | 您的SugarCRM開發人員帳戶使用者名稱。 | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | 您的SugarCRM開發人員帳戶密碼。 | `123456789` |

### 建立Platform結構描述 [!DNL SugarCRM]

建立之前 [!DNL SugarCRM] 來源連線中，您必須先建立用於來源的Platform結構。 請參閱上的教學課程 [建立平台結構描述](../../../../../xdm/schema/composition.md) 以取得如何建立綱要的完整步驟。

![顯示SugarCRM事件結構描述範例的平台UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>對應結構時，請確定您也對應強制 `event_id` 和 `timestamp` Platform所需的欄位。

## 連線您的 [!DNL SugarCRM Events] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示各種來源，供您建立帳戶。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在 *CRM* 類別，選取 **[!UICONTROL SugarCRM事件]**，然後選取 **[!UICONTROL 新增資料]**.

![具有SugarCRM Events卡片之目錄的Platform UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

此 **[!UICONTROL 連線SugarCRM事件帳戶]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL SugarCRM Events] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![與現有帳戶連線SugarCRM事件帳戶的平台UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明和您的認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![使用新帳戶連線SugarCRM事件帳戶的Platform UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-events/new.png)

## 後續步驟

依照本教學課程中的指示，您已建立與的連線， [!DNL SugarCRM Events] 帳戶。 您現在可以繼續進行下一個教學課程及 [設定資料流以將資料匯入Platform](../../dataflow/crm.md).

## 其他資源

以下各節提供您在使用時，可參考的其他資源 [!DNL SugarCRM] 來源。

### 護欄 {#guardrails}

此 [!DNL SugarCRM] API節流速率是每分鐘90次呼叫或每天2000次呼叫，以先發生者為準。 不過，將引數新增至連線規格已避免此限制，這會延遲要求時間，使速率限制永遠無法達到。

### 驗證 {#validation}

驗證您是否已正確設定來源及 [!DNL SugarCRM Events] 正在擷取資料，請遵循下列步驟：

* 在Platform UI中選取 **[!UICONTROL 檢視資料流]** 在 [!DNL SugarCRM Events] 來源目錄上的卡片功能表。 接下來，選取 **[!UICONTROL 預覽資料集]** 以驗證所擷取的資料。

* 根據您使用的物件型別，您可以根據 [!DNL SugarMarket] 事件頁面如下：

![SugarMarket帳戶頁面的熒幕擷圖顯示帳戶清單](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>此 [!DNL SugarMarket] 頁面不包含已刪除的物件計數。 不過，透過此來源擷取的資料也會包含已刪除的計數，這些將會標示已刪除的旗標。
