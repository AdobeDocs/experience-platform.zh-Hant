---
title: 使用平台UI建立OracleEloqua源連接
description: 瞭解如何使用平台UI將Adobe Experience Platform連接到OracleEloqua。
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 1%

---

# 建立 [!DNL Oracle Eloqua] 使用平台UI的源連接

本教程提供建立 [!DNL Oracle Eloqua] 源連接，使用Adobe Experience Platform用戶介面。

## 快速入門

本指南要求對平台的以下元件有良好的理解：

* [源](../../../../home.md):平台允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):平台提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

如果您已經通過身份驗證 [!DNL Oracle Eloqua] 平台上的帳戶，則您可以跳過本文檔的其餘部分，繼續學習有關 [建立資料流，將營銷自動化資料帶到平台](../../dataflow/marketing-automation.md)。

### 收集所需憑據

為了連接 [!DNL Oracle Eloqua] 到平台，必須提供以下驗證屬性的值：

| 憑據 | 說明 |
| --- | --- |
| 端點 | 您的終結點 [!DNL Oracle Eloqua] 伺服器。 [!DNL Oracle Eloqua] 支援多個資料中心。 要查找您的終結點，請登錄到 [[!DNL Oracle Eloqua] 介面](https://login.eloqua.com) 然後從重定向URL複製基URL部分。 URL模式的格式為 `xxx.xx.eloqua.com` 應輸入 `http` 或 `https`。 |
| 用戶名 | 您的用戶名 [!DNL Oracle Eloqua] 伺服器。 用戶名必須格式化為 `siteName + \\ + username`，也請參見Wiki頁。 `siteName` 是您用於登錄的公司名稱 [!DNL Oracle Eloqua] 和 `username` 是您的用戶名。 例如，您的登錄用戶名可以是： `Eloqua\Andy`。 **注釋**:必須使用單個反斜線(`\`)使用UI時，因為Experience PlatformUI會自動添加附加反斜線(`\`)。 |
| 密碼 | 與您的 [!DNL Oracle Eloqua] 用戶名。 |

有關的身份驗證憑據的詳細資訊 [!DNL Oracle Eloqua]，請參見 [[!DNL Oracle Eloqua] 認證指南](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html)。

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL Oracle Eloqua] 帳戶到平台。

## 連接 [!DNL Oracle Eloqua] 帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 [!UICONTROL 營銷自動化] 類別，選擇 **[!UICONTROL Oracle雄辯]**，然後選擇 **[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

的 **[!UICONTROL 連接OracleEloqua帳戶]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要使用現有帳戶，請選擇 [!DNL Oracle Eloqua] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後為您提供名稱、可選說明和相應的值 [!DNL Oracle Eloqua] 憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![新](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 後續步驟

按照本教程，您已經驗證並建立了源連接 [!DNL Oracle Eloqua] 帳戶和平台。 現在，您可以繼續下一個教程， [建立資料流，將營銷自動化資料帶到平台](../../dataflow/marketing-automation.md)。
