---
title: 在UI中建立SFTP源連接
description: 瞭解如何使用Adobe Experience PlatformUI建立SFTP源連接。
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# 建立 [!DNL SFTP] UI中的源連接

本教程提供建立 [!DNL SFTP] 源連接使用Adobe Experience PlatformUI。

## 快速入門

本教程需要瞭解平台的以下元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

>[!IMPORTANT]
>
>建議在使用JSON對象插入時避免新行或回車 [!DNL SFTP] 源連接。 要繞過限制，請每行使用一個JSON對象，並使用多行來獲取後續檔案。

如果您已經有 [!DNL SFTP] 連接，您可以跳過本文檔的其餘部分並繼續學習有關 [配置資料流](../../dataflow/batch/cloud-storage.md)。

### 收集所需憑據

為了連接到 [!DNL SFTP]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 與您的 [!DNL SFTP] 伺服器。 |
| `port` | 的 [!DNL SFTP] 您正在連接到的伺服器埠。 如果未提供，則值預設為 `22`。 |
| `username` | 有權訪問您的 [!DNL SFTP] 伺服器。 |
| `password` | 您的密碼 [!DNL SFTP] 伺服器。 |
| `privateKeyContent` | Base64編碼的SSH私鑰內容。 OpenSSH密鑰的類型必須分為RSA或DSA。 |
| `passPhrase` | 如果密鑰檔案或密鑰內容受密碼片語保護，則解密私鑰的密碼或密碼。 如果PrivateKeyContent受密碼保護，則此參數需要與PrivateKeyContent的密碼短語一起作為值使用。 |
| `maxConcurrentConnections` | 此參數允許您為平台在連接到SFTP伺服器時將建立的併發連接數指定最大限制。 必須將此值設定為小於SFTP設定的限制。 **注釋**:當為現有SFTP帳戶啟用此設定時，它將僅影響將來的資料流，而不影響現有的資料流。 |
| 檔案夾路徑 | 要提供訪問權限的資料夾的路徑。 [!DNL SFTP] 源，可提供資料夾路徑以指定用戶對所選子資料夾的訪問權限。 |

收集了所需憑據後，您可以按照以下步驟建立新憑據 [!DNL SFTP] 連接到平台的帳戶。

## 連接到 [!DNL SFTP] 伺服器

在平台UI中，選擇 **[!UICONTROL 源]** 從左導航欄訪問 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 [!UICONTROL 雲儲存] 類別，選擇 **[!UICONTROL SFTP]** ，然後選擇 **[!UICONTROL 添加資料]**。

![Experience Platform源目錄，且SFTP源已選定。](../../../../images/tutorials/create/sftp/catalog.png)

的 **[!UICONTROL 連接到SFTP]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要連接現有帳戶，請選擇要連接的FTP或SFTP帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![Experience PlatformUI上現有SFTP帳戶的清單。](../../../../images/tutorials/create/sftp/existing.png)

### 新帳戶

>[!IMPORTANT]
>
>SFTP支援RSA或DSA類型OpenSSH密鑰。 確保密鑰檔案內容以 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` 結尾 `"-----END [RSA/DSA] PRIVATE KEY-----"`。 如果私鑰檔案是PPK格式檔案，請使用PuTTY工具將PPK格式轉換為OpenSSH格式。

如果要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後提供新名稱和可選說明 [!DNL SFTP] 帳戶。

![SFTP的新帳戶螢幕](../../../../images/tutorials/create/sftp/new.png)

的 [!DNL SFTP] 源支援通過SSH公鑰進行基本身份驗證和身份驗證。

>[!BEGINTABS]

>[!TAB 基本身份驗證]

要使用基本身份驗證，請選擇 **[!UICONTROL 密碼]** 然後提供要連接的主機和埠值以及用戶名和密碼。 在此步驟中，您還可以指定要提供訪問權限的子資料夾的路徑。 完成後，選擇 **[!UICONTROL 連接到源]**。

![使用基本身份驗證的SFTP源的新帳戶螢幕](../../../../images/tutorials/create/sftp/password.png)

>[!TAB SSH公鑰身份驗證]

要使用基於SSH公鑰的憑據，請選擇 **[!UICONTROL SSH公鑰]**  然後提供主機和埠值，以及私鑰內容和密碼組合。 在此步驟中，您還可以指定要提供訪問權限的子資料夾的路徑。 完成後，選擇 **[!UICONTROL 連接到源]**。

![使用SSH公鑰的SFTP源的新帳戶螢幕。](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## 後續步驟

按照本教程，您已建立到SFTP帳戶的連接。 現在，您可以繼續下一個教程， [配置資料流，將雲儲存中的資料引入平台](../../dataflow/batch/cloud-storage.md)。
