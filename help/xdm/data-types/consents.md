---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；同意；同意；偏好設定；偏好設定；privacyOptOuts；marketingPreferences；optOutType；basisOfProcessing；同意
title: 同意和偏好設定資料型別
description: 「隱私權同意」、「Personalization」和「行銷偏好設定」資料型別旨在支援收集由「同意管理平台」(CMP)和其他資料來源從您的資料作業產生的客戶許可權和偏好設定。
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 0%

---

# [!UICONTROL 同意和偏好設定]資料型別

[!UICONTROL 隱私權、Personalization和行銷偏好設定的同意]資料型別（以下稱為「[!UICONTROL 同意和偏好設定]」資料型別）是[!DNL Experience Data Model] (XDM)資料型別，其目的在於支援收集由同意管理平台(CMP)和其他來源從您的資料作業產生的客戶許可權和偏好設定。

本檔案說明[!UICONTROL 同意和偏好設定]資料型別所提供的欄位結構和預期用途。

## 先決條件 {#prerequisites}

此檔案需要實際瞭解XDM以及在[!DNL Experience Platform]中使用結構描述。 請先檢閱下列檔案再繼續：

* [XDM系統總覽](https://www.adobe.com/go/xdm-home-en)
* 結構描述組合的[基本概念](https://www.adobe.com/go/xdm-schema-best-practices-en)

## 資料型別結構 {#structure}

>[!IMPORTANT]
>
>[!UICONTROL 同意和偏好設定]資料型別的設計涵蓋一系列同意和偏好設定管理使用案例。 因此，本檔案以一般術語說明資料型別欄位的使用，並僅提供您應如何解譯這些欄位使用的建議。 請洽詢您的隱私權法律團隊，使資料型別的結構符合您的組織如何解讀並向您的客戶展示這些同意和偏好設定選擇。

[!UICONTROL 同意和偏好設定]資料型別提供數個欄位，用於擷取&#x200B;**同意**&#x200B;和&#x200B;**偏好設定**&#x200B;資訊。

同意是一個選項，可讓客戶指定如何使用其資料。 大部分的同意都有法律層面，因為有些司法管轄區在資料以特定方式使用前必須先取得許可，或若不需要肯定同意，則要求客戶可以選擇停止該使用（選擇退出）。

偏好設定是一個選項，可讓客戶指定應如何處理其品牌體驗的不同方面。 這些屬於兩個類別：

* **Personalization偏好設定**：關於品牌應如何個人化體驗提供給客戶的偏好設定。
* **行銷偏好設定**：關於是否允許品牌透過各種管道聯絡客戶的偏好設定。

下列熒幕擷圖顯示資料型別的結構在Experience Platform UI中的呈現方式：

![](../images/data-types/consents.png)

>[!TIP]
>
>如需如何在Experience Platform UI中查詢任何XDM資源及檢查其結構的步驟，請參閱[探索XDM資源](../ui/explore.md)的指南。

下列JSON顯示[!UICONTROL 同意和偏好設定]資料型別可以處理的資料型別範例。 以下各節將提供有關這些欄位各自特定用途的資訊。

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
>您可以為您在Experience Platform中定義的任何XDM結構描述產生範例JSON資料，以視覺化方式對應您的客戶同意和偏好設定資料。 如需詳細資訊，請參閱下列檔案：
>
>* [在UI中產生範例資料](../ui/sample.md)
>* [在API中產生範例資料](../api/sample-data.md)

## `consents` {#choices}

`consents`包含數個描述客戶同意和偏好設定的欄位。 以下各小節會詳細說明這些欄位。

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

`collect`代表客戶同意收集其資料。

```json
"collect": {
  "val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `val` | 客戶針對此使用案例提供的同意選擇。 如需接受的值和定義，請參閱[附錄](#choice-values)。 |

{style="table-layout:auto"}

### `adID`

`adID`代表客戶同意是否可以使用廣告商ID在此裝置上跨應用程式連結客戶。

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `idType` | 廣告ID型別，可能是Apple廣告商ID的`IDFA`或Google廣告商ID的`GAID`，也稱為Android廣告商ID (AAID)。 |
| `val` | 客戶針對此使用案例提供的同意選擇。 如需接受的值和定義，請參閱[附錄](#choice-values)。 |

{style="table-layout:auto"}

### `share`

`share`代表客戶同意其資料可以與第二方或第三方共用（或賣給）。

```json
"share": {
  "val": "y"
}
```

| 屬性 | 說明 |
| --- | --- |
| `val` | 客戶針對此使用案例提供的同意選擇。 如需接受的值和定義，請參閱[附錄](#choice-values)。 |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize`擷取客戶對其資料用於個人化的偏好設定。 客戶可以選擇退出特定的個人化使用案例，或完全選擇退出個人化。

>[!IMPORTANT]
>
>`personalize`未涵蓋行銷使用案例。 例如，如果客戶選擇退出所有管道的個人化，他們不應停止透過這些管道接收通訊。 相反地，他們收到的訊息應該是通用的，而不是根據其設定檔。
>
>根據相同範例，如果客戶選擇退出所有頻道的直銷（透過`marketing`，在[下一節](#marketing)中說明），則即使允許個人化，該客戶也不應接收任何訊息。

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `content` | 代表客戶對您網站或應用程式上的個人化內容的偏好設定。 |
| `val` | 客戶針對指定使用案例提供的個人化偏好設定。 如果不需要提示客戶提供同意，此欄位的值應該指出進行個人化的基礎。 如需接受的值和定義，請參閱[附錄](#choice-values)。 |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing`擷取客戶對其資料可用於哪些行銷用途的偏好設定。 客戶可以選擇退出特定行銷使用案例，或完全選擇退出直銷。

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
| `preferred` | 表示客戶接收通訊的偏好管道。 如需接受的值，請參閱[附錄](#preferred-values)。 |
| `any` | 代表整體直銷的客戶偏好設定。 此欄位中提供的同意偏好設定視為任何行銷管道的「預設」偏好設定，除非被`marketing`下提供的其他子欄位覆寫。 如果您打算使用更精細的同意選項，建議您排除此欄位。<br><br>如果值設定為`n`，則所有更具體的個人化設定都將被忽略。 如果值設定為`y`，則所有較精細的個人化選項也應視為`y`，除非明確設定為`n`。 如果未設定該值，則每個個人化選項的值都應按照指定接受。 |
| `email` | 指出客戶是否同意接收電子郵件訊息。 |
| `push` | 指出客戶是否允許接收推播通知。 |
| `sms` | 指出客戶是否同意接收簡訊。 |
| `val` | 客戶針對指定使用案例提供的偏好設定。 如果不需要提示客戶提供同意，此欄位的值應該指出行銷使用案例應該發生的基礎。 如需接受的值和定義，請參閱[附錄](#choice-values)。 |
| `time` | 行銷偏好設定變更時間的ISO 8601時間戳記（如適用）。 請注意，如果任何個別偏好設定的時間戳記與`metadata`下提供的時間戳記相同，則不會為該偏好設定設定此欄位。 |
| `reason` | 當客戶選擇退出行銷使用案例時，此字串欄位代表客戶選擇退出的原因。 |

{style="table-layout:auto"}

### `metadata`

`metadata`會擷取有關客戶同意和偏好設定的一般中繼資料，而不論何時進行上次更新。

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| 屬性 | 說明 |
| --- | --- |
| `time` | 上次更新任何客戶同意和偏好設定的ISO 8601時間戳記。 此欄位可用於取代將時間戳記套用到個別偏好設定，以減少載入和複雜性。 在個別偏好設定下提供`time`值，會覆寫該特定偏好設定的`metadata`時間戳記。 |

{style="table-layout:auto"}

## 使用資料型別擷取資料 {#ingest}

若要使用[!UICONTROL 同意和偏好設定]資料型別從客戶擷取同意資料，您必須根據包含該資料型別的結構描述建立資料集。

如需如何將資料型別指派給欄位的步驟，請參閱有關[在UI](https://www.adobe.com/go/xdm-schema-editor-tutorial-en)中建立結構描述的教學課程。 建立包含欄位（具有[!UICONTROL 同意和偏好設定]資料型別）的結構描述後，請參閱資料集使用指南中有關[建立資料集](../../catalog/datasets/user-guide.md#create)的章節，並依照步驟使用現有結構描述建立資料集。

>[!IMPORTANT]
>
>若要將同意資料傳送至[!DNL Real-Time Customer Profile]，您必須根據包含[!UICONTROL 同意和偏好設定]資料型別的[!DNL XDM Individual Profile]類別，建立啟用[!DNL Profile]的結構描述。 您根據該結構描述建立的資料集也必須為[!DNL Profile]啟用。 請參閱上述連結的教學課程，以瞭解結構描述和資料集[!DNL Real-Time Customer Profile]需求的相關特定步驟。
>
>此外，您也必須確保合併原則已設定為優先處理包含最新同意和偏好設定資料的資料集，以便客戶設定檔能夠正確更新。 如需詳細資訊，請參閱[合併原則](../../rtcdp/profile/merge-policies.md)的概觀。

## 處理同意和偏好設定變更

當客戶在您的網站上變更其同意或偏好設定時，應使用[Adobe Experience Platform Web SDK](../../web-sdk/commands/setconsent.md)收集並立即強制執行這些變更。 如果客戶選擇退出資料收集，所有資料收集必須立即停止。 如果客戶選擇退出個人化，則他們造訪的下一個頁面上應該不會出現個人化。

## 附錄 {#appendix}

以下各節提供有關[!UICONTROL 同意和偏好設定]資料型別的其他參考資訊。

### `val`的接受值 {#choice-values}

下表概述`val`的接受值：

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是（選擇加入） | 客戶已選擇加入以獲得同意或偏好設定。 換言之，他們&#x200B;**都**&#x200B;同意使用其資料，如相關同意或偏好設定所指示。 |
| `n` | 否（選擇退出） | 客戶已選擇退出同意或偏好設定。 換言之，他們&#x200B;**不**&#x200B;同意使用其資料，如相關同意或偏好設定所指示。 |
| `p` | 待處理的驗證 | 系統尚未收到最終同意或偏好設定值。 這最常用於需要兩步驟驗證的同意作業。 例如，如果客戶選擇接收電子郵件，該同意會設為`p`，直到他們在電子郵件中選取連結，以驗證他們是否已提供正確的電子郵件地址，屆時同意會更新為`y`。<br><br>如果此同意或偏好設定未使用兩集驗證程式，則可能會改用`p`選項來表示客戶尚未回應同意提示。 例如，您可以在客戶回應同意提示前，在網站的第一頁自動將值設為`p`。 在不要求明確同意的管轄區中，您也可以使用它來表示客戶尚未明確選擇退出（換言之，假設您同意）。<br><br>雖然此值可使用其他機制在[!DNL Profile]中擷取（例如串流擷取），但在[!DNL Edge Network]上的資料收集或同意收集中&#x200B;**不支援**。 雖然`p`值無法明確傳送，但[[!DNL Web SDK]](../../landing/governance-privacy-security/consent/sdk.md)仍會處理事件佇列，而且一旦一般使用者的明確同意為`in`，就會將事件分派給[!DNL Edge Network]。 |
| `u` | 未知 | 客戶的同意或偏好設定資訊未知。 |
| `dy` | 預設為「是（選擇加入）」 | 客戶本身並未提供同意值，且預設會被視為選擇加入（「是」）。 換言之，除非客戶另有指示，否則假定您同意。<br><br>請注意，如果法律或您公司隱私權政策的變更導致部分或所有使用者的預設值變更，您必須手動更新包含預設值的所有設定檔。 |
| `dn` | 「否」的預設值（選擇退出） | 客戶本身並未提供同意值，且預設會視為選擇退出（「否」）。 換言之，在客戶指出不同意見之前，他們會被假定為已拒絕同意。<br><br>請注意，如果法律或您公司隱私權政策的變更導致部分或所有使用者的預設值變更，您必須手動更新包含預設值的所有設定檔。 |
| `LI` | 合法利益 | 為了特定目的收集和處理這些資料的合法商業利益，壓倒了它對個人造成的潛在傷害。 |
| `CT` | 合約 | 為特定目的收集資料是履行與個人的合約義務所必需的。 |
| `CP` | 遵守法律義務 | 為了符合企業的法律義務，必須針對特定目的收集資料。 |
| `VI` | 個人的重大利益 | 為了保護個人切身利益，必須針對特定目的收集資料。 |
| `PI` | 公共利益 | 為特定目的收集資料是執行符合公眾利益或行使官方權力的任務所必需的。 |

{style="table-layout:auto"}

### `preferred`的接受值 {#preferred-values}

下表概述`preferred`的接受值。 `preferred`值表示客戶接收通訊的偏好管道，這些通訊會告知他們資料收集、隱私權政策和個人化選項。

| 值 | 說明 |
| --- | --- |
| `email` | 此偏好設定表示客戶同意透過電子郵件接收訊息。 |
| `push` | 此偏好設定表示客戶同意接收推播通知。 這些是直接傳送到其裝置（通常是行動應用程式）的訊息或警示。 |
| `inApp` | 此偏好設定表示客戶同意接收應用程式內訊息。 這些訊息會在行動或網頁應用程式中傳送，並在使用者主動參與應用程式時提供資訊。 |
| `sms` | 此偏好設定表示客戶同意透過SMS （短訊息服務）接收訊息。 這些是傳送至其行動電話的簡訊。 |
| `phone` | 此偏好設定表示客戶同意透過電話互動接收通訊。 |
| `phyMail` | 此偏好設定表示客戶同意透過實體郵件接收資料。 |
| `inVehicle` | 此偏好設定表示客戶同意在他們的車輛中接收通知。 這些訊息可透過車輛資訊娛樂系統或其他車輛內通訊通道傳送。 |
| `inHome` | 此偏好設定表示客戶同意在家中接收訊息。 這些訊息可透過智慧型家用裝置或其他家用通訊通道傳送。 |
| `iot` | 此偏好設定代表客戶同意接收與物聯網(IoT)相關的訊息。 這些訊息可透過其環境中已連線的裝置和系統傳遞。 |
| `social` | 此偏好設定表示客戶同意透過社群媒體平台接收通訊。 |
| `other` | 此偏好設定包含不符合標準類別的管道。 它代表特定企業或產業專用的替代或專門通訊管道。 |
| `none` | 此偏好設定表示客戶沒有偏好的通訊通道。 |
| `unknown` | 此偏好設定表示不清楚或未指定客戶偏好的通訊通道。 如果客戶未提供明確的同意或偏好設定資訊，就可能會發生這種情況。 |

{style="table-layout:auto"}

### 完整[!UICONTROL 同意和偏好設定]結構描述 {#full-schema}

若要檢視[!UICONTROL 同意和偏好設定]資料型別的完整結構描述，請參閱[官方XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json)。
