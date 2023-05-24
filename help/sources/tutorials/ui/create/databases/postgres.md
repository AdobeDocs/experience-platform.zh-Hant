---
keywords: Experience Platform；首頁；熱門主題；[!DNL PostgreSQL];[!DNL PostgreSQL];PostgreSQL
solution: Experience Platform
title: 在UI中建立PostgreSQL源連接
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立PostgreSQL源連接。
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 2%

---

# 建立 [!DNL PostgreSQL] UI中的源連接

Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供建立 [!DNL PostgreSQL] 源連接器使用 [!DNL Platform] 用戶介面。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有 [!DNL PostgreSQL] 連接，您可以跳過本文檔的其餘部分並繼續學習有關 [配置資料流](../../dataflow/databases.md)。

### 收集所需憑據

為了訪問 [!DNL PostgreSQL] 帳戶 [!DNL Platform]，必須提供以下值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與您的 [!DNL PostgreSQL] 帳戶。 的 [!DNL PostgreSQL] 連接字串模式為： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |

有關入門的詳細資訊，請參閱此 [[!DNL PostgreSQL] 文檔](https://www.postgresql.org/docs/9.2/app-psql.html)。

#### 為連接字串啟用SSL加密

您可以為 [!DNL PostgreSQL] 連接字串，方法是將連接字串與以下屬性附加：

| 屬性 | 說明 | 範例 |
| --- | --- | --- |
| `EncryptionMethod` | 允許您在 [!DNL PostgreSQL] 資料。 | <uL><li>`EncryptionMethod=0`(停用)</li><li>`EncryptionMethod=1`(啟用)</li><li>`EncryptionMethod=6`（請求SSL）</li></ul> |
| `ValidateServerCertificate` | 驗證您發送的證書 [!DNL PostgreSQL] 資料庫 `EncryptionMethod` 的子菜單。 | <uL><li>`ValidationServerCertificate=0`(停用)</li><li>`ValidationServerCertificate=1`(啟用)</li></ul> |

以下是 [!DNL PostgreSQL] 附加有SSL加密的連接字串： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`。

## 連接 [!DNL PostgreSQL] 帳戶

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL PostgreSQL] 帳戶 [!DNL Platform]。

登錄到 [Adobe Experience Platform](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左導航欄訪問 **[!UICONTROL 源]** 工作區。 的 **[!UICONTROL 目錄]** 螢幕顯示可為其建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 **[!UICONTROL 資料庫]** 類別，選擇 **[!UICONTROL PostgreSQL資料庫]**。 如果這是您第一次使用此連接器，請選擇 **[!UICONTROL 配置]**。 否則，選擇 **[!UICONTROL 添加資料]** 新建 [!DNL PostgreSQL] 連接器。

![](../../../../images/tutorials/create/postgresql/catalog.png)

的 **[!UICONTROL 連接到[!DNL PostgreSQL]]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和 [!DNL PostgreSQL] 憑據。 完成後，選擇 **[!UICONTROL 連接]** 然後再給新連接建立一段時間。

![](../../../../images/tutorials/create/postgresql/new.png)

### 現有帳戶

要連接現有帳戶，請選擇 [!DNL PostgreSQL] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/postgresql/existing.png)

## 後續步驟

按照本教程，您已建立到 [!DNL PostgreSQL] 帳戶。 現在，您可以繼續下一個教程， [配置資料流以將資料 [!DNL Platform]](../../dataflow/databases.md)。
