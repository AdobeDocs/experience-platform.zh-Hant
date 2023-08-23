---
title: 在UI中建立SugarCRM帳戶和聯絡人來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立SugarCRM帳戶與聯絡人來源連線。
exl-id: 45840d7e-4c19-4720-8629-be446347862d
source-git-commit: 0de4b32ac2ddc90dabefd469b6658388a4532e0d
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 2%

---

# 建立 [!DNL SugarCRM Accounts & Contacts] ui中的來源連線

本教學課程提供建立 [!DNL SugarCRM Accounts & Contacts] 使用Adobe Experience Platform使用者介面的來源連線。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。

如果您已有有效的 [!DNL SugarCRM] 帳戶，您可以略過本檔案的其餘部分，並前往上的教學課程 [設定資料流](../../dataflow/crm.md).

### 收集必要的認證

為了連線 [!DNL SugarCRM Accounts & Contacts] 至Platform，您必須提供下列連線屬性的值：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| `Host` | 來源連線到的SugarCRM API端點。 | `developer.salesfusion.com` |
| `Username` | 您的SugarCRM開發人員帳戶使用者名稱。 | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | 您的SugarCRM開發人員帳戶密碼。 | `123456789` |

### 建立Platform結構描述

建立之前 [!DNL SugarCRM] 來源連線中，您必須先建立用於來源的Platform結構。 請參閱上的教學課程 [建立平台結構描述](../../../../../xdm/schema/composition.md) 以取得如何建立綱要的完整步驟。

此 [!DNL SugarCRM Accounts & Contacts] 支援多個API。 這表示您必須根據要運用的物件型別，建立個別綱要。 請參閱下列帳戶和連絡人結構描述的範例：

>[!BEGINTABS]

>[!TAB 帳戶]

![顯示帳戶範例結構描述的平台UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-accounts.png)

>[!TAB 連絡人]

![顯示連絡人範例結構描述的Platform UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-contacts.png)

>[!ENDTABS]

## 連線您的 [!DNL SugarCRM Accounts & Contacts] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示各種來源，供您建立帳戶。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在 *CRM* 類別，選取 **[!UICONTROL SugarCRM帳戶與連絡人]**，然後選取 **[!UICONTROL 新增資料]**.

![使用SugarCRM帳戶與聯絡人卡片目錄的Platform UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/catalog-sugarcrm-accounts-contacts.png)

此 **[!UICONTROL 連線SugarCRM帳戶與聯絡人帳戶]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL SugarCRM Accounts & Contacts] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![使用現有帳戶連線SugarCRM帳戶與聯絡人帳戶的Platform UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明和您的認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![使用新帳戶連線SugarCRM帳戶與聯絡人帳戶的Platform UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/new.png)

### 選擇資料

最後，您必須選取要擷取至Platform的物件型別。

| 物件型別 | 說明 |
| --- | --- |
| `Accounts` | 與貴組織有關係的公司。 |
| `Contacts` | 與您的組織建立關係的個人。 |

>[!BEGINTABS]

>[!TAB 帳戶]

![顯示已選取帳戶選項之設定的SugarCRM帳戶與聯絡人平台UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-accounts.png)

>[!TAB 連絡人]

![顯示已選取連絡人選項之設定的SugarCRM帳戶與連絡人平台UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-contacts.png)

>[!ENDTABS]

## 後續步驟

依照本教學課程中的指示，您已建立與的連線， [!DNL SugarCRM Accounts & Contacts] 帳戶。 您現在可以繼續進行下一個教學課程及 [設定資料流以將資料匯入Platform](../../dataflow/crm.md).

## 其他資源

以下各節提供您在使用時，可參考的其他資源 [!DNL SugarCRM] 來源。

### 護欄 {#guardrails}

此 [!DNL SugarCRM] API節流速率是每分鐘90次呼叫或每天2000次呼叫，以先發生者為準。 不過，將引數新增至連線規格已避免此限制，這會延遲要求時間，使速率限制永遠無法達到。

### 驗證 {#validation}

驗證您是否已正確設定來源及 [!DNL SugarCRM Accounts & Contacts] 正在擷取資料，請遵循下列步驟：

* 在Platform UI中選取 **[!UICONTROL 檢視資料流]** 在 [!DNL SugarCRM Accounts & Contacts] 來源目錄上的卡片功能表。 接下來，選取 **[!UICONTROL 預覽資料集]** 以驗證所擷取的資料。

* 根據您使用的物件型別，您可以根據 [!DNL SugarMarket] 以下的帳戶或連絡人頁面：

>[!BEGINTABS]

>[!TAB 帳戶]

![SugarMarket帳戶頁面的熒幕擷圖顯示帳戶清單](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-accounts.png)

>[!TAB 連絡人]

![SugarMarket連絡人頁面顯示連絡人清單的熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-contacts.png)

>[!ENDTABS]

>[!NOTE]
>
>此 [!DNL SugarMarket] 頁面不包含已刪除的物件計數。 不過，透過此來源擷取的資料也會包含已刪除的計數，這些將會標示已刪除的旗標。
