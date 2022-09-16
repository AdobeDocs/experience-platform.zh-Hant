---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
solution: Experience Platform
title: 使用Platform UI建立MailChimp成員源連接
topic-legacy: tutorial
description: 了解如何使用Platform UI將Adobe Experience Platform連線至MailChimp成員。
exl-id: dc620ef9-624d-4fc9-8475-bb475ea86eb7
source-git-commit: 430b544835956ec0b212fb44d48beaae46afdd2e
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# 建立 [!DNL Mailchimp Members] 使用Platform UI的來源連線

本教學課程提供建立 [!DNL Mailchimp] 來源連接器以內嵌 [!DNL Mailchimp Members] 使用者介面將資料傳送至Adobe Experience Platform。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Platform可讓您從各種來源擷取資料，同時能使用來建構、加上標籤，以及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md):Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以協助開發及改進數位體驗應用程式。

## 收集所需憑據

為了把 [!DNL Mailchimp Members] 資料至Platform時，您必須先提供與您的 [!DNL Mailchimp] 帳戶。

此 [!DNL Mailchimp Members] 原始碼支援OAuth 2重新整理程式碼和基本驗證。 有關這些驗證類型的詳細資訊，請參閱下表。

### OAuth 2重新整理程式碼

| 憑證 | 說明 |
| --- | --- |
| 網域 | 用於連接到MailChimp API的根URL。 根URL的格式為 `https://{DC}.api.mailchimp.com`，其中 `{DC}` 代表與您帳戶對應的資料中心。 |
| 授權測試URL | 連接時，授權測試URL用於驗證憑據 [!DNL Mailchimp] 到平台。 如果未提供，則在建立源連接步驟期間會自動檢查憑據。 |
| 存取權杖 | 用於驗證源的相應訪問令牌。 這是OAuth型驗證的必要項目。 |

如需使用OAuth 2驗證您的 [!DNL Mailchimp] 帳戶至Platform，請參閱 [[!DNL Mailchimp] 使用OAuth 2的檔案](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### 基本驗證

| 憑證 | 說明 |
| --- | --- |
| 網域 | 用於連接到MailChimp API的根URL。 根URL的格式為 `https://{DC}.api.mailchimp.com`，其中 `{DC}` 代表與您帳戶對應的資料中心。 |
| 使用者名稱 | 與您的MailChimp帳戶對應的用戶名。 這是基本驗證的必要條件。 |
| 密碼 | 與您的MailChimp帳戶對應的密碼。 這是基本驗證的必要條件。 |

## 連接您的 [!DNL Mailchimp Members] 帳戶至平台

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 [!UICONTROL 行銷自動化] 類別，選擇 **[!UICONTROL Mailchimp行銷活動]**，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/mailchimp-members/catalog.png)

此 **[!UICONTROL 連接Mailchimp促銷活動帳戶]** 頁。 在此頁面中，您可以選取要存取現有帳戶，還是選擇建立新帳戶。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Mailchimp Members] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/mailchimp-members/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供您的 [!DNL Mailchimp Members] 源連接詳細資訊。

![new](../../../../images/tutorials/create/mailchimp-members/new.png)


#### 使用OAuth 2進行驗證

若要使用OAuth 2，請選取 [!UICONTROL OAuth 2重新整理程式碼]，提供網域、授權測試URL和存取權杖的值，然後選取 **[!UICONTROL 連接到源]**. 請稍候驗證憑證，然後選取 **[!UICONTROL 下一個]** 繼續。

![oauth](../../../../images/tutorials/create/mailchimp-members/oauth.png)

#### 使用基本身份驗證進行身份驗證

要使用基本身份驗證，請選擇 [!UICONTROL 基本驗證]，請提供您的網域、使用者名稱和密碼的值，然後選取 **[!UICONTROL 連接到源]**. 請稍候驗證憑證，然後選取 **[!UICONTROL 下一個]** 繼續。

![基本](../../../../images/tutorials/create/mailchimp-members/basic.png)

### 選擇 [!DNL Mailchimp Members] 資料

驗證來源後，您必須提供 `listId` 與 [!DNL Mailchimp Members] 帳戶。

在 [!UICONTROL 選擇資料] 頁面，輸入 `listId` 然後選取 **[!UICONTROL 探索]**.

![探索](../../../../images/tutorials/create/mailchimp-members/explore.png)

頁面會更新為互動式結構樹狀結構，可讓您探索及檢查資料的階層。 選擇 **[!UICONTROL 下一個]** 繼續。

![select-data](../../../../images/tutorials/create/mailchimp-members/select-data.png)

## 後續步驟

使用 [!DNL Mailchimp] 帳戶已驗證，您 [!DNL Mailchimp Members] 若選取資料，您現在可以開始建立資料流，將資料帶入Platform。 有關如何建立資料流的詳細步驟，請參閱 [建立資料流，將行銷自動化資料帶入Platform](../../dataflow/marketing-automation.md).
