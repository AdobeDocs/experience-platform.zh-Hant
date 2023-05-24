---
title: SugarCRM源概述
description: 瞭解如何使用API或用戶介面將SugarCRM連接到Adobe Experience Platform。
badge: β
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# (Beta) [!DNL SugarCRM]

>[!NOTE]
>
>的 [!DNL SugarCRM] 源為beta。 查看 [源概述](../../home.md#terms-and-conditions) 的子菜單。

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

Experience Platform支援從第三方CRM應用程式接收資料。 對CRM提供程式的支援包括 [!DNL SugarCRM]。

[[!DNL SugarCRM]](https://www.sugarcrm.com/) 是一種客戶關係管理系統。 [!DNL SugarCRM]其功能包括銷售人員自動化，營銷活動，客戶支援，協作，移動CRM, Social CRM和報告。

的 [!DNL SugarCRM] 源允許您從以下API終結點中接收帳戶、聯繫人和事件資料：

* [帳戶](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [聯繫人](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [事件](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)


[!DNL SugarCRM] 使用承載令牌作為與通信的驗證機制 [!DNL SugarCRM] 帳戶和聯繫API以及 [!DNL SugarCRM] 事件API。

## IP地址允許清單

在使用源連接器之前，必須將IP地址清單添加到允許清單。 如果無法將特定於區域的IP地址添加到允許清單，則在使用源時可能會導致錯誤或效能不佳。 查看 [IP地址允許清單](../../ip-address-allow-list.md) 的子菜單。

## 先決條件

在建立 [!DNL SugarCRM] 源連接，必須首先確保您具有以下功能：

* A [!DNL SugarMarket] 帳戶。 必須聯繫 [!DNL SugarCRM] 帳戶經理獲取有效 [!DNL SugarMarket] 帳戶。

* 唯一的API用戶名和密碼與與市場營銷或銷售流程關聯的任何用戶帳戶分開。 此唯一的用戶名和密碼組合必須具有API訪問權限。 有關設定帳戶的流程的詳細資訊，請訪問 [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) 文檔。

## 連接 [!DNL SugarCRM Accounts & Contacts] 到平台

* [建立源連接以 [!DNL SugarCRM Accounts & Contacts] 使用API向平台發送資料](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md)。
* [建立源連接以 [!DNL SugarCRM Accounts & Contacts] 使用用戶介面向平台發送資料](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md)。
* [使用流服務API為CRM源建立資料流](../../tutorials/api/collect/crm.md)


## 連接 [!DNL SugarCRM Events] 到平台

* [建立源連接以 [!DNL SugarCRM Events] 使用API向平台發送資料](../../tutorials/api/create/crm/sugarcrm-events.md)。
* [建立源連接以 [!DNL SugarCRM Events] 使用用戶介面向平台發送資料](../../tutorials/ui/create/crm/sugarcrm-events.md)。
* [在UI中為CRM源連接建立資料流](../../tutorials/ui/dataflow/crm.md)
