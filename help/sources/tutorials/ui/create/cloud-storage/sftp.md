---
keywords: Experience Platform;home；熱門主題；SFTP;sftp
solution: Experience Platform
title: 在UI中建立SFTP來源連線
topic: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立SFTP來源連線。
translation-type: tm+mt
source-git-commit: 0e11acc4a599d360cb3048445003f61848ad23d3
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---


# 在UI中建立SFTP來源連線

本教學課程提供使用Adobe Experience PlatformUI建立SFTP來源連線的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

>[!IMPORTANT]
>
>建議在使用SFTP來源連線來收錄JSON物件時，避免新行或回車。 若要解決限制，請每行使用單一JSON物件，並使用多行來建立後續檔案。

如果您已經有有效的SFTP連接，則可跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集必要的認證

要連接到SFTP，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | 與您的SFTP伺服器相關聯的名稱或IP位址。 |
| `username` | 可存取您SFTP伺服器的使用者名稱。 |
| `password` | SFTP伺服器的密碼。 |
| `privateKeyContent` | Base64編碼的SSH私鑰內容。 OpenSSH密鑰的類型必須分類為RSA或DSA。 |
| `passPhrase` | 如果密鑰檔案或密鑰內容受密碼片語保護，則解密密鑰的密碼或密碼。 如果PrivateKeyContent受到密碼保護，則此參數必須與PrivateKeyContent的密碼短語一起使用，作為值。 |

收集完所需憑證後，您可依照下列步驟建立新的SFTP帳戶以連線至平台。

## 連線至您的SFTP伺服器

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL Catalog]畫面會顯示各種來源，您可以為其建立傳入帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在[!UICONTROL Cloud storage]類別下，選擇&#x200B;**[!UICONTROL SFTP]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL Add data]**&#x200B;以建立新的SFTP連接。

![目錄](../../../../images/tutorials/create/sftp/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Connect to SFTP]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果使用新憑據，請選擇&#x200B;**[!UICONTROL New account]**。 在出現的輸入表單上，提供名稱、選用說明和您的認證。 完成後，選擇&#x200B;**[!UICONTROL Connect]** ，然後允許一些時間建立新連接。

SFTP連接器提供您不同的存取驗證類型。 在&#x200B;**[!UICONTROL Account authentication]**&#x200B;下，選擇&#x200B;**[!UICONTROL Password]**&#x200B;以使用基於密碼的憑據。

![connect-password](../../../../images/tutorials/create/sftp/password.png)

或者，您也可以選擇&#x200B;**[SSH公鑰]**，並使用[!UICONTROL Private key content]和[!UICONTROL Passphrase]的組合連接SFTP帳戶。

>[!IMPORTANT]
>
>SFTP連接器支援RSA或DSA類型的OpenSSH金鑰。 請確定您的關鍵檔案內容以`"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`開頭，以`"-----END [RSA/DSA] PRIVATE KEY-----"`結尾。 如果私密金鑰檔案是PPK格式檔案，請使用PuTTY工具從PPK轉換為OpenSSH格式。

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| 憑證 | 說明 |
| ---------- | ----------- |
| 私密金鑰內容 | Base64編碼的SSH私鑰內容。 OpenSSH密鑰的類型必須分類為RSA或DSA。 |
| 密碼短語 | 指定密鑰檔案或密鑰內容受密碼片語保護時解密密鑰的密碼或密碼。 如果PrivateKeyContent受到密碼保護，則此參數必須與PrivateKeyContent的密碼短語一起使用，作為值。 |

### 現有帳戶

若要連線現有帳戶，請選取您要連線的FTP或SFTP帳戶，然後選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/sftp/existing.png)

## 後續步驟

在本教學課程中，您已建立與FTP或SFTP帳戶的連線。 您現在可以繼續下一個教學課程，並[設定資料流，將雲端儲存空間的資料匯入Platform](../../dataflow/batch/cloud-storage.md)。