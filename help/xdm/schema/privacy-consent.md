---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;consent;Consent;preferences;Preferences;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;
solution: Adobe Experience Platform
title: 隱私權混音概觀
description: 「隱私權／行銷偏好（同意）」混合是「體驗資料模型」(XDM)混合，其目的在於支援收集CMP和其他來自客戶來源的使用者權限和偏好。 本檔案涵蓋混合程式所提供的各種欄位的結構與用途。
topic: guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 1%

---


# [!DNL Privacy Consent] mixin總覽

混 [!DNL Privacy/Marketing Preferences (Consent)] 合素（以下稱為「混合素」）是[!DNL Privacy Consent][!DNL Experience Data Model] (XDM)混合素，旨在支援由CMPs和來自客戶的其他來源產生的用戶權限和偏好的收集。 本檔案涵蓋混合程式所提供的各種欄位的結構與用途。

## 先決條件 {#prerequisites}

本文檔需要對(XDM) [!DNL Experience Data Model] 和中的方案的使用有良好的瞭解 [!DNL Experience Platform]。 請先閱讀下列檔案，然後再繼續：

* [XDM系統概述](http://www.adobe.com/go/xdm-home-en)
* [架構構成基礎](http://www.adobe.com/go/xdm-schema-best-practices-en)

## 架構示例 {#schema}

>[!NOTE]
>
>以下範例旨在說明透過 [!DNL Platform][!DNL Privacy Consent] mixin傳送至的資料結構，以便提供本檔案下一節的內容，說明mixin提供的主要欄位。 在附錄中可找到架構結構的完整 [示例](#full-schema) ，以供參考。

下列JSON顯示混合可處理之資料類 [!DNL Privacy Consent] 型的範例。 下一節將提供有關這些欄位之特定使用資訊。

```json
{
  "xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ],
  "xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  },
  "xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  },
  "xdm:version": "1.0.0",
  "xdm:timestamp": "2019-01-01T15:52:25+00:00",
  "xdm:userLocale": "UK",
  "xdm:localeSource": "ip"
}
```

## 欄位 {#fields}

以下各節介紹混音所提供之每個主要欄位的使用， [!DNL Privacy Consent] 以及其子欄位的結構。

### xdm:privacyOptOuts {#privacyOptOuts}

`xdm:privacyOptOuts` 是代表客戶所選一般退出設定的陣列。 此陣列中可包含數個物件，每個物件代表特定退出類型以及客戶為該類型選取的偏好設定。

```json
"xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ]
```

| 屬性 | 說明 |
| --- | --- |
| `xdm:optOutType` | 選擇退出的類型。 請參閱附 [錄](#optOutType-values) ，瞭解接受的值和定義。 |
| `xdm:optOutValue` | 客戶為此特定選擇退出類型選擇的選定首選項。 請參閱附 [錄](#choice-optOutValue-values) ，瞭解接受的值和定義。 |
| `xdm:timestamp` | 選擇退出偏好設定變更時的ISO 8601時間戳記（如果適用）。 |
| `xdm:basisOfProcessing` | 指出資料的收集和處理依據與隱私權相關。 依預設，此欄位會設為 `consent`，表示只有在使用者已提供同意（如所示）時才應處理資 `xdm:optOutValue`料。<br><br>在某些情況下，客戶不會被提示同意資料處理。 `xdm:basisOfProcessing` 必須包含在這些情況下的退出對象中，以說明未提供同意提示的原因。 請參閱附 [錄](#basisOfProcessing-values) ，瞭解接受的值和定義。 |

### xdm:personalizationPreferences {#personalizationPreferences}

`xdm:personalizationPreferences` 擷取客戶偏好設定，以瞭解他們的資料可以透過哪些方式個人化。 使用者可以選擇退出特定的個人化使用案例，或完全選擇退出個人化。

>[!IMPORTANT]
>
>`xdm:personalizationPreferences` 不涵蓋行銷使用案例。 例如，如果客戶選擇拒絕個人化的電子郵件，他們不會停止收到電子郵件。 相反，他們收到的電子郵件將是通用的，而不是根據他們的個人檔案。
>
>同樣，如果客戶退出電子郵件行銷(透過下一節所述 `xdm:marketingPreferences`[](#marketingPreferences))，則該客戶將不會收到任何電子郵件，即使允許電子郵件個人化亦然。

```json
"xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  }
```

| 屬性 | 說明 |
| --- | --- |
| `xdm:default` | 此物件中提供的資料代表整體客戶個人化的偏好。 |
| `xdm:details` | 一系列物件，針對客戶提供偏好的每個特定個人化類型各一個。 |
| `xdm:choice` | 客戶提供的同意偏好一般個人化，或特定個人化類型，視其是分別在下 `xdm:default` 或 `xdm:details`下提供。 請參閱附 [錄](#choice-optOutValue-values) ，瞭解接受的值和定義。 |
| `xdm:type` | 陣列中的對 `xdm:details` 像必須提供此欄位，以指明客戶為其提供許可資料的特定個人化使用案例。 請參閱附 [錄](#type-values) ，瞭解接受的值和定義。 |
| `xdm:timestamp` | 選擇退出偏好設定變更時的ISO 8601時間戳記（如果適用）。 |
| `xdm:basisOfProcessing` | 指出資料的收集和處理依據與隱私權相關。 依預設，此欄位會設為 `consent`，表示只有在使用者已提供同意（如所示）時才應處理資 `xdm:choice`料。<br><br>在某些情況下，客戶不會收到要提供個人化同意書的提示。 `xdm:basisOfProcessing` 必須包含在這些情況下的退出對象中，以說明未提供同意提示的原因。 請參閱附 [錄](#basisOfProcessing-values) ，瞭解接受的值和定義。 |


### xdm:marketingPreferences {#marketingPreferences}

`xdm:marketingPreferences` 擷取客戶對其資料可用於哪些行銷目的的偏好。 使用者可以選擇退出特定的行銷使用案例，或完全退出直接行銷。

```json
"xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  }
```

| 屬性 | 說明 |
| --- | --- |
| `xdm:default` | 此物件中提供的資料代表整體客戶對直接行銷的偏好。 |
| `xdm:details` | 一系列物件，針對客戶提供偏好的每個特定行銷使用案例提供一個物件。 |
| `xdm:choice` | 客戶提供的許可偏好一般行銷或特定行銷使用案例，視其分別是在或 `xdm:default` 下 `xdm:details`提供。 請參閱附 [錄](#choice-optOutValue-values) ，瞭解接受的值和定義。 |
| `xdm:subscriptions` | 其金鑰代表公司特定訂閱的物件，例如郵寄清單或電子報。 每個訂閱物件應接著包含 `xdm:choice` 相關訂閱的值。 |
| `xdm:type` | 陣列中的對 `xdm:details` 像必須提供此欄位，以指明客戶為其提供許可資料的具體行銷使用案例。 請參閱附 [錄](#type-values) ，瞭解接受的值和定義。 |
| `xdm:timestamp` | 選擇退出偏好設定變更時的ISO 8601時間戳記（如果適用）。 |
| `xdm:basisOfProcessing` | 指出資料的收集和處理依據與隱私權相關。 依預設，此欄位會設為 `consent`，表示只有在使用者已提供同意（如所示）時才應處理資 `xdm:choice`料。<br><br>在某些情況下，並未提示客戶同意直接行銷。 `xdm:basisOfProcessing` 必須包含在這些情況下的退出對象中，以說明未提供同意提示的原因。 請參閱附 [錄](#basisOfProcessing-values) ，瞭解接受的值和定義。 |

## 使用混合素吸收許可資料 {#ingest}

若要使用 [!DNL Privacy Consent] mixin從客戶擷取同意資料，您必須將mixin新增或現有的架構，並根據該架構建立資料集。

有關如何將混 [音新增至架構的步驟](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) ，請參閱在UI中建立架構的教學課程。 混合[!DNL  Privacy Consent] in與基於類或的方案 [!DNL XDM Individual Profile] 相容 [!DNL XDM ExperienceEvent]。

建立包含混合的模式後，請參 [!DNL Privacy Consent] 閱資料集使用手冊中有關建立資料集的 [部分](../../catalog/datasets/user-guide.md#create) ，按照使用現有模式建立資料集的步驟操作。

>[!IMPORTANT]
>
>如果您想要傳送同意資料 [!DNL Real-time Customer Profile]給，則必鬚根據包含混合的類別 [!DNL Profile]，建立啟用 [!DNL XDM Individual Profile] 的架構 [!DNL Privacy Consent] 。 您根據該模式建立的資料集也必須啟用 [!DNL Profile]。 請參閱上述教學課程，以取得與需求相關的特定 [!DNL Real-time Customer Profile] 步驟。

## 附錄 {#appendix}

以下各節提供有關混音的其他參考 [!DNL Privacy Consent] 資訊。

### xdm:optOutType的接受值 {#optOutType-values}

下表概述了以下的接受值 `xdm:optOutType`:

| 值 | 說明 |
| --- | --- |
| `general_opt_out` | 資料無法用於任何用途。 這通常會封鎖資料收集，除非處理基礎並非「同意」。<br><br>使用此選擇退出類型時，接受的值 `in` 並取 `out` 得下列內容含義：<ul><li>`in`:使用者 **已同意其資料** ，以便用於一般處理。</li><li>`out`:使用者 **不同意** ，其資料用於一般處理。</li></ul>如需詳細資訊， [請參閱xdm:optOutValue的接受值表](#choice-optOutValue-values) 。 |
| `anonymous_analysis` | 資料無法用於不需要任何類型使用者ID的一般Web量度，例如特定頁面被檢視的次數。 |
| `device_linking` | 訪客使用之某個裝置的資料無法與該訪客使用之其他裝置的資料結合。 裝置會使用常用的使用者名稱或電子郵件地址等技術進行連結，通常會透過Adobe裝置合作社或私人裝置圖表進行連結。 |
| `pseudonymous_analysis` | 資料無法用於Adobe Analytics提供的網路量度，因為Adobe Analytics需要假名ID來識別使用者透過網站（例如流失報表）的路徑、建立工作階段，以及用于歸因。 |
| `sales_sharing_opt_out` | 資料不能用於銷售用途或與第三方共用。<br><br>使用此選擇退出類型時，接受的值 `in` 並取 `out` 得下列內容含義：<ul><li>`in`:使用者 **已同意其資料** ，以便用於銷售和分享用途。</li><li>`out`:使用者 **不同意其資料** ，這些資料會用於銷售和分享用途。</li></ul>如需詳細資訊， [請參閱xdm:optOutValue的接受值表](#choice-optOutValue-values) 。 |

### xdm:basisOfProcessing的接受值 {#basisOfProcessing-values}

下表概述了以下的接受值 `xdm:basisOfProcessing`:

| 值 | 說明 |
| --- | --- |
| `consent` **（預設值）** | 允許針對指定目的收集資料，因為個人已提供明確權限。 如果未提供其他值， `xdm:basisOfProcessing` 則此為預設值。 <br><br>**重要**:只有將 `xdm:choice` 和的 `xdm:optOutValue` 值設定為時，才 `xdm:basisOfProcessing` 會使用 `consent`。 如果本表中列出的任何其他值都用於， `xdm:basisOfProcessing` 則會忽略個人的同意選擇。 |
| `compliance` | 為達到特定目的而收集資料，是為了履行企業的法律義務。 |
| `contract` | 為達到特定目的而收集資料，是為了履行與個人的合同義務。 |
| `legitimate_interest` | 收集並處理資料以達到特定目的的正當商業利益，比其對個人的潛在傷害要大。 |
| `public_interest` | 為特定目的收集資料，是為了公共利益或行使官方權力而執行的。 |
| `vital_interest` | 為了保護個人的切身利益，必須收集符合特定目的的資料。 |

### xdm:choice和xdm:optOutValue的接受值 {#choice-optOutValue-values}

下表概述和的接受 `xdm:choice` 值 `xdm:optOutValue`:

| 值 | 說明 |
| --- | --- |
| `pending` | 系統尚未從客戶處接收到許可優先資訊。 可在取得同意時用於網站的第一頁。 它也可用來表示「假定」同意，而非明確提供。 |
| `in` | 使用者已選擇同意偏好。 換言之，他們 **同意** ，如有關同意偏好所示，使用其資料。 |
| `out` | 使用者已選擇退出同意偏好。 換言之，他們 **不同意** ，如有關同意偏好所示，使用其資料。 |
| `not_applicable` | 相關的許可偏好不適用於客戶。 |
| `not_provided` | 客戶未提供任何同意偏好資訊。 |
| `unknown` | 客戶的同意偏好資訊未知。 |

### xdm:type的接受值 {#type-values}

下表概述了以下的接受值 `xdm:type`:

| 值 | 說明 |
| --- | --- |
| `ads` | 可從不相關網站檢視的廣告。 |
| `content` | 顯示在您網站上的內容。 |
| `customer_support` | 與客戶支援相關的資料。 |
| `email` | 電子郵件訊息. |
| `iot` | 與「物聯網」(IoT)相關的資料。 |
| `in_app_messages` | 應用程式內訊息. |
| `in_home` | 在家留言。 |
| `in_store` | 店內訊息。 |
| `in_vehicle` | 車內訊息。 |
| `offers` | 特別優惠。 |
| `phone_calls` | 與電話通話互動相關的資料。 |
| `push_notifications` | 推播通知. |
| `sms` | SMS 訊息. |
| `social_media` | 社交媒體內容。 |
| `snail_mail` | 通過常規郵遞發送的資訊。 |
| `third_party_content` | 您網站上顯示的由不相關實體提供的內容或文章。 |
| `third_party_offers` | 您網站廣告服務上顯示的選件或廣告，來自不相關的實體。 |

### 完整架 [!DNL Privacy Consent] 構 {#full-schema}

下列JSON代表在「結 [!DNL Privacy Consent] 構註冊表」中顯示的完整結構：

```json
{
  "meta:license": [
    "Copyright 2019 Adobe Systems Incorporated. All rights reserved.",
    "This work is licensed under a Creative Commons Attribution 4.0 International (CC BY 4.0) license",
    "you may not use this file except in compliance with the License. You may obtain a copy",
    "of the License at https://creativecommons.org/licenses/by/4.0/"
  ],
  "$id": "https://ns.adobe.com/xdm/context/consent-preferences",
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Privacy/Marketing Preferences (Consent)",
  "description": "This schema captures privacy, personalization and marketing preferences (consents).",
  "type": "object",
  "meta:extensible": true,
  "meta:abstract": true,
  "definitions": {
    "consentValue": {
      "type": "string",
      "enum": [
        "not_provided",
        "pending",
        "in",
        "out",
        "unknown",
        "not_applicable"
      ],
      "meta:enum": {
        "not_provided": "Not provided",
        "pending": "Pending verification",
        "in": "Opt-in",
        "out": "Opt-out",
        "unknown": "Unknown",
        "not_applicable": "Not Applicable"
      }
    },
    "basisOfProcessing": {
      "title": "Basis Of Processing",
      "type": "string",
      "description": "Basis of Processing",
      "enum": [
        "consent",
        "legitimate_interest",
        "contract",
        "vital_interest",
        "compliance",
        "public_interest"
      ],
      "meta:enum": {
        "consent": "User Consent",
        "legitimate_interest": "Legitimate Interest",
        "contract": "Contract",
        "vital_interest": "Vital Interest of the Individual",
        "compliance": "Compliance with a Legal Obligation",
        "public_interest": "Public Interest"
      }
    },
    "timestamp": {
      "title": "Preference timestamp",
      "description": "Timestamp of this specific opt out or preference.",
      "type": "string",
      "format": "date-time"
    },
    "consent-preferences": {
      "properties": {
        "xdm:privacyOptOuts": {
          "title": "Privacy Preferences",
          "description": "Encapsulates data privacy preferences.",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "xdm:optOutType": {
                "title": "Opt-out type",
                "type": "string",
                "description": "The type of user permission.",
                "enum": [
                  "general_opt_out",
                  "sales_sharing_opt_out",
                  "anonymous_analysis",
                  "pseudonymous_analysis",
                  "device_linking"
                ],
                "meta:enum": {
                  "general_opt_out": "General opt-out",
                  "sales_sharing_opt_out": "Sales/sharing opt-out",
                  "anonymous_analysis": "Anonymous Analysis",
                  "pseudonymous_analysis": "Pseudonymous Analysis",
                  "device_linking": "Device Linking"
                }
              },
              "xdm:optOutValue": {
                "title": "Opt Out Value",
                "description": "The value of the specific opt out.",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          }
        },
        "xdm:personalizationPreferences": {
          "title": "Personalization Preferences",
          "description": "User's Personalization Preferences",
          "type": "object",
          "properties": {
            "xdm:default": {
              "title": "Global Personalization Preferences",
              "description": "User's Default Personalization Preference",
              "type": "object",
              "properties": {
                "xdm:choice": {
                  "title": "Default Personalization Preferences Value",
                  "description": "The default value for personalization",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            },
            "xdm:details": {
              "title": "Itemized Personalization Preferences",
              "description": "Preferences for specific types of personalization",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "meta:enum": {
                    "content": "Personalize Content",
                    "in_app": "Personalize In App Messages",
                    "offers": "Personalize Offers",
                    "email": "Personalize eMail",
                    "snail_mail": "Personalize Regular Mail",
                    "phone_calls": "Personalize Phone Calls",
                    "push_notifications": "Personalize Push Notifications",
                    "sms": "Personalize SMS",
                    "customer_support": "Personalize Customer Support",
                    "in_store": "Personalize In Store",
                    "in_vehicle": "Personalize In Vehicle",
                    "in_home": "Personalize In Home",
                    "iot": "Personalize IoT",
                    "social_media": "Personalize Social Media",
                    "third_party_offers": "Personalize Third-party Offers",
                    "third_party_content": "Personalize Third-party Content",
                    "ads": "Personalize My Business's Ads on Other Sites"
                  }
                },
                "xdm:choice": {
                  "title": "Personalization Preference Value",
                  "description": "The value for this specific personalization preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            }
          }
        }
      },
      "xdm:marketingPreferences": {
        "title": "Marketing Preferences",
        "description": "User's Direct Marketing Preferences",
        "type": "object",
        "properties": {
          "xdm:default": {
            "title": "Default Direct Marketing Preference",
            "description": "User's Default Marketing Preference",
            "type": "object",
            "properties": {
              "xdm:choice": {
                "title": "Default Marketing Preferences Value",
                "description": "The default value for direct marketing preferences",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          },
          "xdm:details": {
            "title": "Itemized Direct Marketing Preferences",
            "description": "Preferences for specific types of direct marketing",
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "xdm:type": {
                  "title": "Marketing Preference",
                  "type": "string",
                  "description": "The specific marketing preference.",
                  "enum": [
                    "email",
                    "push_notifications",
                    "in_app_messages",
                    "sms",
                    "phone_calls",
                    "snail_mail",
                    "in_vehicle_messages",
                    "in_home_messages",
                    "iot",
                    "social_media"
                  ],
                  "meta:enum": {
                    "email": "Receive eMail",
                    "push_notifications": "Receive Push Notifications",
                    "in_app_messages": "Receive In App Messages",
                    "sms": "Receive SMS",
                    "phone_calls": "Receive Phone Calls",
                    "snail_mail": "Receive Regular Mail",
                    "in_vehicle_messages": "Receive In Vehicle Messages",
                    "in_home_messages": "Receive In Home Messages",
                    "iot": "Receive IoT",
                    "social_media": "Receive Social Media Messages"
                  }
                },
                "xdm:choice": {
                  "title": "Marketing Preference Value",
                  "description": "The value for this specific marketing preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                },
                "xdm:subscriptions": {
                  "title": "Company-specific subscriptions",
                  "description": "Company-specific subscriptions, such as mailing lists or newsletters",
                  "type": "object",
                  "meta:xdmType": "map",
                  "additionalProperties": {
                    "xdm:choice": {
                      "title": "Marketing Preference Value",
                      "description": "The value for this specific marketing preference",
                      "$ref": "#/definitions/consentValue"
                    },
                    "xdm:timestamp": {
                      "$ref": "#/definitions/timestamp"
                    }
                  }
                }
              }
            }
          }
        }
      },
      "xdm:timestamp": {
        "title": "Consent Preferences timestamp",
        "description": "Timestamp of the complete set of user consent preferences.",
        "type": "string",
        "format": "date-time"
      },
      "xdm:version": {
        "title": "Preferences Version",
        "description": "Version of the Privacy Preferences Standard",
        "type": "string"
      },
      "xdm:userLocale": {
        "title": "User Locale",
        "description": "User location or jurisdiction that applies to the consents for this user",
        "type": "string"
      },
      "xdm:localeSource": {
        "title": "Locale Source",
        "description": "Method used to determine the user's locale",
        "enum": [
          "ip",
          "gps",
          "user_provided",
          "website_location",
          "inferred",
          "other"
        ],
        "meta:enum": {
          "ip": "IP Address",
          "gps": "Device GPS",
          "user_provided": "User Provided",
          "website_location": "Website eTDL",
          "inferred": "Inferred",
          "other": "Other"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
    },
    {
      "$ref": "#/definitions/consent-preferences"
    }
  ],
  "meta:status": "experimental"
}
```
