---
keywords: Experience Platform；首頁；熱門主題；crm結構；crm;CRM;Salesforce;Salesforce
solution: Experience Platform
title: Salesforce源連接器概述
description: 了解如何使用API或使用者介面將Salesforce連線至Adobe Experience Platform。
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# [!DNL Salesforce] 連接器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

Experience Platform支援從協力廠商CRM系統擷取資料。 支援CRM提供者包括 [!DNL Salesforce].

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 欄位對應來源 [!DNL Salesforce] 到XDM

在 [!DNL Salesforce] 平台， [!DNL Salesforce] 將來源資料欄位擷取至Platform之前，必須先對應至其適當的目標XDM欄位。

請參閱下列內容，以取得關於 [!DNL Salesforce] 資料集和Platform:

- [聯繫人](../adobe-applications/mapping/salesforce.md#contact)
- [銷售機會](../adobe-applications/mapping/salesforce.md#lead)
- [帳戶](../adobe-applications/mapping/salesforce.md#account)
- [機會](../adobe-applications/mapping/salesforce.md#opportunity)
- [機會聯繫人角色](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campaigns](../adobe-applications/mapping/salesforce.md#campaign)
- [促銷活動成員](../adobe-applications/mapping/salesforce.md#campaign-member)
- [帳戶聯繫關係](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## 設定 [!DNL Salesforce] 命名空間和架構自動生成實用程式

若要使用 [!DNL Salesforce] 源作為 [!DNL B2B-CDP]，您必須先設定 [!DNL Postman] 自動產生 [!DNL Salesforce] 命名空間和結構。 下列檔案提供設定 [!DNL Postman] 實用程式：

- 您可以從此下載命名空間和架構自動產生公用程式集合及環境 [GitHub存放庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- 如需使用Platform API的詳細資訊，包括如何收集必要標題的值以及讀取範例API呼叫的詳細資訊，請參閱 [Platform API快速入門](../../../landing/api-guide.md).
- 如需如何產生Platform API認證的詳細資訊，請參閱 [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md).
- 有關如何設定的資訊 [!DNL Postman] 若為Platform API，請參閱以下的教學課程： [設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md).

使用Platform開發人員主控台和 [!DNL Postman] 設定後，您現在可以開始將適當的環境值套用至 [!DNL Postman] 環境。

下表包含範例值，以及填入 [!DNL Postman] 環境：

| 變數 | 說明 | 範例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用來產生您 `{ACCESS_TOKEN}`. 請參閱 [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以了解如何擷取 `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token(JWT)是用於生成{ACCESS_TOKEN}的驗證憑據。 請參閱 [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以了解如何產生 `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | 用來驗證對Experience PlatformAPI呼叫的唯一識別碼。 請參閱 [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以了解如何擷取 `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成對Experience PlatformAPI的呼叫所需的授權Token。 請參閱 [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以了解如何擷取 `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 關於 [!DNL Marketo]，此值已修正，且一律設為： `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 此 `global` 容器包含所有標準Adobe和Experience Platform合作夥伴提供的類、架構欄位組、資料類型和架構。 關於 [!DNL Marketo]，此值會固定且一律設為 `global`. | `global` |
| `PRIVATE_KEY` | 用於驗證您的 [!DNL Postman] 例項來Experience PlatformAPI。 請參閱設定開發人員主控台的教學課程，以及 [設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md) 有關如何檢索{PRIVATE_KEY}的說明。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用於整合到Adobe I/O的憑據。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系統(IMS)提供Adobe服務驗證的架構。 關於 [!DNL Marketo]，此值已修正，且一律設為： `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 擁有或許可產品和服務並允許訪問其成員的公司實體。 請參閱 [設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md) 有關如何檢索 `{ORG_ID}` 資訊。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您使用的虛擬沙箱分區的名稱。 | `prod` |
| `TENANT_ID` | 用來確保您建立的資源命名正確，且包含在組織中的ID。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您進行API呼叫的URL端點。 此值已修正，且一律設為： `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | 您 [!DNL Marketo] 帳戶。 請參閱 [驗證 [!DNL Marketo] 執行個體](../adobe-applications/marketo/marketo-auth.md) 以了解如何擷取 `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | 組織ID [!DNL Salesforce] 帳戶。 請參閱下列內容 [[!DNL Salesforce] 指南](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) 如需有關 [!DNL Salesforce] 組織ID。 | `00D4W000000FgYJUA0` |
| `has_abm` | 布林值，指出您是否訂閱 [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | 布林值，指出您是否被切換至 [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### 執行指令碼

使用 [!DNL Postman] 集合和環境設定後，您現在可以透過 [!DNL Postman] 介面。

在 [!DNL Postman] 介面，選擇自動生成器實用程式的根資料夾，然後選擇 **[!DNL Run]** 從頂端標題。

![根資料夾](../../images/tutorials/create/salesforce/root-folder.png)

此 [!DNL Runner] 介面。 從此處，確保選中所有複選框，然後選中 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![運行生成器](../../images/tutorials/create/salesforce/run-generator.png)

成功的要求會根據測試版規格建立B2B命名空間和結構。

## Connect [!DNL Salesforce] 使用API到平台

以下檔案提供如何連線的資訊 [!DNL Salesforce] 若要使用API或使用者介面來建立平台：

- [使用流服務API建立Salesforce基本連接](../../tutorials/api/create/crm/salesforce.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流服務API為CRM源建立資料流](../../tutorials/api/collect/crm.md)

## Connect [!DNL Salesforce] 使用UI設為Platform

- [在UI中建立Salesforce來源連線](../../tutorials/ui/create/crm/salesforce.md)
- [在UI中為CRM連線建立資料流](../../tutorials/ui/dataflow/crm.md)
