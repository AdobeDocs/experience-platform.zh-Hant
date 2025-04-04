---
keywords: Experience Platform；首頁；熱門主題；方形；方形
title: 在UI中建立正方形Source連線
description: 瞭解如何使用Adobe Experience Platform UI建立方形來源連線。
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 3%

---

# 在使用者介面中建立[!DNL Square]來源連線

本教學課程提供使用Experience Platform使用者介面建立[!DNL Square]來源聯結器的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

### 收集必要的認證

若要存取您的[!DNL Square]帳戶Experience Platform，您必須提供下列值：

| 認證 | 說明 |
| --- | --- |
| Host | [!DNL Square]執行個體的網址。 |
| 用戶端 ID | 與您的[!DNL Square]帳戶相關聯的使用者端ID。 |
| 用戶端密碼 | 與您的[!DNL Square]帳戶相關聯的使用者端密碼。 |
| 存取權杖 | 存取權杖是用來驗證您的[!DNL Square]帳戶（具有OAuth 2.0驗證）。 存取權杖可從[!DNL Square]取得。 |
| 重新整理權杖 | 重新整理權杖會在您目前的存取權杖過期後，用來產生新的存取權杖。 可從[!DNL Square]取得重新整理權杖。 |

如需這些認證以及如何取得認證的詳細資訊，請參閱OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens)上的[[!DNL Square] 檔案。

收集必要的認證後，您可以依照下列步驟將[!DNL Square]帳戶連結至Experience Platform。

## 連線您的[!DNL Square]帳戶

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在[!UICONTROL 付款]類別下，選取&#x200B;**[!UICONTROL 方塊]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![目錄](../../../../images/tutorials/create/square/catalog.png)

**[!UICONTROL 連線至廣場]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取您要用來建立新資料流的[!DNL Square]帳戶，然後選取[下一步] ]**以繼續。**[!UICONTROL 

![現有](../../../../images/tutorials/create/square/existing.png)

### 新帳戶

如果您正在建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明以及您的[!DNL Square]認證的適當值。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![新](../../../../images/tutorials/create/square/new.png)

## 後續步驟

依照本教學課程，您已驗證並建立[!DNL Square]帳戶與Experience Platform之間的來源連線。 您現在可以繼續下一個教學課程，並[建立資料流以將付款資料帶入Experience Platform](../../dataflow/payments.md)。
