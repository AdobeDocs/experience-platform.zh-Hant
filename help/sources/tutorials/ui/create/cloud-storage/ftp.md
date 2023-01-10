---
keywords: Experience Platform；首頁；熱門主題；FTP;FTP
solution: Experience Platform
title: 在UI中建立FTP來源連線
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立FTP來源連線。
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# 在UI中建立FTP來源連線

>[!NOTE]
>
>FTP連接器為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

本教學課程提供使用Adobe Experience Platform UI建立FTP來源連線的步驟。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效的FTP連線，可略過本檔案的其餘部分，並繼續進行以下的教學課程： [配置資料流](../../dataflow/batch/cloud-storage.md).

### 收集所需憑據

若要連線至FTP，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 與您的FTP伺服器相關聯的名稱或IP位址。 |
| `username` | 可存取您FTP伺服器的使用者名稱。 |
| `password` | FTP伺服器的密碼。 |

## 連線至您的FTP伺服器

收集完所需憑證後，您可以依照下列步驟建立新的FTP帳戶以連線至Platform。

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示各種來源，您可以用來建立入站帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 [!UICONTROL 雲端儲存空間] 類別，選擇 **[!UICONTROL FTP]**. 如果這是您第一次使用此連接器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 建立新FTP連線。

![目錄](../../../../images/tutorials/create/ftp/catalog.png)

此 **[!UICONTROL 連線至FTP]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、可選說明和您的憑證。 完成後，請選取 **[!UICONTROL Connect]** 然後讓新連接建立一段時間。

![new](../../../../images/tutorials/create/ftp/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的FTP帳戶，然後選取 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/ftp/existing.png)

## 後續步驟

依照本教學課程，您已建立與FTP帳戶的連線。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料從雲儲存帶入平台](../../dataflow/batch/cloud-storage.md).
