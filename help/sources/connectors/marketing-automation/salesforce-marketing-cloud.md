---
solution: Experience Platform
title: SalesforceMarketing Cloud源概覽
description: 瞭解如何使用API或用戶介面將SalesforceMarketing Cloud連接到Adobe Experience Platform。
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

Experience Platform支援從第三方營銷自動化系統接收資料。 對營銷自動化提供商的支援包括 [!DNL Salesforce Marketing Cloud]。

## 先決條件

在連接之前 [!DNL Salesforce Marketing Cloud] 源到平台，必須確保 **權限作用域** 已預配給 [!DNL Salesforce Marketing Cloud] 客戶端ID和客戶端密碼組合：

* `campaign_read`
* `list_and_subscribers_read`

通過調用 `v2/userinfo` 資源 [!DNL Salesforce Marketing Cloud] API。 查看 [[!DNL Salesforce Marketing Cloud] API整合權限作用域文檔](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) 有關如何請求和比較範圍的指導。

有關作用域（包括其相關權限和行為的清單）的詳細資訊，請參閱 [[!DNL Salesforce Marketing Cloud] REST API文檔](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>)。

>[!IMPORTANT]
>
>當前不支援自定義對象攝取 [!DNL Salesforce Marketing Cloud] 源整合。

## IP地址允許清單

在使用源連接器之前，必須將IP地址清單添加到允許清單。 如果無法將特定於區域的IP地址添加到允許清單，則在使用源時可能會導致錯誤或效能不佳。 查看 [IP地址允許清單](../../ip-address-allow-list.md) 的子菜單。

## 連接 [!DNL Salesforce Marketing Cloud] 到使用API的平台

以下文檔提供了有關如何連接的資訊 [!DNL Salesforce Marketing Cloud] 到使用API的平台：

* [使用流服務API建立SalesforceMarketing Cloud基連接](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [使用流服務API瀏覽資料表](../../tutorials/api/explore/tabular.md)
* [使用流服務API為市場營銷自動化源建立資料流](../../tutorials/api/collect/marketing-automation.md)

## 連接 [!DNL Salesforce Marketing Cloud] 到使用UI的平台

以下文檔提供了有關如何連接的資訊 [!DNL Salesforce Marketing Cloud] 到使用用戶介面的平台：

* [在UI中建立SalesforceMarketing Cloud源連接](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [在UI中為市場營銷自動化源連接建立資料流](../../tutorials/ui/dataflow/marketing-automation.md)
