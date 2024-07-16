---
title: Salesforce Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Salesforce連線至Adobe Experience Platform。
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 5d28db34edd377269e8710b1741098a08616ae5f
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# [!DNL Salesforce]

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商CRM系統擷取資料。 CRM提供者的支援包括[!DNL Salesforce]。

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 從[!DNL Salesforce]到XDM的欄位對應

若要在[!DNL Salesforce]和Platform之間建立來源連線，[!DNL Salesforce]來源資料欄位必須先對應到適當的目標XDM欄位，才能擷取到Platform。

請參閱下列內容，以取得有關[!DNL Salesforce]資料集與Platform之間的欄位對應規則的詳細資訊：

- [連絡人](../adobe-applications/mapping/salesforce.md#contact)
- [銷售機會](../adobe-applications/mapping/salesforce.md#lead)
- [帳戶](../adobe-applications/mapping/salesforce.md#account)
- [機會](../adobe-applications/mapping/salesforce.md#opportunity)
- [機會聯絡人角色](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [行銷活動](../adobe-applications/mapping/salesforce.md#campaign)
- [行銷活動成員](../adobe-applications/mapping/salesforce.md#campaign-member)
- [帳戶聯絡人關係](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## 設定[!DNL Salesforce]名稱空間和結構描述自動產生公用程式

若要使用[!DNL Salesforce]來源做為[!DNL B2B-CDP]的一部分，您必須先設定[!DNL Postman]公用程式來自動產生[!DNL Salesforce]名稱空間和結構描述。 下列檔案提供有關設定[!DNL Postman]公用程式的額外資訊：

- 您可以從此[GitHub存放庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility)下載名稱空間和結構描述自動產生公用程式集合和環境。
- 如需有關使用Platform API的詳細資訊，包括如何收集必要標題的值以及讀取範例API呼叫，請參閱[Platform API快速入門](../../../landing/api-guide.md)的指南。
- 如需如何產生Platform API認證的詳細資訊，請參閱有關[驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md)的教學課程。
- 如需如何設定Platform API [!DNL Postman]的相關資訊，請參閱[設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md)上的教學課程。

透過平台開發人員主控台和[!DNL Postman]設定，您現在可以開始將適當的環境值套用至您的[!DNL Postman]環境。

下表包含範例值，以及有關填入[!DNL Postman]環境的其他資訊：

| 變數 | 說明 | 範例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用來產生`{ACCESS_TOKEN}`的唯一識別碼。 如需如何擷取`{CLIENT_SECRET}`的詳細資訊，請參閱[驗證及存取Experience PlatformAPI](../../../landing/api-authentication.md)的教學課程。 | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web權杖(JWT)是用於產生{ACCESS_TOKEN}的驗證認證。 如需如何產生`{JWT_TOKEN}`的相關資訊，請參閱[驗證及存取Experience PlatformAPI](../../../landing/api-authentication.md)的教學課程。 | `{JWT_TOKEN}` |
| `API_KEY` | 用於驗證對Experience Platform API的呼叫的唯一識別碼。 如需如何擷取`{API_KEY}`的詳細資訊，請參閱[驗證及存取Experience PlatformAPI](../../../landing/api-authentication.md)的教學課程。 | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成對Experience Platform API的呼叫所需的授權權杖。 如需如何擷取`{ACCESS_TOKEN}`的詳細資訊，請參閱[驗證及存取Experience PlatformAPI](../../../landing/api-authentication.md)的教學課程。 | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 關於[!DNL Marketo]，此值是固定的，並且一律設定為： `ent_dataservices_sdk`。 | `ent_dataservices_sdk` |
| `CONTAINER_ID` | `global`容器儲存所有標準Adobe和Experience Platform合作夥伴提供的類別、結構描述欄位群組、資料型別和結構描述。 關於[!DNL Marketo]，此值是固定的，且一律設為`global`。 | `global` |
| `PRIVATE_KEY` | 用來驗證您的[!DNL Postman]執行個體以Experience PlatformAPI的認證。 請參閱有關設定開發人員主控台和[設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md)的教學課程，以瞭解如何擷取{PRIVATE_KEY}的說明。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用來整合至Adobe I/O的認證。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系統(IMS)提供驗證Adobe服務的架構。 關於[!DNL Marketo]，此值是固定的，且一律設為： `ims-na1.adobelogin.com`。 | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 企業實體，可以擁有或授權產品及服務並允許存取其成員。 如需如何擷取`{ORG_ID}`資訊的說明，請參閱[設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md)的教學課程。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您正在使用的虛擬沙箱分割的名稱。 | `prod` |
| `TENANT_ID` | ID，用來確保您建立的資源已正確命名且包含在您的組織內。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您對其進行API呼叫的URL端點。 此值是固定的，且一律設為： `http://platform.adobe.io/`。 | `http://platform.adobe.io/` |
| `munchkinId` | 您的[!DNL Marketo]帳戶的唯一識別碼。 如需如何擷取`munchkinId`的詳細資訊，請參閱[驗證您的 [!DNL Marketo] 執行個體](../adobe-applications/marketo/marketo-auth.md)的教學課程。 | `123-ABC-456` |
| `sfdc_org_id` | 您的[!DNL Salesforce]帳戶的組織識別碼。 請參閱下列[[!DNL Salesforce] 指南](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1)，以取得您[!DNL Salesforce]組織ID的詳細資訊。 | `00D4W000000FgYJUA0` |
| `has_abm` | 表示您是否訂閱[!DNL Marketo Account-Based Marketing]的布林值。 | `false` |
| `has_msi` | 表示您是否訂閱[!DNL Marketo Sales Insight]的布林值。 | `false` |

{style="table-layout:auto"}

### 執行指令碼

設定好[!DNL Postman]集合和環境後，您現在可以透過[!DNL Postman]介面執行指令碼。

在[!DNL Postman]介面中，選取自動產生器公用程式的根資料夾，然後從頂端標題選取&#x200B;**[!DNL Run]**。

![根資料夾](../../images/tutorials/create/salesforce/root-folder.png)

[!DNL Runner]介面出現。 從這裡，確定已選取所有核取方塊，然後選取&#x200B;**[!DNL Run Namespaces and Schemas Autogeneration Utility]**。

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

成功的請求會根據測試版規格建立B2B名稱空間和結構描述。

## 使用API連線[!DNL Salesforce]至平台

以下檔案提供如何使用API或使用者介面將[!DNL Salesforce]連線到Platform的資訊：

- [使用Flow Service API建立Salesforce基本連線](../../tutorials/api/create/crm/salesforce.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為CRM來源建立資料流](../../tutorials/api/collect/crm.md)

## 使用UI連線[!DNL Salesforce]至平台

- [在使用者介面中建立Salesforce來源連線](../../tutorials/ui/create/crm/salesforce.md)
- [在UI中為CRM連線建立資料流](../../tutorials/ui/dataflow/crm.md)
