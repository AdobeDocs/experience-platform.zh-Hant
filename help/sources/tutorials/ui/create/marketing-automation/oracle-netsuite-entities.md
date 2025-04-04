---
title: 在使用者介面中建立 [!DNL Oracle NetSuite Entities] 來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立Oracle NetSuite實體來源連線。
hide: true
hidefromtoc: true
badge: Beta
exl-id: ce0ea37f-16e0-4aef-9809-72c0b11e0440
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 2%

---

# 在使用者介面中建立[!DNL Oracle NetSuite Entities]來源連線

>[!NOTE]
>
>[!DNL Oracle NetSuite Entities]來源是測試版。 如需使用Beta版標示來源的相關資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

請閱讀下列教學課程，瞭解如何在UI中將聯絡人和客戶資料從您的[!DNL Oracle NetSuite Entities]帳戶帶到Adobe Experience Platform。

## 快速入門 {#getting-started}

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Oracle NetSuite]帳戶，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/marketing-automation.md)的教學課程。

>[!TIP]
>
>請閱讀[[!DNL Oracle NetSuite] 總覽](../../../../connectors/marketing-automation/oracle-netsuite.md)，瞭解如何擷取您的驗證認證的相關資訊。

## 連線您的[!DNL Oracle NetSuite Activities]帳戶 {#connect-account}

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;*行銷自動化*&#x200B;類別下，選取&#x200B;**[!DNL Oracle NetSuite Entities]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

使用Experience Platform NetSuite Entities卡片目錄的![Oracle UI熒幕擷圖](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/catalog-card.png)

**[!UICONTROL 連線Oracle NetSuite Entities帳戶]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

>[!IMPORTANT]
>
>重新整理Token會在七天後到期。 您的Token過期後，必須在Experience Platform上以更新後的Token建立帳戶。 如果您沒有使用更新的Token建立新帳戶，您可能會看到下列錯誤訊息： `The request could not be processed. Error from flow provider: The request could not be processed. Rest call failed with client error, status code 401 Unauthorized, please check your activity settings.`

### 現有帳戶 {#existing-account}

若要使用現有帳戶，請選取您要用來建立新資料流的[!DNL Oracle NetSuite Entities]帳戶，然後選取[下一步] ]**以繼續。**[!UICONTROL 

![Experience Platform UI熒幕擷圖可將Oracle NetSuite Entities帳戶與現有帳戶連線](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/existing.png)

### 新帳戶 {#new-account}

如果您正在建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明和您的認證。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![Experience Platform UI熒幕擷圖可將Oracle NetSuite Entities帳戶與新帳戶連線](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/new.png)

### 選取資料

接著，選取您要擷取至Experience Platform的物件型別。

| 實體型別 | 說明 |
| --- | --- |
| 聯絡 | 擷取聯絡人姓名、電子郵件、電話號碼，以及與客戶相關聯的任何自訂聯絡人相關欄位。 |
| 客戶 | 擷取特定客戶資料，包括客戶名稱、地址和關鍵識別碼等詳細資訊。 |

>[!BEGINTABS]

>[!TAB 連絡人]

![顯示已選取連絡人選項之組態的Oracle Netsuite實體Experience Platform UI熒幕擷取畫面](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/select-data-contact.png)

>[!TAB 客戶]

![Experience Platform Netsuite實體的Oracle UI熒幕擷取畫面，顯示已選取「客戶」選項的組態](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/select-data-customer.png)

>[!ENDTABS]

## 後續步驟 {#next-steps}

依照本教學課程中的指示，您已建立與[!DNL Oracle NetSuite Entities]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流，以將行銷自動化資料帶入Experience Platform](../../dataflow/marketing-automation.md)。

## 其他資源 {#additional-resources}

以下各節提供在使用[!DNL Oracle NetSuite Entities]來源時可以參考的其他資源。

### 對應 {#mapping}

Experience Platform會根據您選取的目標結構或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以根據自己的需求，選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算或計算的值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱[資料準備UI指南](../../../../../data-prep/ui/mapping.md)。

>[!NOTE]
>
>顯示的欄位取決於您的[!DNL Oracle NetSuite]帳戶有權存取的訂閱。 例如，如果您無權存取帳單，則看不到與帳單相關的欄位。

### 正在安排 {#scheduling}

排程[!DNL Oracle NetSuite Entities]資料流進行內嵌時，您必須選取下列頻率和間隔設定：

| 頻率 | 間隔 |
| --- | --- |
| `Once` | 1 |

擷取資料時，[!DNL Oracle NetSuite]會以日期格式（而非時間戳記）來回應上次修改或建立的日期。 因此，排程限製為一天。

提供排程的值之後，請選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的排程步驟。](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/scheduling.png)
