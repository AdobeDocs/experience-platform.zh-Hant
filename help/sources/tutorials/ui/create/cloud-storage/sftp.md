---
keywords: Experience Platform；首頁；熱門主題；SFTP;sftp
solution: Experience Platform
title: 在UI中建立SFTP來源連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立SFTP來源連線。
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: ade0da445b18108a7f8720404cc7a65139ed42b1
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# 在UI中建立[!DNL SFTP]源連接

本教學課程提供使用Adobe Experience Platform UI建立[!DNL SFTP]來源連線的步驟。

## 快速入門

本教學課程需要妥善了解Platform的下列元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

>[!IMPORTANT]
>
>建議您在使用[!DNL SFTP]來源連線擷取JSON物件時，避免使用新的行或回車。 若要解決限制，請每行使用單一JSON物件，然後使用多行來建立後續檔案。

如果已經有有效的[!DNL SFTP]連接，則可以跳過本文檔的其餘部分，並繼續進行[配置資料流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集所需憑據

要連接到[!DNL SFTP]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 與[!DNL SFTP]伺服器相關聯的名稱或IP地址。 |
| `port` | 要連接的[!DNL SFTP]伺服器埠。 若未提供，則值預設為`22`。 |
| `username` | 可訪問[!DNL SFTP]伺服器的用戶名。 |
| `password` | [!DNL SFTP]伺服器的密碼。 |
| `privateKeyContent` | Base64編碼的SSH私密金鑰內容。 OpenSSH金鑰的類型必須分類為RSA或DSA。 |
| `passPhrase` | 如果密鑰檔案或密鑰內容受密碼短語保護，則解密私鑰的密碼短語或密碼。 如果PrivateKeyContent受密碼保護，則此參數需要與PrivateKeyContent的密碼短語一起使用，作為值。 |

收集完所需憑證後，您可以依照下列步驟建立新的[!DNL SFTP]帳戶以連線至Platform。

## 連接到您的[!DNL SFTP]伺服器

在平台UI中，從左側導覽列選取&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL 目錄]螢幕顯示各種來源，您可以用這些來源建立入站帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在[!UICONTROL 雲儲存]類別下，選擇&#x200B;**[!UICONTROL SFTP]**，然後選擇&#x200B;**[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/sftp/catalog.png)

此時會出現「**[!UICONTROL 連線至SFTP]**」頁面。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的FTP或SFTP帳戶，然後選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/sftp/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇&#x200B;**[!UICONTROL 新帳戶]**，然後為新[!DNL SFTP]帳戶提供名稱和可選說明。

#### 使用密碼進行驗證

[!DNL SFTP] 支援不同的身份驗證類型進行訪問。在&#x200B;**[!UICONTROL 帳戶驗證]**&#x200B;下，選擇&#x200B;**[!UICONTROL 密碼]**，然後提供要連接的主機和埠值，以及您的用戶名和密碼。

![connect-password](../../../../images/tutorials/create/sftp/password.png)

#### 使用SSH公開金鑰進行驗證

若要使用基於SSH公鑰的憑據，請選擇&#x200B;**[!UICONTROL SSH公鑰]**，然後提供主機和埠值，以及私鑰內容和密碼短語組合。

>[!IMPORTANT]
>
>SFTP支援RSA或DSA類型OpenSSH金鑰。 確保密鑰檔案內容的開頭為`"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`，結尾為`"-----END [RSA/DSA] PRIVATE KEY-----"`。 如果私鑰檔案是PPK格式檔案，請使用PuTTY工具從PPK格式轉換為OpenSSH格式。

![connect-ssh](../../../../images/tutorials/create/sftp/ssh-public-key.png)

| 憑據 | 說明 |
| ---------- | ----------- |
| 私密金鑰內容 | Base64編碼的SSH私密金鑰內容。 OpenSSH金鑰的類型必須分類為RSA或DSA。 |
| 密碼短語 | 如果密鑰檔案或密鑰內容受密碼短語保護，則指定密碼短語或密碼以解密私鑰。 如果PrivateKeyContent受密碼保護，則此參數需要與PrivateKeyContent的密碼短語一起使用，作為其值。 |


## 後續步驟

依照本教學課程，您已建立與SFTP帳戶的連線。 您現在可以繼續下一個教學課程，並[配置資料流，將雲儲存中的資料帶入Platform](../../dataflow/batch/cloud-storage.md)。
