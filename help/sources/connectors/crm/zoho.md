---
keywords: Experience Platform；首頁；熱門主題；Zoho CRM；zoho crm；Zoho；zoho
solution: Experience Platform
title: Zoho CRM Source Connector概述
description: 瞭解如何使用API或使用者介面將Zoho CRM連結至Adobe Experience Platform。
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# [!DNL Zoho CRM]

>[!WARNING]
>
>[!DNL Zoho CRM]來源將於2025年6月底淘汰。

Adobe Experience Platform允許從外部來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商CRM系統擷取資料。 CRM提供者的支援包括[!DNL Zoho CRM]。

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 擷取[!DNL Zoho CRM]的驗證認證

您必須先擷取認證以驗證您的[!DNL Zoho CRM]來源，才能將[!DNL Zoho CRM]帳戶中的資料帶入Experience Platform。 請依照下列步驟擷取您的使用者端ID、使用者端密碼、存取權杖和重新整理權杖。

### 註冊您的應用程式

擷取驗證認證的第一步，是使用[[!DNL Zoho CRM] 開發人員主控台](https://accounts.zoho.com/)註冊您的應用程式。 若要註冊您的應用程式，您必須從以下專案選取您的使用者端型別：Java Script、網頁式、行動裝置、非瀏覽器行動應用程式或自行使用者端。 接著，提供應用程式名稱、網頁URL及授權重新導向URI的值，供[!DNL Zoho CRM]使用授與Token重新導向。

註冊成功即會傳回您的使用者端ID和使用者端密碼。

### 建立授權請求

接下來，您必須使用網頁式應用程式或自我使用者端來建立[授權要求](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html)。 授權請求會傳回您的授與Token，讓您擷取存取Token。

建立授權要求時，您必須填寫&#x200B;**範圍**&#x200B;和&#x200B;**存取型別**&#x200B;的值。 請參閱此[[!DNL Zoho CRM] 檔案](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html)以取得範圍詳細資訊，而您的&#x200B;**存取型別**&#x200B;應一律設定為`offline`。

### 產生存取權並重新整理Token

擷取您的授與Token後，您可以產生[存取和重新整理Token](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html)，方法是在提供使用者端ID、使用者端密碼、授與Token和重新導向URI時，向`{ACCOUNTS_URL}/oauth/v2/token`發出POST要求。 在此步驟中，您也必須包含`grant_type`作為引數，並將值設為`"authorization_code"`。

成功的請求會傳回您的存取和重新整理權杖，然後您可以使用這些權杖進行驗證。

如需取得認證的詳細步驟，請參閱[[!DNL Zoho CRM] 驗證指南](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html)。

## 使用API連線[!DNL Zoho CRM]至[!DNL Experience Platform]

以下檔案提供如何使用API或使用者介面將[!DNL Zoho CRM]連線至Experience Platform的資訊：

- [使用Flow Service API建立 [!DNL Zoho CRM] 基本連線](../../tutorials/api/create/crm/zoho.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為CRM來源建立資料流](../../tutorials/api/collect/crm.md)

## 使用UI連線[!DNL Zoho CRM]至[!DNL Experience Platform]

- [在使用者介面中建立 [!DNL Zoho CRM] 來源連線](../../tutorials/ui/create/crm/zoho.md)
- [在UI中為CRM來源連線建立資料流](../../tutorials/ui/dataflow/crm.md)
