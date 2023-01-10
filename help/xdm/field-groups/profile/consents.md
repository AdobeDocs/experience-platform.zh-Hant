---
solution: Experience Platform
title: 同意和首選項架構欄位組
description: 本文檔概述了「同意」和「首選項」架構欄位組。
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# [!UICONTROL 同意和偏好設定] 欄位群組

[!UICONTROL 同意和偏好設定] 是 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md) 擷取個別客戶的同意和偏好設定資訊。

>[!NOTE]
>
>由於此欄位組僅與相容 [!DNL XDM Individual Profile]，則無法用於 [!DNL XDM ExperienceEvent] 結構。 如果您想在「體驗事件」結構中加入同意和偏好設定資料，請新增 [[!UICONTROL 隱私權、個人化和行銷偏好設定的同意] 資料類型](../../data-types/consents.md) 透過使用 [自訂欄位群組](../../ui/resources/field-groups.md#create) 。

## 欄位群組結構 {#structure}

此 [!UICONTROL 同意和偏好設定] 欄位組提供單個對象類型欄位， `consents`，擷取同意和偏好設定資訊。 此欄位將 [[!UICONTROL 隱私權、個人化和行銷偏好設定的同意] 資料類型](../../data-types/consents.md)，移除 `adID` 欄位和新增 `idSpecific` 映射欄位。

![](../../images/field-groups/consent.png)

>[!TIP]
>
>請參閱 [探索XDM資源](../../ui/explore.md) 如需如何在Platform UI中尋找任何XDM資源並檢查其結構的步驟，請參閱。

下列JSON顯示資料類型的範例，其中 [!UICONTROL 同意和偏好設定] 欄位群組可以處理。 有關如何使用欄位組提供的大多數欄位的資訊，請參閱 [同意和首選項資料類型](../../data-types/consents.md). 以下子區段著重於欄位群組新增至資料類型的唯一屬性。

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
>* [在API中產生範例資料](../../api/sample-data.md)


### `idSpecific`

`idSpecific` 特定同意或偏好設定並非普遍適用於客戶，但僅限於單一裝置或ID時，才可使用。 例如，客戶可以選擇不接收某個地址的電子郵件，同時允許另一個地址的電子郵件。

>[!IMPORTANT]
>
>管道層級同意和偏好(即 `consents` 外部 `idSpecific`)會套用至該管道中的所有ID。 因此，無論是採用等同的ID或裝置專屬設定，所有通道層級的同意和偏好設定都會直接生效：
>
>* 如果客戶已在管道層級選擇退出，則 `idSpecific` 會被忽略。
>* 如果未設定管道層級同意或偏好設定，或客戶已選擇加入，則中的相等同意或偏好設定 `idSpecific` 都很榮幸。


中的每個鍵 `idSpecific` 物件代表Adobe Experience Platform Identity Service所識別的特定身分命名空間。 雖然您可以定義自己的自訂命名空間，將不同的識別碼分類，但建議您使用Identity Service提供的其中一個標準命名空間，以減少「即時客戶設定檔」的儲存大小。 如需身分識別命名空間的詳細資訊，請參閱 [身分命名空間概述](../../../identity-service/namespaces.md) （在Identity Service檔案中）。

每個命名空間對象的鍵都表示客戶為其設定首選項的唯一標識值。 每個標識值都可以包含一組完整的同意和首選項，格式與 `consents`.

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
  "ECID": {
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

內 `marketing` 提供於 `idSpecific` 區段 `any` 和 `preferred` 不支援欄位。 這些欄位只能在使用者層級設定。 此外， `idSpecific` 行銷偏好設定 `email`, `sms`，和 `push` 不支援 `subscriptions` 欄位。

也有只能在 `idSpecific` 小節： `adID`. 以下小節將介紹此欄位。

#### `adID`

此 `adID` 同意代表客戶同意是否可使用廣告商ID（IDFA或GAID）來連結此裝置上各應用程式的客戶。 此值只能設定在 `ECID` 身分命名空間 `idSpecific` ，則無法為其他命名空間或此欄位群組的使用者層級設定和。

```json
"idSpecific": {
  "ECID": {
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
>
>您不需要直接設定此值，因為Adobe Experience Platform Mobile SDK會在適當時自動設定。

## 使用欄位群組擷取資料 {#ingest}

若要使用 [!UICONTROL 同意和偏好設定] 欄位群組，您必鬚根據包含該欄位群組的結構，建立資料集。

請參閱 [在UI中建立結構](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) 以取得如何指派欄位群組至欄位的步驟。 建立包含欄位的架構後，請使用 [!UICONTROL 同意和偏好設定] 欄位群組，請參閱 [建立資料集](../../../catalog/datasets/user-guide.md#create) 在「資料集使用指南」中，依照步驟使用現有結構建立資料集。

>[!IMPORTANT]
>
>如果您想要將同意資料傳送至 [!DNL Real-Time Customer Profile]，您必須建立 [!DNL Profile] — 啟用的架構，基於 [!DNL XDM Individual Profile] 包含 [!UICONTROL 同意和偏好設定] 欄位群組。 您根據該結構建立的資料集也必須啟用 [!DNL Profile]. 如需相關的特定步驟，請參閱上述連結的教學課程 [!DNL Real-Time Customer Profile] 結構和資料集的需求。
>
>此外，您也必須確定合併原則的設定順序為包含最新同意和偏好設定資料的資料集優先順序，以便正確更新客戶設定檔。 請參閱 [合併策略](../../../rtcdp/profile/merge-policies.md) 以取得更多資訊。

## 處理同意和偏好設定變更

當客戶在您的網站上變更其同意或偏好設定時，應收集這些變更，並立即使用 [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). 如果客戶選擇退出資料收集，則所有資料收集必須立即停止。 如果客戶選擇退出個人化，則其造訪的下一頁不應出現個人化。

## 後續步驟

本檔案說明 [!UICONTROL 同意和偏好設定] 欄位群組。 有關欄位組提供的其他欄位的詳細資訊，請參閱 [[!UICONTROL 隱私權、個人化和行銷偏好設定的同意] 資料類型](../../data-types/consents.md).
