---
title: 在UI中建立SugarCRM帳戶與連絡人來源連線
description: 了解如何使用Adobe Experience Platform UI建立SugarCRM帳戶與連絡人來源連線。
source-git-commit: d4b5c3b897371eea591925d071afc120a3f246d7
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# （測試版）建立 [!DNL SugarCRM Accounts & Contacts] UI中的源連接

>[!NOTE]
>
>此 [!DNL SugarCRM Accounts & Contacts] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

本教學課程提供建立 [!DNL SugarCRM Accounts & Contacts] 源連接(使用Adobe Experience Platform用戶介面)。

## 快速入門

本教學課程需要妥善了解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效 [!DNL SugarCRM] 帳戶，您可以略過本檔案的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/crm.md).

### 收集所需憑據

為了連接 [!DNL SugarCRM Accounts & Contacts] 若要使用Platform，您必須提供下列連線屬性的值：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `Host` | 源連接的SugarCRM API端點。 | `developer.salesfusion.com` |
| `Username` | 您的SugarCRM開發人員帳戶使用者名稱。 | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | 您的SugarCRM開發人員帳戶密碼。 | `123456789` |

### 建立平台結構

建立之前 [!DNL SugarCRM] 源連接時，您還必須確保首先建立要用於源的平台架構。 請參閱 [建立平台結構](../../../../../xdm/schema/composition.md) 以取得如何建立結構的完整步驟。

此 [!DNL SugarCRM Accounts & Contacts] 支援多個API。 這表示您必鬚根據您運用的物件類型，建立個別的結構。 請參閱下列帳戶和連絡人結構範例：

>[!BEGINTABS]

>[!TAB 帳戶]

![Platform UI螢幕擷取畫面，顯示帳戶的範例結構](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-accounts.png)

>[!TAB 聯繫人]

![Platform UI螢幕截圖，顯示Contacts的示例架構](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-contacts.png)

>[!ENDTABS]

## 連接您的 [!DNL SugarCRM Accounts & Contacts] 帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 *CRM* 類別，選擇 **[!UICONTROL SugarCRM帳戶和聯繫人]**，然後選取 **[!UICONTROL 新增資料]**.

![Platform UI螢幕截圖，顯示SugarCRM帳戶與聯繫人卡](../../../../images/tutorials/create/sugarcrm-accounts-contacts/catalog-sugarcrm-accounts-contacts.png)

此 **[!UICONTROL 連接SugarCRM帳戶和聯繫人帳戶]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL SugarCRM Accounts & Contacts] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![Platform UI螢幕截圖顯示現有帳戶的Connect SugarCRM帳戶與聯繫人帳戶](../../../../images/tutorials/create/sugarcrm-accounts-contacts/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選用說明和您的憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![使用新帳戶連接SugarCRM帳戶與聯繫人帳戶的平台UI螢幕截圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/new.png)

### 選擇資料

最後，您必須選取要擷取至Platform的物件類型。

| 物件類型 | 說明 |
| --- | --- |
| `Accounts` | 與您的組織有關係的公司。 |
| `Contacts` | 您的組織與其有既定關係的個人。 |

>[!BEGINTABS]

>[!TAB 帳戶]

![顯示已選取「帳戶」選項之設定的SugarCRM帳戶與連絡人UI螢幕擷取](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-accounts.png)

>[!TAB 聯繫人]

![顯示已選擇「聯繫人」選項的配置的SugarCRM帳戶和聯繫人的平台UI螢幕截圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-contacts.png)

>[!ENDTABS]

## 後續步驟

依照本教學課程，您已建立與 [!DNL SugarCRM Accounts & Contacts] 帳戶。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料導入Platform](../../dataflow/crm.md).

## 其他資源

以下各節提供您在使用 [!DNL SugarCRM] 來源。

### 護欄 {#guardrails}

此 [!DNL SugarCRM] API限制率為每分鐘90次呼叫，或每天2000次呼叫（以先發生者為準）。 但是，在連接規格中添加參數將延遲請求時間，從而永遠不會達到速率限制，這樣就可以繞過此限制。

### 驗證 {#validation}

驗證您已正確設定來源和 [!DNL SugarCRM Accounts & Contacts] 正在擷取資料，請遵循下列步驟：

* 在平台UI中，選取 **[!UICONTROL 查看資料流]** 旁邊 [!DNL SugarCRM Accounts & Contacts] 來源目錄上的卡片功能表。 下一步，選擇 **[!UICONTROL 預覽資料集]** 來驗證已擷取的資料。

* 根據您使用的物件類型，您可以根據 [!DNL SugarMarket] 帳戶或聯繫人頁面如下：

>[!BEGINTABS]

>[!TAB 帳戶]

![顯示帳戶清單的SugarMarket帳戶頁面螢幕截圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-accounts.png)

>[!TAB 聯繫人]

![顯示聯繫人清單的SugarMarket聯繫人頁面螢幕截圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-contacts.png)

>[!ENDTABS]

>[!NOTE]
>
>此 [!DNL SugarMarket] 頁面不包含已刪除的物件計數。 不過，透過此來源擷取的資料也會包含已刪除的計數，這些計數會以已刪除的標幟標示。