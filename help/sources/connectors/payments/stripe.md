---
title: Stripe
description: 瞭解如何將Stripe帳戶的付款資料擷取至Adobe Experience Platform
badge: Beta
source-git-commit: f8df3ddb96ad0810a7a46b0a55125336c427aebd
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 1%

---

# [!DNL Stripe]

>[!NOTE]
>
>此 [!DNL Stripe] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

各種規模的數千家企業都在使用 [!DNL Stripe] 透過線上和親身參與的方式接受付款、創造新的收入來源，並透過Adobe Experience Platform、Adobe Commerce和以下協助向全球擴張 [!DNL Magento Open Source].

使用 [!DNL Stripe] Experience Platform中的來源，用於擷取客戶在購買流程期間擷取的資料。 內嵌後，即可使用此資料建立個人化優惠方案，並解鎖更豐富的商業深入分析。

>[!TIP]
>
>關於的問題 [!DNL Stripe] Experience Platform上的來源，聯絡 [!DNL Stripe] Adobe合作夥伴<span>@stripe.com.

>[!BEGINSHADEBOX]

**的範例使用案例 [!DNL Stripe] 來源**

您的企業可讓客戶在您的線上商店購買商品，選擇如下 **立即購買** 和 **稍後付款** (使用 [!DNL Klarna]， [!DNL Afterpay]， [!DNL Affirm]，或 [!DNL Zip])。

使用 [!DNL Stripe] 要分析使用的資料來源 **立即購買** 和 **稍後付款** 選項並嘗試為這些客戶提供個人化優惠方案。 例如，考慮建議使用附加元件專案，在結帳前增加購物車中的專案數量。

>[!ENDSHADEBOX]

請閱讀以下檔案，瞭解如何設定 [!DNL Stripe] 來源帳戶、擷取必要的認證，並建立您的結構描述。

## 先決條件 {#prerequisites}

以下各節提供您在連線前必須完成的先決條件設定資訊 [!DNL Stripe] 要Experience Platform的帳戶。

### 擷取您的存取權杖

