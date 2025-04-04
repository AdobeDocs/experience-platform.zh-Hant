---
title: SAP Commerce Source概觀
description: 瞭解如何使用API或使用者介面將SAP Commerce連線至Adobe Experience Platform。
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 3%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>[!DNL SAP Commerce]來源是測試版。 如需使用Beta版標示來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html)是適用於B2B與B2C企業的雲端型電子商務平台解決方案，屬於SAP客戶體驗產品組合的一部分。 [[!DNL SAP] 訂閱帳單](https://www.sap.com/products/financial-management/subscription-billing.html)是產品組合下的產品，可透過標準化的整合，透過簡化的銷售和付款體驗來啟用完整的訂閱生命週期管理。

[!DNL SAP Commerce]來源可讓您從下列[[!DNL SAP] 訂閱帳單](https://www.sap.com/products/financial-management/subscription-billing.html)商業夥伴API端點，將客戶和連絡人資訊擷取到Experience Platform：

* [客戶](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [連絡人](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

此外，如果執行[!DNL SAP Commerce]以擷取客戶資料，也會呼叫[客戶聯絡人關係](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) API以擷取客戶的聯絡資訊。

## IP位址允許清單 {#ip-allow-list}

使用來源聯結器之前，可能需要將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 先決條件 {#prerequisites}

在將[!DNL SAP Commerce]資料帶入Experience Platform之前，您必須先確定您具備下列條件：

* [!DNL SAP Subscription Billing]帳戶。 如果您還沒有有效的帳單帳戶，請連絡您的[!DNL SAP]帳戶管理員。 如需其他詳細資訊，請參閱[[!DNL SAP] 平台組態](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf)檔案。

* [!DNL SAP]服務金鑰。 [!DNL SAP]服務金鑰可讓您透過Experience Platform存取[!DNL SAP Subscription Billing] API。 [!DNL SAP Commerce] 需要下列項目:
   * 用戶端 ID
   * 用戶端密碼
   * URL。 URL模式如下： `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`。 當您使用API [建立基礎連線](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection)或透過Experience Platform UI [連線您的 [!DNL SAP Commerce] 帳戶](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account)時，此值稍後將用於取得`region`和`tokenEndpoint`的值。

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

以下檔案提供如何使用API或使用者介面將[!DNL SAP Commerce]連線至Experience Platform的資訊：

* [使用API建立來源連線和資料流，將 [!DNL SAP Commerce] 資料匯入Experience Platform](../../tutorials/api/create/ecommerce/sap-commerce.md)。
* [使用UI](../../tutorials/ui/create/ecommerce/sap-commerce.md)將您的 [!DNL SAP Commerce] 帳戶連線至Experience Platform。
* [使用UI為來源建立資料流](../../tutorials/ui/dataflow/ecommerce.md)
