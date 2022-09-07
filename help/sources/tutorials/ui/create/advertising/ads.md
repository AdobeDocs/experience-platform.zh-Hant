---
keywords: Experience Platform；首頁；熱門主題；Google Ads;Google Ads來源連接器；google ads連接器
title: 在UI中建立Google Ads來源連線
description: 了解如何使用Google UI建立Adobe Experience Platform Ads來源連線。
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: 56419f41188c9bfdbeda7dde680f269b980a37f0
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# 在UI中建立Google Ads來源連線

>[!NOTE]
>
>Google廣告來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

本教學課程提供使用Google使用者介面建立Adobe Experience Platform Ads來源連接器的步驟。

## 快速入門

本教學課程需要妥善了解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效的Google Ads連線，可以略過本檔案的其餘部分，並繼續進行以下的教學課程： [配置資料流](../../dataflow/advertising.md)

### 收集所需憑據

若要存取您的Google Ads帳戶平台，您必須提供下列值：

| 憑據 | 說明 |
| ---------- | ----------- |
| 用戶端客戶ID | 用戶端客戶ID是與您要透過Google Ads API管理之Google Ads用戶端帳戶對應的帳號。 此ID會遵循 `123-456-7890`. |
| 開發人員代號 | 開發人員代號可讓您存取Google Ads API。 您可以使用相同的開發人員代號，對您的所有Google Ads帳戶提出要求。 擷取開發人員代號，方法為 [登入您的經理帳戶](https://ads.google.com/home/tools/manager-accounts/) 接著，導覽至API中心頁面。 |
| 重新整理Token | 重新整理代號是 [!DNL OAuth2] 驗證。 此Token可讓您在存取Token過期後重新產生存取Token。 |
| 用戶端ID | 用戶端ID會與用戶端密碼一併用於 [!DNL OAuth2] 驗證。 用戶端ID和用戶端密碼可搭配使用，將您的應用程式識別至Google，以代表您的帳戶運作。 |
| 用戶端密碼 | 用戶端密碼會與用戶端ID搭配使用，作為 [!DNL OAuth2] 驗證。 用戶端ID和用戶端密碼可搭配使用，將您的應用程式識別至Google，以代表您的帳戶運作。 |

請參閱API概觀檔案，以取得 [開始使用Google Ads的詳細資訊](https://developers.google.com/google-ads/api/docs/first-call/overview).

## 連線您的Google Ads帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 **[!UICONTROL 廣告]** 類別，選擇 **[!UICONTROL Google Ads]**，然後選取 **[!UICONTROL 新增資料]**.

![Experience PlatformUI來源目錄中Google Ads來源的影像](../../../../images/tutorials/create/ads/catalog.png).

此 **[!UICONTROL 連線至Google Ads]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的Google Ads帳戶，然後選取 **[!UICONTROL 下一個]** 繼續。

![可用來建立Google Ads資料流的現有帳戶清單的影像，其包含](../../../../images/tutorials/create/ads/existing.png).

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、選用說明和您的Google Ads憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![Experience PlatformUI上新帳戶連線畫面的影像](../../../../images/tutorials/create/ads/connect.png).

## 後續步驟

依照本教學課程，您已建立與Google Ads帳戶的連線。 您現在可以繼續下一個教學課程，以及 [設定資料流以將廣告資料匯入Platform](../../dataflow/advertising.md).
