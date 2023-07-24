---
title: SAP Commerce來源概觀
description: 瞭解如何使用API或使用者介面將SAP Commerce連線至Adobe Experience Platform。
last-substantial-update: 2023-07-26T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 99edb8b2bcd4225235038e966a367d91375c961a
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>此 [!DNL SAP Commerce] 來源為測試版。 請參閱 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html)，SAP客戶體驗產品組合中提供適用於B2B和B2C企業的雲端型電子商務平台解決方案。 [[!DNL SAP] 訂閱帳單](https://www.sap.com/products/financial-management/subscription-billing.html) 是產品組合中的產品，透過標準化的整合，透過簡化的銷售與付款體驗，實現完整的訂閱生命週期管理。

此 [!DNL SAP Commerce] 來源可讓您將客戶和聯絡人資訊從 [[!DNL SAP] 訂閱帳單](https://www.sap.com/products/financial-management/subscription-billing.html) 以下業務合作夥伴API端點：

* [客戶](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [連絡人](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

此外，如果 [!DNL SAP Commerce] 執行以擷取客戶資料， [客戶 — 聯絡人關係](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) 也會呼叫API以擷取客戶的聯絡資訊。

## IP位址允許清單 {#ip-allow-list}

在使用來源聯結器之前，可能需要將IP位址清單新增到允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 先決條件 {#prerequisites}

在帶上 [!DNL SAP Commerce] 要Experience Platform的資料，您必須先確定您具備下列專案：

* A [!DNL SAP Subscription Billing] 帳戶。 如果您還沒有有效的帳單帳戶，請連絡您的 [!DNL SAP] 客戶經理。 請參閱 [[!DNL SAP] 平台設定](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) 其他詳細資料的檔案。

* [!DNL SAP] 服務金鑰。 此 [!DNL SAP] 服務金鑰可讓您存取 [!DNL SAP Subscription Billing] 透過Experience Platform的API。 [!DNL SAP Commerce] 需要下列項目:
   * 使用者端ID
   * 使用者端密碼
   * URL. URL模式如下： `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. 此值稍後將用於取得 `region` 和 `tokenEndpoint` 當您 [建立基本連線](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) 使用API或當您使用 [連線您的 [!DNL SAP Commerce] 帳戶](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) 透過Platform UI。

+++選取以檢視服務金鑰的範例

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

## 後續步驟

以下檔案提供有關如何連線的資訊 [!DNL SAP Commerce] 使用API或使用者介面的to Platform：

* [建立來源連線和資料流以帶來 [!DNL SAP Commerce] 使用API將資料匯入Platform](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [連線您的 [!DNL SAP Commerce] 要使用UIExperience Platform的帳戶](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [使用UI為來源建立資料流](../../tutorials/ui/dataflow/ecommerce.md)
