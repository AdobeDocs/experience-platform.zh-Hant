---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Google AdWords來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: ec2d0a33e0ae92a3153b7bdcad29734e487a0439
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---


# 在UI中 [!DNL Google AdWords] 建立來源連接器

>[!NOTE]
>連接 [!DNL Google AdWords] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用使用者介 [!DNL Google AdWords] 面建立來源連接器 [!DNL Platform] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [[!DNL Experience Data Model] (XDM)系統](../../../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL 即時客戶基本資料]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的 [!DNL Google AdWords] 連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料流 [的教程](../../dataflow/payments.md)

### 收集必要的認證

若要存取您的帳 [!DNL Google AdWords] 戶 [!DNL Platform]，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `clientCustomerId` | 帳戶的客戶客戶ID [!DNL AdWords] 。 |
| `developerToken` | 與管理員帳戶關聯的開發人員Token。 |
| `refreshToken` | 從授權訪問 [!DNL Google] 獲得的刷新令牌 [!DNL AdWords]。 |
| `clientId` | 用於取得重新整理 [!DNL Google] Token之應用程式的用戶端ID。 |
| `clientSecret` | 用來取得重新整理Token [!DNL Google] 之應用程式的用戶端密碼。 |

如需快速入門的詳細資訊，請參閱本 [[!DNL Google AdWords] 檔案](https://developers.google.com/adwords/api/docs/guides/authentication)。

## 連線您的帳 [!DNL Google AdWords] 戶

收集完所需的認證後，您可依照下列步驟將帳戶連結 [!DNL Google AdWords] 至 [!DNL Platform]。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 **** Sources工作區。 「目 **[!UICONTROL 錄]** 」畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「廣 **[!UICONTROL 告]** 」類別下，選 **[!UICONTROL 取「Google AdWords」]**。 如果這是您第一次使用此連接器，請選擇「配 **[!UICONTROL 置」]**。 否則，請選 **[!UICONTROL 擇「添加資料]** 」(Add data [!DNL Google AdWords] )以建立新連接器。

![目錄](../../../../images/tutorials/create/ads/catalog.png)

此時 **[!UICONTROL 會顯示「連線至Google AdWords]** 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供名稱、選用說明和您的認 [!DNL Google AdWords] 證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![連接](../../../../images/tutorials/create/ads/connect.png)

### 現有帳戶

若要連線現有帳戶，請選 [!DNL Google AdWords] 取您要連線的帳戶，然後選取「下 **[!UICONTROL 一]** 步」繼續。

![現有](../../../../images/tutorials/create/ads/existing.png)

## 後續步驟

遵循本教學課程，您已建立與帳戶的 [!DNL Google AdWords] 連線。 您現在可以繼續下一個教學課程，並 [設定資料流，將廣告資料帶入 [!DNL Platform]](../../dataflow/advertising.md)。