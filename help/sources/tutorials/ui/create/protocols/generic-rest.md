---
keywords: Experience Platform；首頁；熱門主題；一般REST API
title: 在使用者介面中建立一般REST API Source連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立通用REST API來源連線。
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 3%

---

# 在使用者介面中建立[!DNL Generic REST API]來源連線

>[!NOTE]
>
> [!DNL Generic REST API]來源是測試版。 如需使用Beta標籤聯結器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

本教學課程提供使用Adobe Experience Platform使用者介面建立[!DNL Generic REST API]來源聯結器的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 收集必要的認證

若要在Experience Platform上存取您的[!DNL Generic REST API]帳戶，您必須為您選擇的驗證型別提供有效的認證。 一般REST API支援OAuth 2重新整理程式碼和基本驗證。 請參閱下清單格，瞭解兩種支援的驗證型別之證明資料的資訊。

#### OAuth 2重新整理代碼

| 認證 | 說明 |
| --- | --- |
| Host | 您向其提出請求的來源的主機URL。 此值為必填，無法使用要求引數覆寫來略過。 |
| 授權測試URL | （選用）建立基本連線時，授權測試URL會用於驗證認證。 如果未提供，則會在來源連線建立步驟期間自動檢查認證。 |
| 用戶端 ID | （選用）與您的使用者帳戶相關聯的使用者端ID。 |
| 用戶端密碼 | （選用）與您的使用者帳戶相關聯的使用者端密碼。 |
| 存取權杖 | 用來存取應用程式的主要驗證認證。 存取權杖代表應用程式的授權，可存取使用者資料的特定方面。 此值為必填，無法使用要求引數覆寫來略過。 |
| 重新整理權杖 | （選用）當存取權杖過期時，用來產生新存取權杖的權杖。 |
| 存取記號URL | （選用）用來擷取存取權杖的URL端點。 |
| 要求引數覆寫 | （選擇性）屬性，可讓您指定要覆寫哪些認證引數。 |


#### 基本驗證

| 認證 | 說明 |
| --- | --- |
| Host | 您向其提出請求的來源的主機URL。 |
| 使用者名稱 | 與您的使用者帳戶對應的使用者名稱。 |
| 密碼 | 與您的使用者帳戶對應的密碼。 |

## 連線您的通用REST API帳戶

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以用來建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋列來尋找您要使用的特定來源。

在[!UICONTROL 通訊協定]類別下，選取&#x200B;**[!UICONTROL 一般REST API]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![目錄](../../../../images/tutorials/create/generic-rest/catalog.png)

**[!UICONTROL 連線至一般REST API]**&#x200B;頁面就會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的Generic REST API帳戶，然後選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/generic-rest/existing.png)

### 新帳戶

如果您正在建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後為您新的[!DNL Generic REST API]帳戶提供名稱和選項說明。

![新](../../../../images/tutorials/create/generic-rest/new.png)

#### 使用OAuth 2重新整理程式碼進行驗證

[!DNL Generic REST API]同時支援OAuth 2重新整理程式碼和基本驗證。 若要使用OAuth2驗證進行驗證，請選取&#x200B;**[!UICONTROL OAuth2RefreshCode]**，提供您的OAuth 2認證，然後選取&#x200B;**[!UICONTROL 連線至來源]**。

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### 使用基本驗證進行驗證

若要使用基本驗證，請選取&#x200B;**[!UICONTROL 基本驗證]**，提供您的主機、使用者名稱和密碼，然後選取&#x200B;**[!UICONTROL 連線到來源]**。

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## 後續步驟

依照本教學課程中的指示，您已建立與一般REST API帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入Experience Platform](../../dataflow/protocols.md)。
