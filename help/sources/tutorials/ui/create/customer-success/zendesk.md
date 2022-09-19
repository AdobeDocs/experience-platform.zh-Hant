---
keywords: Experience Platform;Zendesk；來源；連接器；來源連接器；來源sdk;sdk;SDK;Zendesk;Zendesk
title: 在UI中建立Zendesk源連接
description: 了解如何使用Adobe Experience Platform UI建立Zendesk來源連線。
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: 795c98fb555f79afd7a7035a23a9989cc734a1e1
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 6%

---

# （測試版）建立 [!DNL Zendesk] UI中的源連接

>[!NOTE]
>
>此 [!DNL Zendesk] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

本教學課程提供建立 [!DNL Zendesk] 源連接(使用Adobe Experience Platform用戶介面)。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

### 收集所需憑據

若要存取 [!DNL Zendesk] 帳戶，您必須提供下列憑證的值：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| 子網域 | 在註冊過程中建立的帳戶專屬的唯一網域。 | `yoursubdomain` |
| 存取權杖 | Zendesk API代號。 | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

如需驗證 [!DNL Zendesk] 來源，請參閱 [[!DNL Zendesk] 來源概觀](../../../../connectors/customer-success/zendesk.md).

![Zendesk API代號](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### 建立平台結構 [!DNL Zendesk]

建立之前 [!DNL Zendesk] 源連接時，您還必須確保首先建立要用於源的平台架構。 請參閱 [建立平台結構](../../../../../xdm/schema/composition.md) 以取得如何建立結構的完整步驟。

有關 [!DNL Zendesk] 需要的架構 [!DNL Zendesk Search API]，請參閱 [限制](#limits) 一節。

![建立結構](../../../../images/tutorials/create/zendesk/schema.png)

## 連接您的 [!DNL Zendesk] 帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 *客戶成功* 類別，選擇 **[!UICONTROL 曾代克]**，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/zendesk/catalog.png)

此 **[!UICONTROL Connect Zendesk帳戶]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要使用現有帳戶，請選取 *曾代克* 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/zendesk/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選用說明和您的憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![new](../../../../images/tutorials/create/zendesk/new.png)

### 選擇資料

驗證來源後，頁面會更新為互動式結構樹狀結構，讓您探索及檢查資料的階層。 選擇 **[!UICONTROL 下一個]** 繼續。

![select-data](../../../../images/tutorials/create/zendesk/select-data.png)

## 後續步驟

依照本教學課程，您已驗證並建立來源連線，連線位於 [!DNL Zendesk] 帳戶和平台。 您現在可以繼續下一個教學課程，以及 [建立資料流，將客戶成功資料匯入Platform](../../dataflow/customer-success.md).

## 其他資源

以下各節提供您在使用 [!DNL Zendesk] 來源。

### 驗證 {#validation}

以下概述驗證您已成功連線時可採取的步驟 [!DNL Zendesk] 來源 [!DNL Zendesk] 設定檔正在擷取至Platform。

在平台UI中，選取 **[!UICONTROL 資料集]** 從左側導覽器存取 [!UICONTROL 資料集] 工作區。 此 [!UICONTROL 資料集活動] 畫面會顯示執行的詳細資訊。

![活動頁面](../../../../images/tutorials/create/zendesk/dataset-activity.png)

接下來，選擇要查看的資料流的資料流運行ID，以查看該資料流運行的特定詳細資訊。

![「資料流」頁](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

最後，選取 **[!UICONTROL 預覽資料集]** 以顯示擷取的資料。

![Zendesk資料集](../../../../images/tutorials/create/zendesk/preview-dataset.png)

您也可以根據 [!DNL Zendesk] > [!DNL Customers] 頁面。

![zendesk客戶](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Zendesk架構

下表列出了必須為Zendesk設定的受支援映射。

>[!TIP]
>
>請參閱 [Zendesk Search API >導出搜索結果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) 以取得API的詳細資訊。

| 來源 | 類型 |
|---|---|
| `results.active` | 布林值 |
| `results.alias` | 字串 |
| `results.created_at` | 字串 |
| `results.custom_role_id` | 整數 |
| `results.default_group_id` | 整數 |
| `results.details` | 字串 |
| `results.email` | 字串 |
| `results.external_id` | 整數 |
| `results.iana_time_zone` | 字串 |
| `results.id` | 整數 |
| `results.last_login_at` | 字串 |
| `results.locale` | 字串 |
| `results.locale_id` | 整數 |
| `results.moderator` | 布林值 |
| `results.name` | 字串 |
| `results.notes` | 字串 |
| `results.only_private_comments` | 布林值 |
| `results.organization_id` | 整數 |
| `results.phone` | 字串 |
| `results.photo` | 字串 |
| `results.report_csv` | 布林值 |
| `results.restricted_agent` | 布林值 |
| `results.result_type` | 字串 |
| `results.role` | 字串 |
| `results.role_type` | 整數 |
| `results.shared` | 布林值 |
| `results.shared_agent` | 布林值 |
| `results.shared_phone_number` | 布林值 |
| `results.signature` | 字串 |
| `results.suspended` | 布林值 |
| `results.ticket_restriction` | 字串 |
| `results.time_zone` | 字串 |
| `results.two_factor_auth_enabled` | 布林值 |
| `results.updated_at` | 字串 |
| `results.url` | 字串 |
| `results.verified` | 布林值 |

{style=&quot;table-layout:auto&quot;}

### 限制 {#limits}

* 此 [Zendesk Search API >導出搜索結果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) 每頁最多傳回1000筆記錄。
   * 的值 ``filter[type]`` 參數設為 ``user`` 因此，Zendesk連接只返回用戶。
   * 每頁的結果數由 ``page[size]`` 參數。 值設為 ``100``. 這是為了減少Zendesk設定的減速約束的影響。
   * 請參閱 [限制](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits) 和 [分頁](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1).
   * 您也可以參閱 [使用游標分頁對清單進行分頁](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/).
