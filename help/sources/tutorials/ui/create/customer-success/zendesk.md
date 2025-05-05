---
title: 在使用者介面中建立Zendesk Source連線
description: 瞭解如何使用Adobe Experience Platform UI建立Zendesk來源連線。
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 7%

---

# 在使用者介面中建立[!DNL Zendesk]來源連線

本教學課程提供使用Adobe Experience Platform使用者介面建立[!DNL Zendesk]來源連線的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

### 收集必要的認證

若要在Experience Platform上存取您的[!DNL Zendesk]帳戶，您必須提供下列認證的值：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| 子網域 | 您在註冊過程中所建立帳戶的特定唯一網域。 | `yoursubdomain` |
| 存取權杖 | Zendesk API權杖。 | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

如需驗證[!DNL Zendesk]來源的詳細資訊，請參閱[[!DNL Zendesk] 來源概觀](../../../../connectors/customer-success/zendesk.md)。

![Zendesk API權杖](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### 為[!DNL Zendesk]建立Experience Platform結構描述

在建立[!DNL Zendesk]來源連線之前，您也必須先建立Experience Platform結構描述以用於您的來源。 如需如何建立結構描述的完整步驟，請參閱有關[建立Experience Platform結構描述](../../../../../xdm/schema/composition.md)的教學課程。

有關[!DNL Zendesk Search API]所需的[!DNL Zendesk]結構描述的其他指引，請參閱以下[限制](#limits)區段。

![建立結構描述](../../../../images/tutorials/create/zendesk/schema.png)

## 連線您的[!DNL Zendesk]帳戶

在Experience Platform UI中，從左側導覽列選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;*客戶成功*&#x200B;類別下，選取&#x200B;**[!UICONTROL Zendesk]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![目錄](../../../../images/tutorials/create/zendesk/catalog.png)

**[!UICONTROL Connect Zendesk帳戶]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取您要用來建立新資料流的&#x200B;*Zendesk*&#x200B;帳戶，然後選取[下一步]&#x200B;**以繼續。**

![現有](../../../../images/tutorials/create/zendesk/existing.png)

### 新帳戶

如果您正在建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明和您的認證。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![新](../../../../images/tutorials/create/zendesk/new.png)

### 選取資料

來源通過驗證後，頁面會更新為互動式結構描述樹狀結構，讓您探索和檢查資料的階層。 選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

![select-data](../../../../images/tutorials/create/zendesk/select-data.png)

## 後續步驟

依照本教學課程，您已驗證並建立[!DNL Zendesk]帳戶與Experience Platform之間的來源連線。 您現在可以繼續進行下一個教學課程，並[建立資料流以將客戶成功資料帶入Experience Platform](../../dataflow/customer-success.md)。

## 其他資源

以下各節提供在使用[!DNL Zendesk]來源時可以參考的其他資源。

### 驗證 {#validation}

以下概述您可以採取的步驟，以驗證您是否已成功連線您的[!DNL Zendesk]來源，以及是否正在將[!DNL Zendesk]設定檔擷取到Experience Platform。

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 資料集]**&#x200B;以存取[!UICONTROL 資料集]工作區。 [!UICONTROL 資料集活動]畫面會顯示執行的詳細資訊。

![活動頁面](../../../../images/tutorials/create/zendesk/dataset-activity.png)

接著，選取您要檢視之資料流程的資料流程執行ID，以檢視有關該資料流程執行的特定詳細資訊。

![資料流頁面](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

最後，選取&#x200B;**[!UICONTROL 預覽資料集]**&#x200B;以顯示所擷取的資料。

![Zendesk資料集](../../../../images/tutorials/create/zendesk/preview-dataset.png)

您也可以根據[!DNL Zendesk] > [!DNL Customers]頁面上的資料來驗證您的Experience Platform資料。

![zendesk-customers](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Zendesk結構描述

下表列出必須為Zendesk設定的支援對應。

>[!TIP]
>
>如需有關API的詳細資訊，請參閱[Zendesk Search API >匯出搜尋結果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results)。

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

{style="table-layout:auto"}

### 限制 {#limits}

* [Zendesk搜尋API >匯出搜尋結果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results)每頁最多傳回1000筆記錄。
   * ``filter[type]``引數的值設為``user``，因此Zendesk連線只會傳回使用者。
   * 每頁的結果數由``page[size]``引數管理。 值設定為``100``。 這麼做是為了減少Zendesk所設定的減速限制的影響。
   * 請參閱[限制](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits)和[分頁](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1)。
   * 您也可以參考[使用游標分頁來分頁清單](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/)。
