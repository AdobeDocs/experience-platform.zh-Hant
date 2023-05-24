---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API；同意；同意；首選項；隱私；選擇；隱私；選擇；市場優先選項；選擇退出類型；基本處理；同意
title: 同意和首選項資料類型
description: 隱私、個性化和市場營銷首選項的同意資料類型旨在支援收集由同意管理平台(CMP)和您的資料操作中的其他源生成的客戶權限和首選項。
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '2034'
ht-degree: 1%

---

# [!UICONTROL 同意和首選項] 資料類型

的 [!UICONTROL 隱私、個性化和市場營銷首選項的同意] 資料類型(以下簡稱「[!UICONTROL 同意和首選項] 資料類型」是 [!DNL Experience Data Model] (XDM)資料類型，用於支援收集由同意管理平台(CMP)和資料操作中的其他源生成的客戶權限和首選項。

本檔案涵蓋了C.A.C.提供的欄位的結構和用途 [!UICONTROL 同意和首選項] 資料類型。

## 先決條件 {#prerequisites}

本文檔需要對XDM和中架構的使用有一定的瞭解 [!DNL Experience Platform]。 請在繼續之前查看以下文檔：

* [XDM 系統概觀](https://www.adobe.com/go/xdm-home-en)
* [架構組合的基礎](https://www.adobe.com/go/xdm-schema-best-practices-en)

## 資料類型結構 {#structure}

>[!IMPORTANT]
>
>的 [!UICONTROL 同意和首選項] 資料類型旨在涵蓋一系列同意和偏好管理使用案例。 因此，本文檔以一般術語描述了資料類型欄位的使用，並僅就如何解釋這些欄位的使用提出建議。 請咨詢您的隱私法律團隊，使資料類型的結構與您的組織解釋和向客戶展示這些同意和首選項選擇的方式保持一致。

的 [!UICONTROL 同意和首選項] 資料類型提供了幾個用於捕獲的欄位 **同意** 和 **偏好** 的下界。

同意是允許客戶指定如何使用其資料的選項。 大多數同意具有法律方面，因為某些管轄區要求在資料能夠以特定方式使用之前獲得許可，或者要求客戶有權在不需要正面同意的情況下停止使用（選擇退出）。

首選項是一種選項，允許客戶指定如何處理其品牌體驗的不同方面。 這分為兩類：

* **個性化首選項**:有關品牌如何個性化向客戶交付的體驗的首選項。
* **市場營銷首選項**:有關品牌是否允許通過各種渠道與客戶聯繫的首選項。

以下螢幕快照顯示了資料類型結構在平台UI中的表示方式：

![](../images/data-types/consents.png)

>[!TIP]
>
>請參閱上的指南 [探索XDM資源](../ui/explore.md) 有關如何查找任何XDM資源並檢查其在平台UI中的結構的步驟。

以下JSON顯示以下資料類型的示例： [!UICONTROL 同意和首選項] 資料類型可以處理。 以下各節提供了有關這些欄位具體用途的資訊。

```json
{
  "consents": {
    "collect": {
      "val": "VI",
    },
    "adID": {
      "idType": "IDFA",
      "val": "y"
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
>您可以為在Experience Platform中定義的任何XDM架構生成示例JSON資料，以幫助直觀地顯示客戶同意和首選項資料的映射方式。 有關詳細資訊，請參閱以下文檔：
>
>* [在UI中生成示例資料](../ui/sample.md)
>* [在API中生成示例資料](../api/sample-data.md)


## `consents` {#choices}

`consents` 包含幾個描述客戶同意和首選項的欄位。 以下各小節對這些欄位作了進一步詳細說明。

```json
"consents": {
  "collect": {
    "val": "VI",
  },
  "adID": {
    "idType": "IDFA",
    "val": "y"
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

`collect` 表示客戶同意收集其資料。

```json
"collect": {
  "val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `val` | 客戶為此使用案例提供的同意選擇。 查看 [附錄](#choice-values) 以獲取接受的值和定義。 |

{style="table-layout:auto"}

### `adID`

`adID` 表示客戶同意是否可以使用廣告商ID將客戶連結到此設備上的應用。

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `idType` | 廣告ID類型 `IDFA` Apple廣告商或 `GAID` 用於Google的廣告商ID，也稱為Android廣告商ID(AAID)。 |
| `val` | 客戶為此使用案例提供的同意選擇。 查看 [附錄](#choice-values) 以獲取接受的值和定義。 |

{style="table-layout:auto"}

### `share`

`share` 表示客戶同意其資料是否可以與（或出售給）第二方或第三方共用。

```json
"share": {
  "val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `val` | 客戶為此使用案例提供的同意選擇。 查看 [附錄](#choice-values) 以獲取接受的值和定義。 |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` 捕獲客戶的首選項，以確定其資料可以通過哪些方式用於個性化。 客戶可以選擇退出特定的個性化使用案例，或完全退出個性化。

>[!IMPORTANT]
>
>`personalize` 不包括營銷用例。 例如，如果客戶退出所有渠道的個性化設定，則他們不應停止通過這些渠道接收通信。 相反，他們收到的消息應是泛型的，而不是基於他們的個人資料。
>
>同一示例中，如果客戶選擇不直接營銷所有渠道(通過 `marketing`，在 [下一部分](#marketing))，則該客戶不應接收任何消息，即使允許個性化。

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `content` | 表示客戶對網站或應用程式上的個性化內容的首選項。 |
| `val` | 客戶提供的指定用例的個性化首選項。 如果客戶不需要提示其同意，則此欄位的值應指明個性化設定的依據。 查看 [附錄](#choice-values) 以獲取接受的值和定義。 |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing` 捕獲客戶對其資料可用於哪些市場營銷目的的偏好。 客戶可以選擇退出特定的營銷使用案例，或完全退出直接營銷。

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
| `preferred` | 指示客戶接收通信的首選通道。 查看 [附錄](#preferred-values) 為接受的值。 |
| `any` | 代表客戶對直接營銷的總體偏好。 此欄位中提供的同意首選項被視為任何市場營銷渠道的「預設」首選項，除非由下面提供的附加子欄位覆蓋 `marketing`。 如果您計畫使用更細粒度的同意選項，建議您排除此欄位。<br><br>如果值設定為 `n`，則應忽略所有更具體的個性化設定。 如果值設定為 `y`，則所有更細粒度的個性化選項也應視為 `y`，除非顯式設定 `n`。 如果取消設定值，則應按指定的方式處理每個個性化選項的值。 |
| `email` | 指示客戶是否同意接收電子郵件。 |
| `push` | 指示客戶是否允許接收推送通知。 |
| `sms` | 指示客戶是否同意接收文本消息。 |
| `val` | 客戶提供的指定使用案例的首選項。 如果客戶不需要提示其同意，則此欄位的值應指明進行市場營銷使用案例的依據。 查看 [附錄](#choice-values) 以獲取接受的值和定義。 |
| `time` | ISO 8601時間戳（如果適用），顯示當市場營銷首選項發生更改時。 請注意，如果任何單個首選項的時間戳與下面提供的時間戳相同 `metadata`，則不為該首選項設定此欄位。 |
| `reason` | 當客戶從市場營銷使用案例中選擇時，此字串欄位表示客戶選擇退出的原因。 |

{style="table-layout:auto"}

### `metadata`

`metadata` 捕獲有關客戶上次更新時的同意和首選項的常規元資料。

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| 屬性 | 說明 |
| --- | --- |
| `time` | 上次更新客戶的任何同意和首選項的ISO 8601時間戳。 可以使用此欄位，而不是將時間戳應用到單個首選項以減少負載和複雜性。 提供 `time` 單個首選項下的值將覆蓋 `metadata` 特定首選項的時間戳。 |

{style="table-layout:auto"}

## 使用資料類型接收資料 {#ingest}

為了使用 [!UICONTROL 同意和首選項] 資料類型從客戶處接收同意資料，必須基於包含該資料類型的架構建立資料集。

請參閱上的教程 [在UI中建立架構](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) 有關如何將資料類型分配給欄位的步驟。 建立包含域的架構後 [!UICONTROL 同意和首選項] 資料類型，請參閱 [建立資料集](../../catalog/datasets/user-guide.md#create) 在dataset使用手冊中，按照使用現有模式建立資料集的步驟進行操作。

>[!IMPORTANT]
>
>如果要將同意資料發送到 [!DNL Real-Time Customer Profile]，需要建立 [!DNL Profile]-enabled方案，基於 [!DNL XDM Individual Profile] 包含 [!UICONTROL 同意和首選項] 資料類型。 您基於該架構建立的資料集也必須為 [!DNL Profile]。 請參閱上面連結的教程，瞭解與 [!DNL Real-Time Customer Profile] 模式和資料集的要求。
>
>此外，您還必須確保將合併策略配置為將包含最新同意和首選項資料的資料集優先化，以便正確更新客戶配置檔案。 請參閱 [合併策略](../../rtcdp/profile/merge-policies.md) 的子菜單。

## 處理同意和首選項更改

當客戶在您的網站上更改其同意或首選項時，應收集這些更改並立即使用 [Adobe Experience PlatformWeb SDK](../../edge/consent/supporting-consent.md)。 如果客戶從資料收集中退出，則必須立即停止所有資料收集。 如果客戶選擇取消個性化，則他們訪問的下一頁上不應顯示個性化。

## 附錄 {#appendix}

以下各節提供了有關 [!UICONTROL 同意和首選項] 資料類型。

### 接受的值 `val` {#choice-values}

下表概述了 `val`:

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是（選擇加入） | 客戶已選擇同意或優先。 換句話說， **做** 同意使用有關同意或偏好所表示的資料。 |
| `n` | 否（選擇退出） | 客戶已選擇不同意或拒絕。 換句話說， **不** 同意使用有關同意或偏好所表示的資料。 |
| `p` | 等待驗證 | 系統尚未收到最終同意或偏好值。 這通常是需要兩步驗證的同意的一部分。 例如，如果客戶選擇接收電子郵件，則該同意設定為 `p` 直到他們在電子郵件中選擇一個連結以驗證他們是否提供了正確的電子郵件地址，此時將將同意更新為 `y`。<br><br>如果此同意或首選項不使用兩組驗證過程，則 `p` 而可以使用choice指示客戶尚未響應同意提示。 例如，可以自動將值設定為 `p` 在客戶響應同意提示之前，在網站的首頁上。 在不需要明確同意的管轄區中，您也可以使用它來指示客戶沒有明確選擇不加入（換句話說，假定同意）。 |
| `u` | 未知 | 客戶的同意或偏好資訊未知。 |
| `dy` | 預設為是（選中） | 客戶本身並未提供同意值，預設情況下會被視為選擇加入（「是」）。 換句話說，在客戶另有說明之前，將假定同意。<br><br>請注意，如果法律或公司隱私策略的更改導致某些或所有用戶的預設值發生更改，則必須手動更新包含預設值的所有配置檔案。 |
| `dn` | 預設值為「否」（選擇退出） | 客戶本身並未提供同意值，預設情況下被視為退出（「否」）。 換句話說，假定客戶在表示不同意之前拒絕同意。<br><br>請注意，如果法律或公司隱私策略的更改導致某些或所有用戶的預設值發生更改，則必須手動更新包含預設值的所有配置檔案。 |
| `LI` | 合法利益 | 收集和處理此資料以達到指定目的的合法商業利益超過其對個人的潛在傷害。 |
| `CT` | 合同 | 為了履行與個人的合同義務，需要為特定目的收集資料。 |
| `CP` | 遵守法律義務 | 為履行企業的法律義務，需要為特定目的收集資料。 |
| `VI` | 個人的切身利益 | 為了保護個人的切身利益，需要為特定目的收集資料。 |
| `PI` | 公共利益 | 為特定目的收集資料，是為了公共利益或行使官方權力而執行一項任務。 |

{style="table-layout:auto"}

### 接受的值 `preferred` {#preferred-values}

下表概述了 `preferred`:

| 值 | 說明 |
| --- | --- |
| `email` | 電子郵件 messages. |
| `push` | 推播通知. |
| `inApp` | 應用程式內訊息. |
| `sms` | 簡訊訊息. |
| `phone` | 電話通話。 |
| `phyMail` | 郵件。 |
| `inVehicle` | 車內資訊。 |
| `inHome` | 家中留言。 |
| `iot` | 物聯網消息。 |
| `social` | 社交媒體內容。 |
| `other` | 不適合標準類別的渠道。 |
| `none` | 沒有首選通道。 |
| `unknown` | 首選通道未知。 |

{style="table-layout:auto"}

### 滿 [!UICONTROL 同意和首選項] 架構 {#full-schema}

查看的完整架構 [!UICONTROL 同意和首選項] 資料類型，請參閱 [正式XDM儲存庫](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json)。
