---
title: SugarCRM來源概觀
description: 了解如何使用API或使用者介面將SugarCRM連線至Adobe Experience Platform。
badge: Beta
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# （測試版） [!DNL SugarCRM]

>[!NOTE]
>
>此 [!DNL SugarCRM] 來源為測試版。 請參閱 [來源概觀](../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

Experience Platform支援從協力廠商CRM應用程式擷取資料。 支援CRM提供者包括 [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) 是客戶關係管理(CRM)系統。 [!DNL SugarCRM]的功能包括銷售力量自動化、行銷活動、客戶支援、共同作業、行動CRM、社交CRM和報告。

此 [!DNL SugarCRM] 來源可讓您從下列API端點內嵌帳戶、連絡人和事件資料：

* [帳戶](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [聯繫人](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [事件](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)


[!DNL SugarCRM] 使用承載令牌作為與通信的驗證機制 [!DNL SugarCRM] 帳戶與連絡API與 [!DNL SugarCRM] 事件API。

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 先決條件

建立 [!DNL SugarCRM] 源連接時，必須首先確保您具有以下內容：

* A [!DNL SugarMarket] 帳戶。 您必須連絡 [!DNL SugarCRM] 帳戶管理員以取得有效 [!DNL SugarMarket] 帳戶（若尚未設定）。

* 與行銷或銷售程式相關聯的任何使用者帳戶不同的唯一API使用者名稱和帳戶。 此唯一的使用者名稱和帳戶組合必須具有API存取權限。 如需設定帳戶的程式詳細資訊，請造訪 [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) 檔案。

## Connect [!DNL SugarCRM Accounts & Contacts] 到平台

* [建立源連接以 [!DNL SugarCRM Accounts & Contacts] 使用API將資料傳送至平台](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [建立源連接以 [!DNL SugarCRM Accounts & Contacts] 使用者介面將資料傳送至Platform](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [使用流服務API為CRM源建立資料流](../../tutorials/api/collect/crm.md)


## Connect [!DNL SugarCRM Events] 到平台

* [建立源連接以 [!DNL SugarCRM Events] 使用API將資料傳送至平台](../../tutorials/api/create/crm/sugarcrm-events.md).
* [建立源連接以 [!DNL SugarCRM Events] 使用者介面將資料傳送至Platform](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [在UI中為CRM源連接建立資料流](../../tutorials/ui/dataflow/crm.md)
