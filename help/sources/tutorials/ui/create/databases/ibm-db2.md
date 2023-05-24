---
keywords: Experience Platform；首頁；熱門主題；DB2;db2;IBMDB2;ibm db2
solution: Experience Platform
title: 在UI中建立IBMDB2源連接
type: Tutorial
description: 瞭解如何使用IBMUI建立Adobe Experience PlatformDB2源連接。
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# 在UI中建立IBMDB2源連接

>[!NOTE]
>
> IBMDB2連接器為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供了使用以下工具建立IBMDB2（以下稱「DB2」）源連接器的步驟： [!DNL Platform] 用戶介面。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有有效的DB2連接，則可以跳過本文檔的其餘部分並繼續上的教程 [配置資料流](../../dataflow/databases.md)。

### 收集所需憑據

以下各節提供了您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

| 憑據 | 說明 |
| ---------- | ----------- |
| `server` | DB2伺服器的名稱。 可以在伺服器名稱后指定埠號（以冒號分隔）。 例如：伺服器：埠。 |
| `database` | DB2資料庫的名稱。 |
| `username` | 用於連接到DB2資料庫的用戶名。 |
| `password` | 為用戶名指定的用戶帳戶的密碼。 |

有關入門的詳細資訊，請參閱 [此DB2文檔](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html)。

## 連接您的IBMDB2帳戶

收集了所需憑據後，您可以按照以下步驟將DB2帳戶連結到 [!DNL Platform]。

登錄到 [Adobe Experience Platform](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左導航欄訪問 **[!UICONTROL 源]** 工作區。 的 **[!UICONTROL 目錄]** 螢幕顯示可為其建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 **[!UICONTROL 資料庫]** 類別，選擇 **[!UICONTROL IBMDB2]**。 如果這是您第一次使用此連接器，請選擇 **[!UICONTROL 配置]**。 否則，選擇 **[!UICONTROL 添加資料]** 建立新的DB2連接器。

![目錄](../../../../images/tutorials/create/ibm-db2/catalog.png)

的 **[!UICONTROL 連接到IBMDB2]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和DB2憑據。 完成後，選擇 **[!UICONTROL 連接]** 然後再給新連接建立一段時間。

![連接](../../../../images/tutorials/create/ibm-db2/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的DB2帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/ibm-db2/existing.png)

## 後續步驟

按照本教程，您已建立了與DB2帳戶的連接。 現在，您可以繼續下一個教程， [配置資料流以將資料 [!DNL Platform]](../../dataflow/databases.md)。
