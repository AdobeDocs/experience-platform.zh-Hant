---
keywords: Experience Platform；首頁；熱門主題；Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Zoho CRM源連接器概述
description: 了解如何使用API或使用者介面將Zoho CRM連線至Adobe Experience Platform。
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# [!DNL Zoho CRM]

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

Experience Platform支援從協力廠商CRM系統擷取資料。 支援CRM提供者包括 [!DNL Zoho CRM].

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 擷取您的驗證憑證 [!DNL Zoho CRM]

將資料從 [!DNL Zoho CRM] 帳戶，您必須先擷取憑證以驗證您的 [!DNL Zoho CRM] 來源。 請依照下列步驟擷取您的用戶端ID、用戶端密碼、存取權杖，以及重新整理權杖。

### 註冊您的應用程式

擷取驗證憑證的第一步，是使用 [[!DNL Zoho CRM] 開發人員控制台](https://accounts.zoho.com/). 要註冊應用程式，必須從以下位置選擇客戶端類型：Java Script、網頁型、行動裝置、非瀏覽器行動應用程式或自助用戶端。 接下來，提供應用程式名稱、網頁URL和授權的重定向URI的值 [!DNL Zoho CRM] 然後可使用授權Token來重新導向您。

成功註冊會傳回用戶端ID和用戶端密碼。

### 建立授權請求

接下來，您必須建立 [授權請求](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) 使用基於web的應用程式或自身客戶端。 授權請求會傳回您的授權Token，而此Token可讓您擷取存取Token。

建立授權請求時，您必須填寫兩者的值 **作用域** 和 **存取類型**. 請參閱 [[!DNL Zoho CRM] 檔案](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) 有關作用域的詳細資訊，而 **存取類型** 應一律設為 `offline`.

### 產生您的存取權並重新整理Token

擷取授權代號後，您就可以產生 [存取和重新整理權杖](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) 透過向 `{ACCOUNTS_URL}/oauth/v2/token` 提供用戶端ID、用戶端密碼、授權Token和重新導向URI時，會執行下列操作： 在此步驟中，您也必須包含 `grant_type` 作為參數，並將值設定為 `"authorization_code"`.

成功的請求會傳回您的存取權並重新整理Token，之後您便可使用這些Token進行驗證。

如需取得認證的詳細步驟，請參閱 [[!DNL Zoho CRM] 驗證指南](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connect [!DNL Zoho CRM] to [!DNL Platform] 使用API

以下檔案提供如何連線的資訊 [!DNL Zoho CRM] 若要使用API或使用者介面來建立平台：

- [建立 [!DNL Zoho CRM] 使用流量服務API的基本連線](../../tutorials/api/create/crm/zoho.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流服務API為CRM源建立資料流](../../tutorials/api/collect/crm.md)

## Connect [!DNL Zoho CRM] to [!DNL Platform] 使用UI

- [建立 [!DNL Zoho CRM] UI中的源連接](../../tutorials/ui/create/crm/zoho.md)
- [在UI中為CRM源連接建立資料流](../../tutorials/ui/dataflow/crm.md)
