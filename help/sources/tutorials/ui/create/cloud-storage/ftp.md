---
keywords: Experience Platform；首頁；熱門主題；FTP;ftp
solution: Experience Platform
title: 在UI中建立FTP源連接
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立FTP源連接。
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# 在UI中建立FTP源連接

>[!NOTE]
>
>FTP接頭處於Beta狀態。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

本教程提供了使用Adobe Experience PlatformUI建立FTP源連接的步驟。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有有效的FTP連接，則可以跳過本文檔的其餘部分並繼續上的教程 [配置資料流](../../dataflow/batch/cloud-storage.md)。

### 收集所需憑據

要連接到FTP，必須提供以下連接屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 與FTP伺服器關聯的名稱或IP地址。 |
| `username` | 有權訪問FTP伺服器的用戶名。 |
| `password` | FTP伺服器的密碼。 |

## 連接到FTP伺服器

收集所需憑據後，可以按照以下步驟建立新FTP帳戶以連接到平台。

登錄到 [Adobe Experience Platform](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左導航欄訪問 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可為其建立入站帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 [!UICONTROL 雲儲存] 類別，選擇 **[!UICONTROL FTP]**。 如果這是您第一次使用此連接器，請選擇 **[!UICONTROL 配置]**。 否則，選擇 **[!UICONTROL 添加資料]** 新建FTP連接。

![目錄](../../../../images/tutorials/create/ftp/catalog.png)

的 **[!UICONTROL 連接到FTP]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和憑據。 完成後，選擇 **[!UICONTROL 連接]** 然後再給新連接建立一段時間。

![新](../../../../images/tutorials/create/ftp/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的FTP帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/ftp/existing.png)

## 後續步驟

按照本教程，您已建立到FTP帳戶的連接。 現在，您可以繼續下一個教程， [配置資料流，將雲儲存中的資料引入平台](../../dataflow/batch/cloud-storage.md)。
