---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;consent;Consent;preferences;Preferences;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;consent;Consent
title: 同意與偏好資料類型
description: 「隱私權／行銷偏好（同意）」資料類型旨在支援收集「同意管理平台」(CMPs)和您資料作業中其他來源產生的客戶權限和偏好。
topic: guide
translation-type: tm+mt
source-git-commit: 1a4dd167ecd4f4f61ffe26af786b355e4561b30d
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 1%

---


# [!DNL Consents & Preferences] 資料類型

資 [!DNL Privacy/Marketing Preferences (Consent)] 料類型（以下稱為「資料類型」）是[!DNL Consents & Preferences][!DNL Experience Data Model] (XDM)資料類型，旨在支援收集「同意管理平台」(CMPs)和您資料作業中其他來源產生的客戶權限和偏好。

本檔案涵蓋資料類型所提供欄位的結構與 [!DNL Consents & Preferences] 用途。

## 先決條件 {#prerequisites}

本文檔需要對XDM和中的架構的使用有良好的瞭解 [!DNL Experience Platform]。 請先閱讀下列檔案，然後再繼續：

* [XDM系統概述](http://www.adobe.com/go/xdm-home-en)
* [架構構成基礎](http://www.adobe.com/go/xdm-schema-best-practices-en)

## 資料類型結構 {#structure}

>[!IMPORTANT]
>
>資料 [!DNL Consents & Preferences] 類型設計為涵蓋一系列許可和優先管理使用案例。 因此，本檔案以一般術語說明資料類型欄位的使用，並僅就您應如何解讀這些欄位提供建議。 請洽詢您的隱私權法律團隊，讓資料類型的結構與您的組織如何解讀及向客戶展示這些同意和偏好選擇保持一致。

資料 [!DNL Consents & Preferences] 類型提供數個欄位，用於擷取 **同意** 和 **偏好資訊** 。

同意是允許客戶指定其資料的使用方式的選項。 大部分同意具有法律意義，因為有些司法轄區需要取得許可才能以特定方式使用資料，或要求客戶有權在不需要同意的情況下停止該使用（選擇退出）。

偏好設定選項可讓客戶指定如何處理其品牌體驗的不同方面。 這分為兩類：

* **個人化偏好設定**:關於品牌應如何個人化傳遞給客戶的體驗的偏好設定。
* **行銷偏好設定**:關於品牌是否允許透過各種管道與客戶聯絡的偏好設定。

下列JSON顯示資料類型可處理之資料類 [!DNL Consents & Preferences] 型的範例。 以下各節提供了有關這些欄位具體使用情況的資訊。

```json
{
  "xdm:consents": {
    "xdm:collect": {
      "xdm:val": "y",
    },
    "xdm:adID": {
      "xdm:val": "VI"
    },
    "xdm:share": {
      "xdm:val": "y",
    },
    "xdm:personalize": {
      "xdm:any": {
        "xdm:val": "y",
      },
      "xdm:content": {
        "xdm:val": "y"
      }
    },
    "xdm:marketing": {
      "xdm:preferred": "email",
      "xdm:any": {
        "xdm:val": "u"
      },
      "xdm:push": {
        "xdm:val": "n",
        "xdm:reason": "Too Frequent",
        "xdm:time": "2019-01-01T15:52:25+00:00"
      }
    },
    "xdm:idSpecific": {
      "email": {
        "jdoe@example.com": {
          "xdm:marketing": {
            "xdm:email": {
              "xdm:val": "n"
            }
          }
        }
      }
    }
  },
  "xdm:metadata": {
    "xdm:time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>上述範例旨在說明透過資料類型傳送至之資料的結構 [!DNL Platform] ，以 [!DNL Consents & Preferences] 提供本檔案其餘內容，說明資料類型所提供的主要欄位。 可在附錄中找到資料類型結構的完整模 [式](#full-schema) ，以供參考。

## xdm:consents {#choices}

`xdm:consents` 包含數個欄位，說明客戶的同意與偏好。 以下子節將詳細說明這些欄位。

```json
"xdm:consents": {
  "xdm:collect": {
    "xdm:val": "y",
  },
  "xdm:adID": {
    "xdm:val": "VI"
  },
  "xdm:share": {
    "xdm:val": "y",
  },
  "xdm:personalize": {
    "xdm:any": {
      "xdm:val": "y",
    },
    "xdm:content": {
      "xdm:val": "y"
    }
  },
  "xdm:marketing": {
    "xdm:preferred": "email",
    "xdm:any": {
      "xdm:val": "u"
    },
    "xdm:email": {
      "xdm:val": "n",
      "xdm:reason": "Too Frequent",
      "xdm:time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### xdm:collect

`xdm:collect` 代表客戶對收集其資料的同意。

```json
"xdm:collect" : {
  "xdm:val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `xdm:val` | 客戶為此使用案例提供的同意選擇。 請參閱附 [錄](#choice-values) ，瞭解接受的值和定義。 |

### xdm:adID

`xdm:adID` 代表客戶同意廣告商ID（IDFA或GAID）是否可用於連結此裝置上各應用程式的客戶。

```json
"xdm:adID" : {
  "xdm:val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `xdm:val` | 客戶為此使用案例提供的同意選擇。 請參閱附 [錄](#choice-values) ，瞭解接受的值和定義。 |

### xdm:share

`xdm:share` 代表客戶同意其資料是否可與第二方或第三方共用（或銷售給）。

```json
"xdm:share" : {
  "xdm:val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `xdm:val` | 客戶為此使用案例提供的許可選擇。 請參閱附 [錄](#choice-values) ，瞭解接受的值和定義。 |

### xdm：個人化 {#personalize}

`xdm:personalize` 擷取客戶偏好設定，以瞭解他們的資料可以透過哪些方式個人化。 客戶可以選擇退出特定的個人化使用案例，或完全退出個人化。

>[!IMPORTANT]
>
>`xdm:personalize` 不涵蓋行銷使用案例。 例如，如果客戶退出所有通道的個人化，他們不應停止透過這些通道接收通信。 相反，他們收到的訊息應該是通用的，而不是根據他們的個人檔案。
>
>同樣的範例是，如果客戶退出所有通道的直效行銷(透過下一節所述 `xdm:marketing`[](#marketing))，即使允許個人化，該客戶也不應收到任何訊息。

```json
"xdm:personalize": {
  "xdm:content": {
    "xdm:val": "y",
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `xdm:content` | 代表客戶對您網站或應用程式中個人化內容的偏好。 |
| `xdm:val` | 指定使用案例的客戶提供的個人化偏好設定。 如果客戶不需要獲得許可，則此欄位的值應指明個人化的發生基礎。 請參閱附 [錄](#choice-values) ，瞭解接受的值和定義。 |

### xdm：行銷 {#marketing}

`xdm:marketing` 擷取客戶對其資料可用於哪些行銷目的的偏好。 客戶可以選擇退出特定的行銷使用案例，或完全退出直接行銷。

```json
"xdm:marketing": {
  "xdm:preferred": "email",
  "xdm:any": {
    "xdm:val": "u"
  },
  "xdm:email": {
    "xdm:val": "n",
    "xdm:reason": "Too Frequent"
  },
  "xdm:push": {
    "xdm:val": "y"
  },
  "xdm:sms": {
    "xdm:val": "y"
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `xdm:preferred` | 指出客戶首選的接收通信渠道。 請參閱附 [錄](#preferred-values) ，瞭解接受的值。 |
| `xdm:any` | 代表客戶對整體直接行銷的偏好。 此欄位中提供的同意偏好設定會視為任何行銷管道的「預設」偏好設定，除非以下方提供的其他子欄位覆寫 `xdm:marketing`。 如果您打算使用更詳細的同意選項，建議您排除此欄位。<br><br>如果值設為，則 `n`應忽略所有更具體的個人化設定。 如果值設為，則 `y`所有更精細的個人化選項也應視為 `y`，除非明確設為 `n`。 如果未設定值，則每個個人化選項的值都應依指定的方式接受。 |
| `xdm:email` | 指出客戶是否同意接收電子郵件訊息。 |
| `xdm:push` | 指出客戶是否允許接收推播通知。 |
| `xdm:sms` | 指出客戶是否同意接收簡訊。 |
| `xdm:val` | 客戶提供的指定使用案例偏好設定。 如果客戶不需要獲得許可，則此欄位的值應指明應根據何種基礎進行市場營銷使用案例。 請參閱附 [錄](#choice-values) ，瞭解接受的值和定義。 |
| `xdm:time` | 行銷偏好設定變更時的ISO 8601時間戳記（如果適用）。 請注意，如果任何個別偏好設定的時間戳記與下方提供的時間戳記相同 `xdm:metadata`，則不會針對該偏好設定設定此欄位。 |
| `xdm:reason` | 當客戶退出行銷使用案例時，此字串欄位代表客戶退出的原因。 |

### xdm:idSpecific

`xdm:idSpecific` 當特定同意或偏好並非普遍適用於客戶，但僅限於單一裝置或ID時，即可使用。 例如，客戶可以選擇不接收某個地址的電子郵件，同時允許另一個地址發送電子郵件。

>[!IMPORTANT]
>
>頻道層級同意與偏好設定(即在外部提供 `xdm:consents` 的 `xdm:idSpecific`偏好設定)適用於該頻道的ID。 因此，不論是採用相同的ID或裝置特定設定，所有通道層級的同意和偏好設定都會直接影響：
>
>* 如果客戶已選擇退出渠道層級，則會忽略中的任何相等同意或 `xdm:idSpecific` 偏好設定。
>* 如果未設定渠道層級的同意或偏好，或客戶已選擇加入，則會遵守中的相同同意或 `xdm:idSpecific` 偏好。


物件中的每個金鑰 `xdm:idSpecific` 代表Adobe Experience Platform Identity Service所識別的特定身分名稱空間。 雖然您可以定義自己的自訂名稱空間來分類不同的識別碼，但建議您使用Identity Service提供的標準名稱空間之一來減少即時客戶個人檔案的儲存空間。 有關身份名稱空間的詳細資訊，請參 [閱Identity Service文檔中的身份名稱空間](../../identity-service/namespaces.md) 概述。

每個namespace對象的鍵代表客戶為其設定首選項的唯一標識值。 每個識別值都可以包含一組完整的同意和偏好設定，格式與相同 `xdm:consents`。

```json
"xdm:idSpecific": {
  "email": {
    "jdoe@example.com": {
      "xdm:marketing": {
        "xdm:email": {
          "xdm:val": "n"
        }
      }
    }
  }
}
```

## xdm：中繼資料

`xdm:metadata` 每當客戶的同意和偏好上次更新時，都會擷取一般中繼資料。

```json
"xdm:metadata": {
  "xdm:time": "2019-01-01T15:52:25+00:00",
}
```

| 屬性 | 說明 |
| --- | --- |
| `xdm:time` | 上次更新客戶同意和偏好的時間戳記。 此欄位可用來取代將時間戳記套用至個別偏好設定，以降低負載和複雜性。 在單個首 `xdm:time` 選項下提供值會覆蓋該特 `xdm:metadata` 定首選項的時間戳記。 |

## 使用資料類型接收資料 {#ingest}

若要使用資料類 [!DNL Consents & Preferences] 型從客戶收集同意資料，您必鬚根據包含該資料類型的架構來建立資料集。

如需如何指派資 [料類型至欄位的步驟](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) ，請參閱在UI中建立架構的教學課程。 在建立包含具有資料類型的欄位的模式後，請參 [!DNL Consents & Preferences] 閱資料集使用手冊中有關建立資料集的 [部分](../../catalog/datasets/user-guide.md#create) ，按照使用現有模式建立資料集的步驟操作。

>[!IMPORTANT]
>
>如果要向發送許可資料 [!DNL Real-time Customer Profile]，則必鬚根據包含資料類 [!DNL Profile]型的類建立啟 [!DNL XDM Individual Profile] 用的模式 [!DNL Consents & Preferences] 。 您根據該模式建立的資料集也必須啟用 [!DNL Profile]。 請參閱上述連結的教學課程，以取得與結構描述和資料集 [!DNL Real-time Customer Profile] 需求相關的特定步驟。
>
>此外，您還必須確保您的合併策略已配置為優先順序包含最新同意和偏好資料的資料集，以便正確更新客戶個人檔案。 See the overview on [merge policies](../../rtcdp/profile/merge-policies.md) for more information.

## 處理同意和偏好變更

當客戶在您的網站上變更其同意或偏好設定時，應使用 [Adobe Experience Platform Web SDK收集並立即強制執行這些變更](../../edge/consent/supporting-consent.md)。 如果客戶退出資料收集，所有資料收集必須立即停止。 如果客戶退出個人化，那麼他們造訪的下一頁上應該不會出現個人化。

## 附錄 {#appendix}

以下各節提供有關資料類型的其他 [!DNL Consents & Preferences] 參考資訊。

### xdm:val的接受值 {#choice-values}

下表概述了以下的接受值 `xdm:val`:

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是 | 客戶已選擇同意或偏好。 換言之，他們 **同意** ，如所涉同意或偏好所示，使用其資料。 |
| `n` | 無 | 客戶已選擇不同意或拒絕。 換言之，他們不 **同意** ，如有關同意或偏好所示，使用其資料。 |
| `p` | 待覈實 | 該系統尚未獲得最終同意或優惠值。 這通常是需要兩步驟驗證的同意的一部分。 例如，如果客戶選擇接收電子郵件，則該同意會設為 `p` ，直到他們在電子郵件中選擇連結以確認他們提供了正確的電子郵件地址，此時同意會更新為 `y`。<br><br>如果此許可或偏好不使用兩組驗證流程，則該選 `p` 擇可用於指示客戶尚未響應許可提示。 例如，您可以在客戶回應 `p` 同意提示之前，自動將值設為網站的第一頁。 在不需要明確同意的司法管轄區中，您也可以使用該司法管轄區來指出客戶未明確選擇退出（換言之，假定同意）。 |
| `u` | 未知 | 客戶的同意或偏好資訊未知。 |
| `LI` | 合法利益 | 收集並處理資料以達到特定目的的正當商業利益，比其對個人的潛在傷害要大。 |
| `CT` | 合約 | 為達到特定目的而收集資料，是為了履行與個人的合同義務。 |
| `CP` | 遵守法律義務 | 為達到特定目的而收集資料，是為了履行企業的法律義務。 |
| `VI` | 個人的切身利益 | 為了保護個人的切身利益，必須收集符合特定目的的資料。 |
| `PI` | 公共利益 | 為特定目的收集資料，是為了公共利益或行使官方權力而執行的。 |

### xdm:preferred的接受值 {#preferred-values}

下表概述了以下的接受值 `xdm:preferred`:

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

### 完整架 [!DNL Consents & Preferences] 構 {#full-schema}

要查看資料類型的完 [!DNL Consents & Preferences] 整模式，請參 [閱正式XDM儲存庫](https://github.com/adobe/xdm/blob/master/components/datatypes/consentpreferences.schema.json)。