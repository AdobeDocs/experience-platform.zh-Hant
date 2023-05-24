---
keywords: Experience Platform；首頁；熱門主題；Zoho CRM;Zoho crm;Zoho;zoho
solution: Experience Platform
title: Zoho CRM源連接器概述
description: 瞭解如何使用API或用戶介面將Zoho CRM連接到Adobe Experience Platform。
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# [!DNL Zoho CRM]

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

Experience Platform支援從第三方CRM系統接收資料。 對CRM提供程式的支援包括 [!DNL Zoho CRM]。

## IP地址允許清單

在使用源連接器之前，必須將IP地址清單添加到允許清單。 如果無法將特定於區域的IP地址添加到允許清單，則在使用源時可能會導致錯誤或效能不佳。 查看 [IP地址允許清單](../../ip-address-allow-list.md) 的子菜單。

## 檢索您的身份驗證憑據 [!DNL Zoho CRM]

在從 [!DNL Zoho CRM] 帳戶到平台，必須首先檢索您的憑據以驗證您的 [!DNL Zoho CRM] 源。 按照以下步驟檢索客戶端ID、客戶端密碼、訪問令牌和刷新令牌。

### 註冊您的應用程式

檢索身份驗證憑據的第一步是使用 [[!DNL Zoho CRM] 開發者控制台](https://accounts.zoho.com/)。 要註冊應用程式，必須從以下位置選擇客戶端類型：Java指令碼、基於Web的移動、非瀏覽器移動應用程式或自客戶端。 接下來，提供應用程式名稱、網頁URL和授權重定向URI的值 [!DNL Zoho CRM] 然後使用授權令牌重定向您。

成功註冊會返回您的客戶端ID和客戶端機密。

### 建立授權請求

接下來，必須建立 [授權請求](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) 使用基於Web的應用程式或自身客戶端。 授權請求返回授予令牌，從而允許您檢索訪問令牌。

建立授權請求時，必須填寫兩者的值 **作用域** 和 **訪問類型**。 請參閱此 [[!DNL Zoho CRM] 文檔](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) 查看有關作用域的詳細資訊， **訪問類型** 應始終設定為 `offline`。

### 生成訪問和刷新令牌

檢索到授權令牌後，可以生成 [訪問和刷新令牌](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) 通過POST請求 `{ACCOUNTS_URL}/oauth/v2/token` 提供客戶端ID、客戶端機密、授予令牌和重定向URI時。 在此步驟中，還必須包括 `grant_type` 作為參數，並將值設定為 `"authorization_code"`。

成功的請求將返回您的訪問和刷新令牌，然後您可以使用這些令牌進行身份驗證。

有關獲取憑據的詳細步驟，請參閱 [[!DNL Zoho CRM] 認證指南](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html)。

## 連接 [!DNL Zoho CRM] 至 [!DNL Platform] 使用API

以下文檔提供了有關如何連接的資訊 [!DNL Zoho CRM] 到使用API或用戶介面的平台：

- [建立 [!DNL Zoho CRM] 使用流服務API的基連接](../../tutorials/api/create/crm/zoho.md)
- [使用流服務API瀏覽資料表](../../tutorials/api/explore/tabular.md)
- [使用流服務API為CRM源建立資料流](../../tutorials/api/collect/crm.md)

## 連接 [!DNL Zoho CRM] 至 [!DNL Platform] 使用UI

- [建立 [!DNL Zoho CRM] UI中的源連接](../../tutorials/ui/create/crm/zoho.md)
- [在UI中為CRM源連接建立資料流](../../tutorials/ui/dataflow/crm.md)
