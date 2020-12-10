---
keywords: Experience Platform;home;popular topics;FTP;ftp
solution: Experience Platform
title: 在UI中建立FTP來源連接器
topic: overview
type: Tutorial
description: 本教學課程提供使用平台使用者介面建立FTP來源連接器的步驟。
translation-type: tm+mt
source-git-commit: e28a3ec2d4330f0e9f3895e0236c9ebea2ef2776
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---


# 在UI中建立FTP來源連接器

>[!NOTE]
>
>FTP連接器處於測試階段。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

本教學課程提供使用平台使用者介面建立FTP來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的FTP連線，則可以略過本文檔的其餘部分，然後繼續有關配置資料 [流的教程](../../dataflow/batch/cloud-storage.md)。

### 收集必要的認證

若要連線至FTP，您必須提供下列連線屬性的值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | 與您的FTP伺服器相關聯的名稱或IP位址。 |
| `username` | 可存取您FTP伺服器的使用者名稱。 |
| `password` | FTP伺服器的密碼。 |

## 連線至您的FTP伺服器

收集完所需憑證後，您可依照下列步驟建立新的FTP帳戶以連線至平台。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取  Sources工作區。 「目 [!UICONTROL 錄] 」畫面會顯示多種來源，您可為其建立傳入帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「雲端 [!UICONTROL 儲存空間] 」類別下，選 **[!UICONTROL 取「FTP」]**。 如果這是您第一次使用此連接器，請選擇「配 **[!UICONTROL 置」]**。 否則，請選 **[!UICONTROL 擇「新增資料]** 」以建立新的FTP連線。

![目錄](../../../../images/tutorials/create/ftp/catalog.png)

此時 **[!UICONTROL 會顯示「連線至FTP]** 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供名稱、選用說明和您的認證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![new](../../../../images/tutorials/create/ftp/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的FTP帳戶，然後選取「下 **[!UICONTROL 一]** 步」繼續。

![現有](../../../../images/tutorials/create/ftp/existing.png)

## 後續步驟

在本教學課程中，您已建立與FTP帳戶的連線。 您現在可以繼續下一個教學課程，並 [設定資料流，將雲端儲存空間的資料匯入平台](../../dataflow/batch/cloud-storage.md)。