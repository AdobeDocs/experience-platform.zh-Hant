---
title: 在UI中建立SugarCRM帳戶和聯繫人源連接
description: 瞭解如何使用Adobe Experience PlatformUI建立SugarCRM帳戶和聯繫人源連接。
exl-id: 45840d7e-4c19-4720-8629-be446347862d
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# (Beta)建立 [!DNL SugarCRM Accounts & Contacts] UI中的源連接

>[!NOTE]
>
>的 [!DNL SugarCRM Accounts & Contacts] 源為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

本教程提供建立 [!DNL SugarCRM Accounts & Contacts] 源連接，使用Adobe Experience Platform用戶介面。

## 快速入門

本教程需要對以下Experience Platform組成部分進行有效理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有 [!DNL SugarCRM] 帳戶，您可以跳過本文檔的其餘部分，繼續學習本教程。 [配置資料流](../../dataflow/crm.md)。

### 收集所需憑據

為了連接 [!DNL SugarCRM Accounts & Contacts] 到平台，必須提供以下連接屬性的值：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `Host` | 源連接到的SugarCRM API終結點。 | `developer.salesfusion.com` |
| `Username` | 您的SugarCRM開發人員帳戶用戶名。 | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | 您的SugarCRM開發人員帳戶密碼。 | `123456789` |

### 建立平台架構

在建立 [!DNL SugarCRM] 源連接，還必須確保首先建立用於源的平台架構。 請參閱上的教程 [建立平台架構](../../../../../xdm/schema/composition.md) 有關如何建立架構的全面步驟。

的 [!DNL SugarCRM Accounts & Contacts] 支援多個API。 這意味著您必鬚根據您正在利用的對象類型建立單獨的方案。 有關帳戶和聯繫人方案，請參閱以下示例：

>[!BEGINTABS]

>[!TAB 帳戶]

![顯示帳戶示例架構的平台UI螢幕快照](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-accounts.png)

>[!TAB 聯繫人]

![平台UI螢幕快照，顯示聯繫人示例架構](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-contacts.png)

>[!ENDTABS]

## 連接 [!DNL SugarCRM Accounts & Contacts] 帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左導航欄訪問 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 *CRM* 類別，選擇 **[!UICONTROL SugarCRM帳戶和聯繫人]**，然後選擇 **[!UICONTROL 添加資料]**。

![SugarCRM帳戶和聯繫人卡目錄的平台UI螢幕快照](../../../../images/tutorials/create/sugarcrm-accounts-contacts/catalog-sugarcrm-accounts-contacts.png)

的 **[!UICONTROL 連接SugarCRM帳戶和聯繫人帳戶]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要使用現有帳戶，請選擇 [!DNL SugarCRM Accounts & Contacts] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![將SugarCRM帳戶和聯繫人帳戶與現有帳戶連接的平台UI螢幕快照](../../../../images/tutorials/create/sugarcrm-accounts-contacts/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後提供名稱、可選說明和您的憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![將SugarCRM帳戶和聯繫人帳戶與新帳戶連接的平台UI螢幕快照](../../../../images/tutorials/create/sugarcrm-accounts-contacts/new.png)

### 選擇資料

最後，必須選擇要接收到平台的對象類型。

| 對象類型 | 說明 |
| --- | --- |
| `Accounts` | 您的組織與哪些公司有關係。 |
| `Contacts` | 您的組織與其有既定關係的個人人員。 |

>[!BEGINTABS]

>[!TAB 帳戶]

![顯示選定「帳戶」選項配置的SugarCRM帳戶和聯繫人的平台UI螢幕快照](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-accounts.png)

>[!TAB 聯繫人]

![顯示選定「聯繫人」選項配置的SugarCRM帳戶和聯繫人的平台UI螢幕快照](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-contacts.png)

>[!ENDTABS]

## 後續步驟

按照本教程，您已建立到 [!DNL SugarCRM Accounts & Contacts] 帳戶。 現在，您可以繼續下一個教程， [配置資料流以將資料引入平台](../../dataflow/crm.md)。

## 其他資源

以下各節提供了在使用 [!DNL SugarCRM] 源。

### 護欄 {#guardrails}

的 [!DNL SugarCRM] API限制速率為每分鐘90次或每天2000次（以最先發生的情況為準）。 但是，通過向連接規範中添加一個參數來繞過此限制，該參數將延遲請求時間，以便永遠不會達到速率限制。

### 驗證 {#validation}

驗證是否正確設定了源和 [!DNL SugarCRM Accounts & Contacts] 正在接收資料，請執行以下步驟：

* 在平台UI中，選擇 **[!UICONTROL 查看資料流]** 欄 [!DNL SugarCRM Accounts & Contacts] 源目錄上的卡菜單。 下一步，選擇 **[!UICONTROL 預覽資料集]** 驗證所攝入的資料。

* 根據您所使用的對象類型，您可以根據在 [!DNL SugarMarket] 以下帳戶或聯繫人頁面：

>[!BEGINTABS]

>[!TAB 帳戶]

![顯示帳戶清單的SugarMarket帳戶頁面螢幕截圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-accounts.png)

>[!TAB 聯繫人]

![顯示聯繫人清單的SugarMarket聯繫人頁面螢幕快照](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-contacts.png)

>[!ENDTABS]

>[!NOTE]
>
>的 [!DNL SugarMarket] 頁面不包括已刪除的對象計數。 但是，通過此源檢索到的資料也將包括已刪除的計數，這些資料將用已刪除的標籤標籤。
