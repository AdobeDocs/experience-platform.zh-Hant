---
keywords: Experience Platform；首頁；熱門主題；onetrust;OneTrust
solution: Experience Platform
title: （測試版）在UI中建立OneTrust來源連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立OneTrust來源連線。
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: cfc6e7cb3877f3b5f716b7f82e7c2d308ef5ed10
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# （測試版）建立 [!DNL OneTrust Integration] UI中的源連接

>[!NOTE]
>
>此 [!DNL OneTrust Integration] 來源為測試版。 其功能和檔案可能會有所變更。 如需使用測試版標籤來源的詳細資訊，請參閱 [來源概觀](../../../../home.md#terms-and-conditions).

本教學課程提供建立 [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) 來源連線，使用Platform使用者介面將歷史和排程的同意資料內嵌至Adobe Experience Platform。

## 先決條件

>[!IMPORTANT]
>
>此 [!DNL OneTrust Integration] 來源連接器和檔案是由 [!DNL OneTrust Integration] 團隊。 如有任何查詢或更新請求，請聯絡 [[!DNL OneTrust] 團隊](https://my.onetrust.com/s/contactsupport?language=en_US) 直接。

連接之前 [!DNL OneTrust Integration] 至Platform，您必須先擷取存取權杖。 如需尋找存取權杖的詳細指示，請參閱 [[!DNL OneTrust Integration] OAuth 2指南](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

存取權杖過期後不會自動重新整理，因為不支援系統對系統的重新整理權杖 [!DNL OneTrust]. 因此，您必須確定您的存取權杖在連線過期之前已更新。 存取權杖的最大可設定有效期限為一年。 若要進一步了解更新存取權杖的資訊，請參閱 [[!DNL OneTrust] 管理OAuth 2.0用戶端認證的相關檔案](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### 收集所需憑據

為了連接 [!DNL OneTrust Integration] 至Platform，您必須提供下列驗證憑證的值：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| 主機名稱 | 來自 [!DNL OneTrust Integration] 需要從中提取資料。 | `https://uat.onetrust.com/` |
| 授權測試URL | （可選）建立基本連線時，授權測試URL用於驗證憑證。 如果未提供，則在建立源連接步驟期間將自動檢查憑據。 |  |
| 存取權杖 | 與 [!DNL OneTrust Integration] 帳戶。 | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

如需這些憑證的詳細資訊，請參閱 [[!DNL OneTrust Integration] 驗證檔案](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## 連接您的 [!DNL OneTrust Integration] 帳戶

>[!NOTE]
>
>此 [!DNL OneTrust Integration] API規格已與Adobe共用，以供資料擷取。

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 *[!UICONTROL 同意與偏好設定]* 類別，選擇 [!DNL OneTrust Integration]，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/onetrust/catalog.png)

此 **[!UICONTROL 連接OneTrust整合帳戶]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL OneTrust Integration] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/onetrust/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選用說明和您的憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![new](../../../../images/tutorials/create/onetrust/new.png)

## 後續步驟

依照本教學課程，您已建立與 [!DNL OneTrust Integration] 帳戶。 您現在可以繼續下一個教學課程，以及 [設定資料流，將同意資料匯入Platform](../../dataflow/consent-and-preferences.md).