* 登入 [[!DNL Stripe] 儀表板](https://dashboard.stripe.com/login) 使用您的 [!DNL Stripe] 電子郵件地址和密碼。
* 在 [!DNL Developers] 儀表板，選取 **[!DNL API keys for developers]**.
* 在 **API金鑰** 索引標籤，選取 **[!DNL Reveal test key]** 以顯示您的存取Token。
* 您現在可以在連線時將此權杖當做存取權杖 [!DNL Stripe] 要Experience Platform的帳戶，使用 [!DNL Flow Service] API或Experience Platform UI。

### 收集必要的認證

為了連線您的 [!DNL Stripe] 要Experience Platform的帳戶，您必須提供下列驗證認證的值：

>[!BEGINTABS]

>[!TAB API]

在連線時，您必須提供下列認證 [!DNL Stripe] 帳戶使用 [!DNL Flow Service] API。

| 認證 | 說明 |
| --- | --- |
| `accessToken` | 您的 [!DNL Stripe] OAuth 2重新整理程式碼驗證Token。 |
| `connectionSpec.id` | 的連線規格ID [!DNL Stripe] 來源。 此ID的固定為： `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB UI]

在連線時，您必須提供下列認證 [!DNL Stripe] 使用Experience Platform使用者介面的帳戶。

| 認證 | 說明 |
| --- | --- |
| 存取權杖 | 您的 [!DNL Stripe] OAuth 2重新整理程式碼驗證Token。 |

>[!ENDTABS]

有關使用的詳細資訊 [!DNL Stripe] API，請閱讀 [[!DNL Stripe] 有關API金鑰的檔案](https://docs.stripe.com/keys).

### 建立體驗資料模型(XDM)結構描述

此 [!DNL Stripe] 來源支援從下列資源路徑擷取資料：

* 費用
* 訂閱
* 退款
* 餘額交易
* 客戶
* 價格

您必須建立XDM結構描述來說明資料集，資料集可儲存將要傳送的欄位和資料型別 [!DNL Stripe] 以Experience Platform。

>[!BEGINTABS]

>[!TAB 費用]

在 [!DNL Stripe]， **費用** 代表將資金移入 [!DNL Stripe]. 閱讀 [[!DNL Stripe] API費用指南](https://docs.stripe.com/api/charges) 以取得特定費用屬性的詳細資訊。

+++選取以檢視Stripe費用物件

```json
{
  "id": "ch_3MmlLrLkdIwHu7ix0snN0B15",
  "object": "charge",
  "amount": 1099,
  "amount_captured": 1099,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_3MmlLrLkdIwHu7ix0uke3Ezy",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null
  },
  "calculated_statement_descriptor": "Stripe",
  "captured": true,
  "created": 1679090539,
  "currency": "usd",
  "customer": null,
  "description": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "outcome": {
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "normal",
    "risk_score": 32,
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": "card_1MmlLrLkdIwHu7ixIJwEWSNR",
  "payment_method_details": {
    "card": {
      "brand": "visa",
      "checks": {
        "address_line1_check": null,
        "address_postal_code_check": null,
        "cvc_check": null
      },
      "country": "US",
      "exp_month": 3,
      "exp_year": 2024,
      "fingerprint": "mToisGZ01V71BCos",
      "funding": "credit",
      "installments": null,
      "last4": "4242",
      "mandate": null,
      "network": "visa",
      "three_d_secure": null,
      "wallet": null
    },
    "type": "card"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xTTJKVGtMa2RJd0h1N2l4KOvG06AGMgZfBXyr1aw6LBa9vaaSRWU96d8qBwz9z2J_CObiV_H2-e8RezSK_sw0KISesp4czsOUlVKY",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source_transfer": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

+++

>[!TAB 訂閱]

在 [!DNL Stripe]，您可以使用 **訂閱** 以重複產生方式向客戶收費。 閱讀 [[!DNL Stripe] 訂閱的API指南](https://docs.stripe.com/api/subscriptions) 以取得特定訂閱屬性的詳細資訊。

+++選取以檢視Stripe訂閱物件

```json
{
  "id": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
  "object": "subscription",
  "application": null,
  "application_fee_percent": null,
  "automatic_tax": {
    "enabled": false,
    "liability": null
  },
  "billing_cycle_anchor": 1679609767,
  "billing_thresholds": null,
  "cancel_at": null,
  "cancel_at_period_end": false,
  "canceled_at": null,
  "cancellation_details": {
    "comment": null,
    "feedback": null,
    "reason": null
  },
  "collection_method": "charge_automatically",
  "created": 1679609767,
  "currency": "usd",
  "current_period_end": 1682288167,
  "current_period_start": 1679609767,
  "customer": "cus_Na6dX7aXxi11N4",
  "days_until_due": null,
  "default_payment_method": null,
  "default_source": null,
  "default_tax_rates": [],
  "description": null,
  "discount": null,
  "ended_at": null,
  "invoice_settings": {
    "issuer": {
      "type": "self"
    }
  },
  "items": {
    "object": "list",
    "data": [
      {
        "id": "si_Na6dzxczY5fwHx",
        "object": "subscription_item",
        "billing_thresholds": null,
        "created": 1679609768,
        "metadata": {},
        "plan": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "plan",
          "active": true,
          "aggregate_usage": null,
          "amount": 1000,
          "amount_decimal": "1000",
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "interval": "month",
          "interval_count": 1,
          "livemode": false,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "tiers_mode": null,
          "transform_usage": null,
          "trial_period_days": null,
          "usage_type": "licensed"
        },
        "price": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "price",
          "active": true,
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "custom_unit_amount": null,
          "livemode": false,
          "lookup_key": null,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "recurring": {
            "aggregate_usage": null,
            "interval": "month",
            "interval_count": 1,
            "trial_period_days": null,
            "usage_type": "licensed"
          },
          "tax_behavior": "unspecified",
          "tiers_mode": null,
          "transform_quantity": null,
          "type": "recurring",
          "unit_amount": 1000,
          "unit_amount_decimal": "1000"
        },
        "quantity": 1,
        "subscription": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
        "tax_rates": []
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/subscription_items?subscription=sub_1MowQVLkdIwHu7ixeRlqHVzs"
  },
  "latest_invoice": "in_1MowQWLkdIwHu7ixuzkSPfKd",
  "livemode": false,
  "metadata": {},
  "next_pending_invoice_item_invoice": null,
  "on_behalf_of": null,
  "pause_collection": null,
  "payment_settings": {
    "payment_method_options": null,
    "payment_method_types": null,
    "save_default_payment_method": "off"
  },
  "pending_invoice_item_interval": null,
  "pending_setup_intent": null,
  "pending_update": null,
  "quantity": 1,
  "schedule": null,
  "start_date": 1679609767,
  "status": "active",
  "test_clock": null,
  "transfer_data": null,
  "trial_end": null,
  "trial_settings": {
    "end_behavior": {
      "missing_payment_method": "create_invoice"
    }
  },
  "trial_start": null
}
```

+++

>[!TAB 退款]

在 [!DNL Stripe]，您可以使用 **退款** 將先前建立的費用退款。 閱讀 [[!DNL Stripe] 退款API指南](https://docs.stripe.com/api/refunds) 以取得特定退款屬性的詳細資訊。

+++選取以檢視Stripe退款物件

```json
{
  "id": "re_1Nispe2eZvKYlo2Cd31jOCgZ",
  "object": "refund",
  "amount": 1000,
  "balance_transaction": "txn_1Nispe2eZvKYlo2CYezqFhEx",
  "charge": "ch_1NirD82eZvKYlo2CIvbtLWuY",
  "created": 1692942318,
  "currency": "usd",
  "destination_details": {
    "card": {
      "reference": "123456789012",
      "reference_status": "available",
      "reference_type": "acquirer_reference_number",
      "type": "refund"
    },
    "type": "card"
  },
  "metadata": {},
  "payment_intent": "pi_1GszsK2eZvKYlo2CfhZyoZLp",
  "reason": null,
  "receipt_number": null,
  "source_transfer_reversal": null,
  "status": "succeeded",
  "transfer_reversal": null
}
```

+++

>[!TAB 餘額交易]

在 [!DNL Stripe]， **餘額交易** 代表基金在貴公司與 [!DNL Stripe] 帳戶。 閱讀 [[!DNL Stripe] 餘額交易的API指南](https://docs.stripe.com/api/balance_transactions) 以取得特定餘額交易屬性的詳細資訊。

+++選取以檢視「Stripe餘額異動」物件

```json
{
  "id": "txn_1MiN3gLkdIwHu7ixxapQrznl",
  "object": "balance_transaction",
  "amount": -400,
  "available_on": 1678043844,
  "created": 1678043844,
  "currency": "usd",
  "description": null,
  "exchange_rate": null,
  "fee": 0,
  "fee_details": [],
  "net": -400,
  "reporting_category": "transfer",
  "source": "tr_1MiN3gLkdIwHu7ixNCZvFdgA",
  "status": "available",
  "type": "transfer"
}
```

+++

>[!TAB 客戶]

在 [!DNL Stripe]， **客戶** 代表您企業的指定客戶。 如需特定客戶屬性的詳細資訊，請參閱 [[!DNL Stripe] 客戶的API指南](https://docs.stripe.com/api/customers) 以取得特定客戶屬性的詳細資訊。

+++選取以檢視StripeCustomer物件

```json
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

+++

>[!TAB 價格]

在 [!DNL Stripe]， **價格** 代表重複購買和一次性購買產品的單位成本、貨幣和可選帳單週期。 閱讀 [[!DNL Stripe] 價格的API指南](https://docs.stripe.com/api/prices) 以取得特定價格屬性的詳細資訊。

+++選取以檢視「Stripe價格」物件

```json
{
  "id": "price_1MoBy5LkdIwHu7ixZhnattbh",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1679431181,
  "currency": "usd",
  "custom_unit_amount": null,
  "livemode": false,
  "lookup_key": null,
  "metadata": {},
  "nickname": null,
  "product": "prod_NZKdYqrwEYx6iK",
  "recurring": {
    "aggregate_usage": null,
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": null,
    "usage_type": "licensed"
  },
  "tax_behavior": "unspecified",
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "recurring",
  "unit_amount": 1000,
  "unit_amount_decimal": "1000"
}
```

+++

>[!ENDTABS]


### IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

### 設定Experience Platform的許可權

您必須同時擁有兩者 **[!UICONTROL 檢視來源]** 和 **[!UICONTROL 管理來源]** 為您的帳戶啟用的許可權以連線您的 [!DNL Stripe] 要Experience Platform的帳戶。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀 [存取控制UI指南](../../../access-control/ui/overview.md).

## 後續步驟

完成先決條件設定後，您就可以繼續連線並擷取 [!DNL Stripe] 要Experience Platform的資料。 請閱讀以下指南，瞭解如何擷取 [!DNL Stripe] 使用API或使用者介面進行Experience Platform的付款資料：

* [使用流程服務API從您的Stripe帳戶擷取付款資料以Experience Platform](../../tutorials/api/create/payments/stripe.md).
* [使用使用者介面從您的Stripe帳戶擷取付款資料以Experience Platform](../../tutorials/ui/create/payments/stripe.md).