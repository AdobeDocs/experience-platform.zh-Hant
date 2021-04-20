---
keywords: Experience Platform；描述檔；即時客戶描述檔；疑難排解；API；同意；同意；偏好；偏好；privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing；同意；同意
title: 同意與偏好資料類型
description: 「同意隱私權、個人化和行銷偏好」資料類型旨在支援收集「同意管理平台」(CMP)和其他來源自您資料作業產生的客戶權限和偏好。
topic: guide
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
translation-type: tm+mt
source-git-commit: 4e9395b4551842cf75b0d1a4ec36c85930c42da5
workflow-type: tm+mt
source-wordcount: '1838'
ht-degree: 1%

---

# [!DNL Consents & Preferences] 資料類型

[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences]資料類型（以下稱為「[!DNL Consents & Preferences]資料類型」）是[!DNL Experience Data Model](XDM)資料類型，旨在支援收集「同意管理平台」(CMP)和您資料作業的其他來源所產生的客戶權限和偏好。

本檔案涵蓋[!DNL Consents & Preferences]資料類型所提供欄位的結構和用途。

## 先決條件 {#prerequisites}

本文檔需要對XDM和[!DNL Experience Platform]中方案的使用有正確的理解。 請先閱讀下列檔案，然後再繼續：

* [XDM系統概述](http://www.adobe.com/go/xdm-home-en)
* [架構構成基礎](http://www.adobe.com/go/xdm-schema-best-practices-en)

## 資料類型結構{#structure}

>[!IMPORTANT]
>
>[!DNL Consents & Preferences]資料類型旨在涵蓋一系列許可和優先管理使用案例。 因此，本檔案以一般術語說明資料類型欄位的使用，並僅就您應如何解讀這些欄位提供建議。 請洽詢您的隱私權法律團隊，讓資料類型的結構與您的組織如何解讀及向客戶展示這些同意和偏好選擇保持一致。

[!DNL Consents & Preferences]資料類型提供了幾個用於捕獲&#x200B;**connency**&#x200B;和&#x200B;**preference**&#x200B;資訊的欄位。

同意是允許客戶指定其資料的使用方式的選項。 大部分同意具有法律意義，因為有些司法轄區需要取得許可才能以特定方式使用資料，或要求客戶有權在不需要同意的情況下停止該使用（選擇退出）。

偏好設定選項可讓客戶指定如何處理其品牌體驗的不同方面。 這分為兩類：

* **個人化偏好設定**:關於品牌應如何個人化傳遞給客戶的體驗的偏好設定。
* **行銷偏好設定**:關於品牌是否允許透過各種管道與客戶聯絡的偏好設定。

下列螢幕擷取顯示資料類型結構在平台UI中的呈現方式：

![](../images/data-types/consents.png)

>[!TIP]
>
>請參閱[探索XDM資源](../ui/explore.md)指南，以瞭解如何在平台UI中查找任何XDM資源並檢查其結構的步驟。

以下JSON顯示[!DNL Consents & Preferences]資料類型可處理的資料類型範例。 以下各節提供了有關這些欄位具體使用情況的資訊。

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "adID": {
      "val": "VI"
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "u"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>您可以針對您在Experience Platform中定義的任何XDM結構，產生範例JSON資料，以協助視覺化您應如何對應客戶同意和偏好資料。 如需詳細資訊，請參閱下列檔案：
>
>* [在UI中產生範例資料](../ui/sample.md)
>* [在API中產生範例資料](../api/sample-data.md)


## `consents` {#choices}

`consents` 包含數個欄位，說明客戶的同意與偏好。以下子節將詳細說明這些欄位。

```json
"consents": {
  "collect": {
    "val": "y",
  },
  "adID": {
    "val": "VI"
  },
  "share": {
    "val": "y",
  },
  "personalize": {
    "content": {
      "val": "y"
    }
  },
  "marketing": {
    "preferred": "email",
    "any": {
      "val": "u"
    },
    "email": {
      "val": "n",
      "reason": "Too Frequent",
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### `collect`

`collect` 代表客戶對收集其資料的同意。

```json
"collect" : {
  "val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `val` | 客戶為此使用案例提供的許可選擇。 有關接受的值和定義，請參見[附錄](#choice-values)。 |

### `adID`

`adID` 代表客戶同意廣告商ID（IDFA或GAID）是否可用於連結此裝置上各應用程式的客戶。

```json
"adID" : {
  "val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `val` | 客戶為此使用案例提供的許可選擇。 有關接受的值和定義，請參見[附錄](#choice-values)。 |

### `share`

`share` 代表客戶同意其資料是否可與第二方或第三方共用（或銷售給）。

```json
"share" : {
  "val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `val` | 客戶為此使用案例提供的許可選擇。 有關接受的值和定義，請參見[附錄](#choice-values)。 |

### `personalize` {#personalize}

`personalize` 擷取客戶偏好設定，以瞭解他們的資料可以透過哪些方式個人化。客戶可以選擇退出特定的個人化使用案例，或完全退出個人化。

>[!IMPORTANT]
>
>`personalize` 不涵蓋行銷使用案例。例如，如果客戶退出所有通道的個人化，他們不應停止透過這些通道接收通信。 相反，他們收到的訊息應該是通用的，而不是根據他們的個人檔案。
>
>同樣，如果客戶退出所有通道的直接行銷（透過[下一節](#marketing)說明），即使允許個人化，該客戶也不應收到任何訊息。`marketing`

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `content` | 代表客戶對您網站或應用程式中個人化內容的偏好。 |
| `val` | 指定使用案例的客戶提供的個人化偏好設定。 如果客戶不需要獲得許可，則此欄位的值應指明個人化的發生基礎。 有關接受的值和定義，請參見[附錄](#choice-values)。 |

### `marketing` {#marketing}

`marketing` 擷取客戶對其資料可用於哪些行銷目的的偏好。客戶可以選擇退出特定的行銷使用案例，或完全退出直接行銷。

```json
"marketing": {
  "preferred": "email",
  "any": {
    "val": "u"
  },
  "email": {
    "val": "n",
    "reason": "Too Frequent"
  },
  "push": {
    "val": "y"
  },
  "sms": {
    "val": "y"
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `preferred` | 指出客戶首選的接收通信渠道。 有關接受的值，請參見[附錄](#preferred-values)。 |
| `any` | 代表客戶對整體直接行銷的偏好。 此欄位中提供的同意偏好設定會視為任何行銷管道的「預設」偏好設定，除非以`marketing`下提供的其他子欄位覆寫。 如果您打算使用更詳細的同意選項，建議您排除此欄位。<br><br>如果值設為，則 `n`應忽略所有更具體的個人化設定。如果值設為`y`，則所有更精細的個人化選項也應視為`y`，除非明確設為`n`。 如果未設定值，則每個個人化選項的值都應依指定的方式接受。 |
| `email` | 指出客戶是否同意接收電子郵件訊息。 |
| `push` | 指出客戶是否允許接收推播通知。 |
| `sms` | 指出客戶是否同意接收簡訊。 |
| `val` | 客戶提供的指定使用案例偏好設定。 如果客戶不需要獲得許可，則此欄位的值應指明應根據何種基礎進行市場營銷使用案例。 有關接受的值和定義，請參見[附錄](#choice-values)。 |
| `time` | 行銷偏好設定變更時的ISO 8601時間戳記（如果適用）。 請注意，如果任何個別偏好設定的時間戳記與`metadata`下提供的時間戳記相同，則不會針對該偏好設定設定此欄位。 |
| `reason` | 當客戶退出行銷使用案例時，此字串欄位代表客戶退出的原因。 |

### `metadata`

`metadata` 每當客戶的同意和偏好上次更新時，都會擷取一般中繼資料。

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| 屬性 | 說明 |
| --- | --- |
| `time` | 上次更新客戶同意和偏好設定時的ISO 8601時間戳記。 此欄位可用來取代將時間戳記套用至個別偏好設定，以降低負載和複雜性。 在個別偏好設定下提供`time`值會覆寫該特定偏好設定的`metadata`時間戳記。 |

## 使用資料類型{#ingest}接收資料

若要使用[!DNL Consents & Preferences]資料類型從客戶收集同意資料，您必鬚根據包含該資料類型的架構來建立資料集。

有關如何將資料類型分配給欄位的步驟，請參閱[在UI](http://www.adobe.com/go/xdm-schema-editor-tutorial-en)中建立模式的教程。 建立包含[!DNL Consents & Preferences]資料類型的欄位的模式後，請參閱資料集使用手冊中[建立dataset](../../catalog/datasets/user-guide.md#create)的部分，按照使用現有模式建立資料集的步驟操作。

>[!IMPORTANT]
>
>如果要向[!DNL Real-time Customer Profile]發送許可資料，則必鬚根據包含[!DNL Consents & Preferences]資料類型的[!DNL XDM Individual Profile]類建立啟用[!DNL Profile]的模式。 您基於該模式建立的資料集也必須為[!DNL Profile]啟用。 請參閱上述連結的教學課程，以取得與架構和資料集的[!DNL Real-time Customer Profile]需求相關的特定步驟。
>
>此外，您還必須確保您的合併策略已配置為優先順序包含最新同意和偏好資料的資料集，以便正確更新客戶個人檔案。 有關詳細資訊，請參閱[合併策略](../../rtcdp/profile/merge-policies.md)的概述。

## 處理同意和偏好變更

當客戶在您的網站上變更其同意或偏好設定時，應使用[Adobe Experience Platform網頁SDK](../../edge/consent/supporting-consent.md)來收集並立即執行這些變更。 如果客戶退出資料收集，所有資料收集必須立即停止。 如果客戶退出個人化，那麼他們造訪的下一頁上應該不會出現個人化。

## 附錄 {#appendix}

以下各節提供有關[!DNL Consents & Preferences]資料類型的其他參考資訊。

### `val` {#choice-values}的接受值

下表概述`val`的接受值：

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是 | 客戶已選擇同意或偏好。 換言之，他們&#x200B;**do**&#x200B;同意使用其資料，如有關同意或偏好所示。 |
| `n` | 無 | 客戶已選擇不同意或拒絕。 換言之，他們&#x200B;**不**&#x200B;同意使用其資料，如所述同意或偏好所示。 |
| `p` | 待覈實 | 該系統尚未獲得最終同意或優惠值。 這通常是需要兩步驟驗證的同意的一部分。 例如，如果客戶選擇接收電子郵件，則該同意會設為`p`，直到他們在電子郵件中選擇連結以確認他們提供了正確的電子郵件地址，此時該同意會更新為`y`。<br><br>如果此許可或偏好不使用兩組驗證流程，則該選 `p` 擇可用於指示客戶尚未響應許可提示。例如，您可以在客戶回應同意提示之前，自動將網站第一頁的值設為`p`。 在不需要明確同意的司法管轄區中，您也可以使用該司法管轄區來指出客戶未明確選擇退出（換言之，假定同意）。 |
| `u` | 未知 | 客戶的同意或偏好資訊未知。 |
| `LI` | 合法利益 | 收集並處理資料以達到特定目的的正當商業利益，比其對個人的潛在傷害要大。 |
| `CT` | 合約 | 為達到特定目的而收集資料，是為了履行與個人的合同義務。 |
| `CP` | 遵守法律義務 | 為達到特定目的而收集資料，是為了履行企業的法律義務。 |
| `VI` | 個人的切身利益 | 為了保護個人的切身利益，必須收集符合特定目的的資料。 |
| `PI` | 公共利益 | 為特定目的收集資料，是為了公共利益或行使官方權力而執行的。 |

### `preferred` {#preferred-values}的接受值

下表概述`preferred`的接受值：

| 值 | 說明 |
| --- | --- |
| `email` | 電子郵件訊息. |
| `push` | 推播通知. |
| `inApp` | 應用程式內訊息. |
| `sms` | SMS 訊息. |
| `phone` | 電話通話互動。 |
| `phyMail` | 實體郵件。 |
| `inVehicle` | 車內訊息。 |
| `inHome` | 在家留言。 |
| `iot` | 物聯網(IoT)消息。 |
| `social` | 社交媒體內容。 |
| `other` | 不符合標準類別的渠道。 |
| `none` | 無首選渠道。 |
| `unknown` | 首選通道未知。 |

### 完整[!DNL Consents & Preferences]方案{#full-schema}

要查看[!DNL Consents & Preferences]資料類型的完整模式，請參閱[正式的XDM儲存庫](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json)。
