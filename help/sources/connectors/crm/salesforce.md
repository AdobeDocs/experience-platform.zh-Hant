---
keywords: Experience Platform；首頁；熱門主題；crm架構；crm;CRM;salesforce;Salesforce
solution: Experience Platform
title: Salesforce源連接器概述
description: 瞭解如何使用API或用戶介面將Salesforce連接到Adobe Experience Platform。
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# [!DNL Salesforce] 連接器

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

Experience Platform支援從第三方CRM系統接收資料。 對CRM提供程式的支援包括 [!DNL Salesforce]。

## IP地址允許清單

在使用源連接器之前，必須將IP地址清單添加到允許清單。 如果無法將特定於區域的IP地址添加到允許清單，則在使用源時可能會導致錯誤或效能不佳。 查看 [IP地址允許清單](../../ip-address-allow-list.md) 的子菜單。

## 欄位映射自 [!DNL Salesforce] 到XDM

建立源連接 [!DNL Salesforce] 平台， [!DNL Salesforce] 在將源資料欄位納入平台之前，必須將其映射到相應的目標XDM欄位。

有關在以下位置之間的欄位映射規則的詳細資訊，請參閱以下 [!DNL Salesforce] 資料集和平台：

- [聯繫人](../adobe-applications/mapping/salesforce.md#contact)
- [銷售線索](../adobe-applications/mapping/salesforce.md#lead)
- [帳戶](../adobe-applications/mapping/salesforce.md#account)
- [機會](../adobe-applications/mapping/salesforce.md#opportunity)
- [機會聯繫人角色](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [行銷活動](../adobe-applications/mapping/salesforce.md#campaign)
- [市場活動成員](../adobe-applications/mapping/salesforce.md#campaign-member)
- [帳戶聯繫人關係](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## 設定 [!DNL Salesforce] 命名空間和架構自動生成實用程式

使用 [!DNL Salesforce] 源作為一部分 [!DNL B2B-CDP]，必須先設定 [!DNL Postman] 用於自動生成 [!DNL Salesforce] 命名空間和架構。 以下文檔提供了有關設定 [!DNL Postman] 實用程式：

- 可以從此下載命名空間和架構自動生成實用程式集合及環境 [GitHub儲存庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility)。
- 有關使用平台API的資訊，包括有關如何收集所需標頭值和讀取示例API調用的詳細資訊，請參閱上的指南 [平台API入門](../../../landing/api-guide.md)。
- 有關如何為平台API生成憑據的資訊，請參見上的教程 [驗證和訪問Experience PlatformAPI](../../../landing/api-authentication.md)。
- 有關如何設定的資訊 [!DNL Postman] 有關平台API，請參見上的教程 [設定開發人員控制台和 [!DNL Postman]](../../../landing/postman.md)。

使用平台開發人員控制台和 [!DNL Postman] 設定後，您現在可以開始將適當的環境值應用到 [!DNL Postman] 環境。

下表包含示例值以及有關填充 [!DNL Postman] 環境：

| 變數 | 說明 | 範例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用於生成您的 `{ACCESS_TOKEN}`。 請參閱上的教程 [驗證和訪問Experience PlatformAPI](../../../landing/api-authentication.md) 有關如何檢索 `{CLIENT_SECRET}`。 | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web令牌(JWT)是用於生成{ACCESS_TOKEN}的身份驗證憑據。 請參閱上的教程 [驗證和訪問Experience PlatformAPI](../../../landing/api-authentication.md) 有關如何生成 `{JWT_TOKEN}`。 | `{JWT_TOKEN}` |
| `API_KEY` | 用於驗證對Experience PlatformAPI的調用的唯一標識符。 請參閱上的教程 [驗證和訪問Experience PlatformAPI](../../../landing/api-authentication.md) 有關如何檢索 `{API_KEY}`。 | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成對Experience PlatformAPI的調用所需的授權令牌。 請參閱上的教程 [驗證和訪問Experience PlatformAPI](../../../landing/api-authentication.md) 有關如何檢索 `{ACCESS_TOKEN}`。 | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 關於 [!DNL Marketo]，此值是固定的，並且始終設定為： `ent_dataservices_sdk`。 | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 的 `global` 容器包含所有標準Adobe和Experience Platform夥伴提供的類、架構欄位組、資料類型和架構。 關於 [!DNL Marketo]，此值是固定的，始終設定為 `global`。 | `global` |
| `PRIVATE_KEY` | 用於驗證您的 [!DNL Postman] 實例到Experience PlatformAPI。 請參閱有關設定開發人員控制台和 [設定開發人員控制台和 [!DNL Postman]](../../../landing/postman.md) 有關如何檢索{PRIVATE_KEY}的說明。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用於整合到Adobe I/O的憑據。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系統(IMS)為Adobe服務提供了驗證框架。 關於 [!DNL Marketo]，此值是固定的，並且始終設定為： `ims-na1.adobelogin.com`。 | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 擁有或許可產品和服務並允許訪問其成員的公司實體。 請參閱上的教程 [設定開發人員控制台和 [!DNL Postman]](../../../landing/postman.md) 有關如何檢索 `{ORG_ID}` 的下界。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您正在使用的虛擬沙盒分區的名稱。 | `prod` |
| `TENANT_ID` | 用於確保建立的資源名稱正確且包含在組織中的ID。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 要對其進行API調用的URL終結點。 此值是固定的，始終設定為： `http://platform.adobe.io/`。 | `http://platform.adobe.io/` |
| `munchkinId` | 您的唯一ID [!DNL Marketo] 帳戶。 請參閱上的教程 [驗證 [!DNL Marketo] 實例](../adobe-applications/marketo/marketo-auth.md) 有關如何檢索 `munchkinId`。 | `123-ABC-456` |
| `sfdc_org_id` | 您的組織ID [!DNL Salesforce] 帳戶。 請參閱以下內容 [[!DNL Salesforce] 引導](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) 有關獲取 [!DNL Salesforce] 組織ID。 | `00D4W000000FgYJUA0` |
| `has_abm` | 一個布爾值，它指示您是否已訂閱 [!DNL Marketo Account-Based Marketing]。 | `false` |
| `has_msi` | 一個布爾值，它指示是否將您 [!DNL Marketo Sales Insight]。 | `false` |

{style="table-layout:auto"}

### 運行指令碼

與 [!DNL Postman] 設定集合和環境，您現在可以通過 [!DNL Postman] 。

在 [!DNL Postman] 介面，選擇自動生成器實用程式的根資料夾，然後選擇 **[!DNL Run]** 的下界。

![根資料夾](../../images/tutorials/create/salesforce/root-folder.png)

的 [!DNL Runner] 對話框。 在此處，確保選中所有複選框，然後選擇 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**。

![運行發電機](../../images/tutorials/create/salesforce/run-generator.png)

成功的請求根據測試版規範建立B2B命名空間和架構。

## 連接 [!DNL Salesforce] 到使用API的平台

以下文檔提供了有關如何連接的資訊 [!DNL Salesforce] 到使用API或用戶介面的平台：

- [使用流服務API建立Salesforce基連接](../../tutorials/api/create/crm/salesforce.md)
- [使用流服務API瀏覽資料表](../../tutorials/api/explore/tabular.md)
- [使用流服務API為CRM源建立資料流](../../tutorials/api/collect/crm.md)

## 連接 [!DNL Salesforce] 到使用UI的平台

- [在UI中建立Salesforce源連接](../../tutorials/ui/create/crm/salesforce.md)
- [在UI中為CRM連接建立資料流](../../tutorials/ui/dataflow/crm.md)
