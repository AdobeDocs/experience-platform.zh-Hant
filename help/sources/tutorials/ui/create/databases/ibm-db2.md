---
keywords: Experience Platform；首頁；熱門主題；DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: 在UI中建立IBM DB2源連接
type: Tutorial
description: 了解如何使用IBM UI建立Adobe Experience Platform DB2來源連線。
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# 在UI中建立IBM DB2來源連線

>[!NOTE]
>
> IBM DB2連接器為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供使用建立IBM DB2（以下稱為「DB2」）來源連接器的步驟 [!DNL Platform] 使用者介面。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已經擁有有效的DB2連接，則可以跳過本文檔的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/databases.md).

### 收集所需憑據

以下各節提供您需要了解的其他資訊，以便使用 [!DNL Flow Service] API。

| 憑據 | 說明 |
| ---------- | ----------- |
| `server` | DB2伺服器的名稱。 您可以在伺服器名稱后面指定連接埠號，該名稱由冒號分隔。 例如：伺服器：埠。 |
| `database` | DB2資料庫的名稱。 |
| `username` | 用於連接到DB2資料庫的用戶名。 |
| `password` | 您為用戶名指定的用戶帳戶的密碼。 |

如需快速入門的詳細資訊，請參閱 [此DB2文檔](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## 連接您的IBM DB2帳戶

收集到所需的憑據後，您可以按照以下步驟將DB2帳戶連結到 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽列存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以為其建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 **[!UICONTROL 資料庫]** 類別，選擇 **[!UICONTROL IBM DB2]**. 如果這是您第一次使用此連接器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 建立新DB2連接器。

![目錄](../../../../images/tutorials/create/ibm-db2/catalog.png)

此 **[!UICONTROL 連接到IBM DB2]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、可選說明和DB2憑據。 完成後，請選取 **[!UICONTROL Connect]** 然後讓新連接建立一段時間。

![connect](../../../../images/tutorials/create/ibm-db2/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的DB2帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/ibm-db2/existing.png)

## 後續步驟

按照本教程，您已建立了與DB2帳戶的連接。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md).
