---
keywords: Experience Platform；首頁；熱門主題；Oracle服務雲；oracle服務雲
title: 在UI中建立Oracle服務雲源連接
description: 瞭解如何使用Adobe Experience PlatformUI建立Oracle服務雲源連接。
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: 1695b7d638feb648d5cd7af07879f3ed13f938eb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# 在UI中建立Oracle服務雲源連接

本教程提供了使用Adobe Experience Platform用戶介面建立Oracle服務雲源連接的步驟。

## 快速入門

本教程需要對以下Experience Platform組成部分進行有效理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有有效的Oracle服務雲源連接，則可以跳過本文檔的其餘部分並繼續上的教程。 [配置資料流](../../dataflow/customer-success.md)

### 收集所需憑據

為了訪問您的Oracle服務雲帳戶 [!DNL Platform]，必須提供以下值：

| 憑據 | 說明 |
| ---------- | ----------- |
| Host | oracle服務雲實例的主機URL。 |
| 用戶名 | oracle服務雲用戶帳戶的用戶名。 |
| 密碼 | oracle服務雲帳戶的密碼。 |

有關驗證Oracle服務雲帳戶的詳細資訊，請參閱 [[!DNL Oracle] 認證指南](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html)。

## 連接您的Oracle服務雲帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可用於建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索欄找到要使用的特定源。

在 [!UICONTROL 客戶成功] 類別，選擇 **[!UICONTROL Oracle服務雲]** ，然後選擇 **[!UICONTROL 添加資料]**。

![突出顯示了Oracle服務雲源的源目錄。](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

的 **[!UICONTROL 連接到Oracle服務雲]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要連接現有帳戶，請選擇要連接的Oracle服務雲帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有帳戶介面。](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和您的Oracle服務雲憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![具有佔位符值的新帳戶介面。](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## 後續步驟

按照本教程，您已建立到Oracle服務雲帳戶的連接。 現在，您可以繼續下一個教程， [配置資料流，將客戶成功資料引入平台](../../dataflow/crm.md)。
