---
solution: Experience Platform
title: 同意和首選項架構欄位組
topic-legacy: overview
description: 本文檔概述了「同意」和「首選項」架構欄位組。
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '2317'
ht-degree: 2%

---

# [!UICONTROL 同意和] 偏好欄位組

[!UICONTROL 同意和]偏好設定是類別 [[!DNL XDM Individual Profile] 的標準欄](../../classes/individual-profile.md)位群組，用來擷取客戶同意和偏好設定資訊。

>[!NOTE]
>
>由於此欄位組僅與[!DNL XDM Individual Profile]相容，因此不能用於[!DNL XDM ExperienceEvent]架構。 如果您想在「體驗事件」結構中包含同意和偏好設定資料，請改為使用[自訂欄位群組](../../ui/resources/field-groups.md#create)，將[[!UICONTROL 隱私權、個人化和行銷偏好設定的同意]資料類型](../../data-types/consents.md)新增至結構。

## 欄位群組結構 {#structure}

>[!IMPORTANT]
>
>「[!UICONTROL 同意」和「首選項」欄位組旨在涵蓋一系列同意和首選項管理使用案例。 ]因此，本檔案以一般術語說明欄位群組欄位的使用，並僅就您應如何解讀這些欄位的使用提出建議。 請洽詢您的隱私權法律團隊，使欄位群組的結構與您的組織解讀方式一致，並向客戶呈現這些同意和偏好選擇。

「[!UICONTROL 同意」和「首選項」欄位組提供幾個欄位，用於捕獲&#x200B;**同意**&#x200B;和&#x200B;**首選項**&#x200B;資訊。]

同意是可讓客戶指定其資料的使用方式的選項。 大部分同意都有法律層面，因為有些管轄區需要取得許可才能以特定方式使用資料，或要求客戶有權在不需要肯定同意的情況下停止該使用（選擇退出）。

偏好設定是可讓客戶指定如何處理其品牌體驗不同方面的選項。 這分為兩類：

* **個人化偏好設定**:品牌如何個人化傳遞給客戶的體驗的相關偏好設定。
* **行銷偏好設定**:關於品牌是否允許透過各種管道聯絡客戶的偏好設定。

下列螢幕擷圖顯示在Platform UI中呈現欄位群組結構的方式：

![](../../images/field-groups/consent.png)

>[!TIP]
>
>請參閱[探索XDM資源](../../ui/explore.md)的指南，了解如何在Platform UI中尋找任何XDM資源並檢查其結構的步驟。

以下JSON顯示[!UICONTROL 同意和偏好設定]欄位組可處理的資料類型範例。 以下各節將提供有關這些欄位具體用途的資訊。

```json
{
  "consents": {
    "collect": {
      "val": "VI"
    },
    "share": {
      "val": "y"
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "email": {
        "val": "y"
      }
    },
    "idSpecific": {
      "ECID": {
        "37784337855396895622558625508046772577": {
          "adID": {
            "val": "n",
          },
          "share": {
            "val": "n"
          },
          "marketing": {
            "push": {
              "val": "n",
              "time": "2020-09-30T01:02:33+00:00",
              "reason": "not relevant"
            }
          }
        }
      },
      "email": {
        "john@xyz.com": {
          "marketing": {
            "email": {
              "val": "y"
            }
          }
        }
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
>您可以為在Experience Platform中定義的任何XDM結構產生範例JSON資料，以便將客戶同意和偏好設定資料的對應方式視覺化呈現。 如需詳細資訊，請參閱下列檔案：
>
>* [在UI中產生範例資料](../../ui/sample.md)
* [在API中產生範例資料](../../api/sample-data.md)


## 欄位使用案例

以下各節提供這些欄位的預期使用案例。

### `collect`

`collect` 代表客戶同意收集其資料。

```json
"collect" : {
  "val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `val` | 此使用案例由客戶提供的同意選擇。 有關接受的值和定義，請參閱[附錄](#choice-values)。 |

{style=&quot;table-layout:auto&quot;}

### `share`

`share` 代表客戶同意其資料可與第二方或第三方共用（或銷售給）。

```json
"share" : {
  "val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `val` | 此使用案例由客戶提供的同意選擇。 有關接受的值和定義，請參閱[附錄](#choice-values)。 |

{style=&quot;table-layout:auto&quot;}

### `personalize` {#personalize}

`personalize` 擷取客戶偏好設定，以了解其資料可用於個人化的方式。客戶可以選擇退出特定的個人化使用案例，或完全選擇退出個人化。

>[!IMPORTANT]
`personalize` 不涵蓋行銷使用案例。例如，如果客戶選擇退出所有管道的個人化，他們不應停止透過這些管道接收通訊。 相反，他們收到的訊息應是一般訊息，而非根據其設定檔。
在相同範例中，如果客戶選擇退出所有管道的直接行銷（透過`marketing`，說明於[下一節](#marketing)中），則即使允許個人化，該客戶也不應收到任何訊息。

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `content` | 代表客戶對您網站或應用程式上個人化內容的偏好設定。 |
| `val` | 指定使用案例的客戶提供個人化偏好設定。 在不需要提示客戶提供同意的情況下，此欄位的值應指出進行個人化的基礎。 有關接受的值和定義，請參閱[附錄](#choice-values)。 |

{style=&quot;table-layout:auto&quot;}

### `marketing` {#marketing}

`marketing` 擷取客戶對其資料可用於哪些行銷目的的偏好設定。客戶可以選擇退出特定的行銷使用案例，或完全退出直接行銷。

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
| `preferred` | 指示客戶用於接收通信的首選通道。 如需接受的值，請參閱[附錄](#preferred-values)。 |
| `any` | 代表客戶對整體直接行銷的偏好。 此欄位中提供的同意偏好設定被視為任何行銷管道的「預設」偏好設定，除非以`marketing`下提供的其他子欄位覆寫。 如果您打算使用更精細的同意選項，建議您排除此欄位。<br><br>如果值設為，則 `n`應忽略所有更具體的個人化設定。如果值設為`y`，則所有更精細的個人化選項也應視為`y`，除非明確設為`n`。 如果值未設定，則每個個人化選項的值應接受指定的值。 |
| `email` | 指出客戶是否同意接收電子郵件訊息。 客戶也可以針對此管道中的個別訂閱提供偏好設定。 如需詳細資訊，請參閱下方的[訂閱](#subscriptions)區段。 |
| `push` | 指出客戶是否允許接收推播通知。 客戶也可以針對此管道中的個別訂閱提供偏好設定。 如需詳細資訊，請參閱下方的[訂閱](#subscriptions)區段。 |
| `sms` | 指示客戶是否同意接收簡訊。 客戶也可以針對此管道中的個別訂閱提供偏好設定。 如需詳細資訊，請參閱下方的[訂閱](#subscriptions)區段。 |
| `val` | 客戶提供的指定使用案例偏好設定。 如果不必提示客戶提供同意，此欄位的值應指出進行行銷使用案例的基礎。 有關接受的值和定義，請參閱[附錄](#choice-values)。 |
| `time` | 行銷偏好設定變更時的ISO 8601時間戳記（若適用）。 請注意，如果任何個別偏好設定的時間戳記與`metadata`下提供的時間戳記相同，則不會為該偏好設定設定此欄位。 |
| `reason` | 當客戶選擇退出行銷使用案例時，此字串欄位代表客戶選擇退出的原因。 |

{style=&quot;table-layout:auto&quot;}

#### `subscriptions` {#subscriptions}

`marketing`物件的`email`、`push`和`sms`屬效能夠代表這些個別管道的客戶訂閱。 若要這麼做，請將`subscriptions`屬性新增至相關的行銷管道。

```json
"marketing": {
  "email": {
    "val": "y",
    "subscriptions": {
      "daily-mail": {
        "val": "y",
        "type": "paid",
        "subscribers": {
          "john@xyz.com": {
            "time": "2019-01-01T15:52:25+00:00",
            "source": "website"
          }
        }
      },
      "shipped": {
        "val": "y",

        "subscribers": {
          "john@xyz.com": {
            "time": "2021-01-01T08:32:53+07:00",
            "source": "website"
          },
          "jane@xyz.com": {
            "time": "2020-02-03T07:54:21+07:00",
            "source": "call center",
          }
        }
      }
    }
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `type` | 訂閱類型。 這可以是任何描述性字串，但須為15個或更少字元。 |
| `subscribers` | 可選的地圖類型欄位，代表已訂閱特定訂閱的一組識別碼（例如電子郵件地址或電話號碼）。 此物件中的每個索引鍵代表相關的識別碼，並包含兩個子屬性： <ul><li>`time`:身分訂閱時的ISO 8601時間戳記（若適用）。</li><li>`source`:訂閱者源。這可以是任何描述性字串，但須為15個或更少字元。</li></ul> |

{style=&quot;table-layout:auto&quot;}


### `metadata`

`metadata` 擷取客戶上次更新時同意和偏好設定的一般中繼資料。

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| 屬性 | 說明 |
| --- | --- |
| `time` | 上次更新客戶同意和偏好設定時的ISO 8601時間戳記。 您可以使用此欄位，而非將時間戳記套用至個別偏好設定，以減少負載和複雜性。 在單個首選項下提供`time`值將覆蓋該特定首選項的`metadata`時間戳。 |

{style=&quot;table-layout:auto&quot;}

### `idSpecific`

`idSpecific` 特定同意或偏好設定並非普遍適用於客戶，但僅限於單一裝置或ID時，才可使用。例如，客戶可以選擇不接收某個地址的電子郵件，同時允許另一個地址的電子郵件。

>[!IMPORTANT]
管道層級同意和偏好設定（即`idSpecific`以外於`consents`下方提供的同意和偏好設定）適用於該管道內的ID。 因此，無論是採用等同的ID或裝置專屬設定，所有通道層級的同意和偏好設定都會直接生效：
* 如果客戶已在管道層級選擇退出，則會忽略`idSpecific`中的任何等同同意或偏好設定。
* 如果未設定管道層級同意或偏好設定，或客戶已選擇加入，則會遵循`idSpecific`中的同等同意或偏好設定。


`idSpecific`物件中的每個索引鍵代表Adobe Experience Platform Identity Service所識別的特定身分命名空間。 雖然您可以定義自己的自訂命名空間，將不同的識別碼分類，但建議您使用Identity Service提供的其中一個標準命名空間，以減少「即時客戶設定檔」的儲存大小。 如需身分識別命名空間的詳細資訊，請參閱身分識別服務檔案中的[身分識別命名空間概述](../../../identity-service/namespaces.md)。

每個命名空間對象的鍵都表示客戶為其設定首選項的唯一標識值。 每個標識值都可以包含一組完整的同意和首選項，格式與`consents`相同。

```json
"idSpecific": {
  "email": {
    "jdoe@example.com": {
      "marketing": {
        "email": {
          "val": "n"
        }
      }
    }
  },
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

在`idSpecific`區段中提供的`marketing`物件中，不支援`any`和`preferred`欄位。 這些欄位只能在使用者層級設定。 此外，`email`、`sms`和`push`的`idSpecific`行銷偏好設定不支援`subscriptions`欄位。

`idSpecific`區段中也只能提供同意：`adID`。 以下小節將介紹此欄位。

#### `adID`

`adID`同意代表客戶同意是否可使用廣告商ID（IDFA或GAID）來連結此裝置上各應用程式的客戶。 此值只能在`idSpecific`區段的`ECID`身分命名空間下配置，無法為其他命名空間或此欄位組的用戶級別設定。

```json
"idSpecific": {
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

>[!NOTE]
您不需要直接設定此值，因為Adobe Experience Platform Mobile SDK會在適當時自動設定。

## 使用欄位群組擷取資料 {#ingest}

若要使用[!UICONTROL 同意和偏好設定]欄位群組來內嵌客戶的同意資料，您必鬚根據包含該欄位群組的結構來建立資料集。

有關如何將欄位群組指派至欄位的步驟，請參閱有關在UI](http://www.adobe.com/go/xdm-schema-editor-tutorial-en)中建立架構的[教學課程。 建立含有欄位（[!UICONTROL 同意與偏好設定]欄位群組）的架構後，請依照使用現有架構建立資料集的步驟，參閱資料集使用指南中[建立資料集](../../../catalog/datasets/user-guide.md#create)的區段。

>[!IMPORTANT]
如果要將同意資料發送到[!DNL Real-time Customer Profile]，則需要根據[!DNL XDM Individual Profile]類建立啟用[!DNL Profile]的架構，該類包含[!UICONTROL 「同意」和「首選項」]欄位組。 您根據該架構建立的資料集也必須為[!DNL Profile]啟用。 如需結構和資料集[!DNL Real-time Customer Profile]需求的具體步驟，請參閱上述連結的教學課程。
此外，您也必須確定合併原則的設定順序為包含最新同意和偏好設定資料的資料集優先順序，以便正確更新客戶設定檔。 有關詳細資訊，請參閱[合併策略](../../../rtcdp/profile/merge-policies.md)上的概述。

## 處理同意和偏好設定變更

當客戶在您的網站上變更其同意或偏好設定時，應使用[Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md)來收集並立即執行這些變更。 如果客戶選擇退出資料收集，則所有資料收集必須立即停止。 如果客戶選擇退出個人化，則其造訪的下一頁不應出現個人化。

## 附錄 {#appendix}

以下各節提供了有關[!UICONTROL Consents and Preferences]欄位組的附加參考資訊。

### `val`的接受值 {#choice-values}

下表概述`val`的接受值：

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是 | 客戶已選擇同意或偏好設定。 換言之，他們&#x200B;**do**&#x200B;同意使用其資料，如同意或偏好所示。 |
| `n` | 無 | 客戶已選擇退出同意或偏好設定。 換言之，他們&#x200B;**不**&#x200B;同意使用其資料，如同意或偏好所示。 |
| `p` | 待定驗證 | 系統尚未收到最終同意或偏好值。 這通常用於需要兩步驗證的同意。 例如，如果客戶選擇接收電子郵件，則該同意會設為`p`，直到客戶選擇電子郵件中的連結以確認他們提供了正確的電子郵件地址，此時同意會更新為`y`。<br><br>如果此同意或偏好設定未使用兩組驗證程式，則可 `p` 以改用該選項來指示客戶尚未響應同意提示。例如，您可以在客戶回應同意提示之前，自動將網站第一頁的值設為`p`。 在不需要明確同意的司法管轄區中，您也可以使用該司法管轄區來指出客戶尚未明確選擇退出（亦即假設同意）。 |
| `u` | 未知 | 客戶的同意或偏好設定資訊未知。 |
| `LI` | 合法利益 | 收集和處理這些資料以達到特定目的的合法商業利益，比它對個人造成的潛在傷害要大。 |
| `CT` | 合約 | 為滿足與個人的合同義務，需要收集特定用途的資料。 |
| `CP` | 遵守法律義務 | 為符合企業的法律義務，需要收集特定用途的資料。 |
| `VI` | 個人的切身利益 | 為了保護個人的切身利益，需要收集資料。 |
| `PI` | 公共利益 | 為特定目的收集資料是為了公共利益或行使官方權力而執行的。 |

{style=&quot;table-layout:auto&quot;}

### `preferred`的接受值 {#preferred-values}

下表概述`preferred`的接受值：

| 值 | 說明 |
| --- | --- |
| `email` | 電子郵件訊息. |
| `push` | 推播通知. |
| `inApp` | 應用程式內訊息. |
| `sms` | 簡訊訊息. |
| `phone` | 電話呼叫互動。 |
| `phyMail` | 實物郵件。 |
| `inVehicle` | 車內資訊。 |
| `inHome` | 內部訊息。 |
| `iot` | 物聯網報文。 |
| `social` | 社交媒體內容。 |
| `other` | 不符合標準類別的管道。 |
| `none` | 無首選通道。 |
| `unknown` | 首選通道未知。 |

{style=&quot;table-layout:auto&quot;}

### 完整[!UICONTROL 同意和偏好設定]架構 {#full-schema}

若要檢視[!UICONTROL 同意和偏好設定]欄位群組的完整架構，請參閱[官方XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json)。
