---
solution: Experience Platform
title: 同意和首選項架構欄位組
description: 此文檔概述了「同意」和「首選項」架構欄位組。
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# [!UICONTROL 同意和首選項] 欄位組

[!UICONTROL 同意和首選項] 是標準欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md) 獲取單個客戶的同意和偏好資訊。

>[!NOTE]
>
>因為此欄位組僅與 [!DNL XDM Individual Profile]，不能用於 [!DNL XDM ExperienceEvent] 架構。 如果要在「體驗事件」架構中包括同意和首選項資料，請添加 [[!UICONTROL 隱私、個性化和市場營銷首選項的同意] 資料類型](../../data-types/consents.md) 通過使用 [自定義域組](../../ui/resources/field-groups.md#create) 的雙曲餘切值。

## 欄位組結構 {#structure}

的 [!UICONTROL 同意和首選項] 欄位組提供單個對象類型欄位， `consents`，以獲取同意和偏好資訊。 此欄位擴展 [[!UICONTROL 隱私、個性化和市場營銷首選項的同意] 資料類型](../../data-types/consents.md)，刪除 `adID` 欄位並添加 `idSpecific` 映射欄位。

![](../../images/field-groups/consent.png)

>[!TIP]
>
>請參閱上的指南 [探索XDM資源](../../ui/explore.md) 有關如何查找任何XDM資源並檢查其在平台UI中的結構的步驟。

以下JSON顯示以下資料類型的示例： [!UICONTROL 同意和首選項] 欄位組可以處理。 有關如何使用欄位組提供的大多數欄位的資訊，請參閱上 [同意和首選項資料類型](../../data-types/consents.md)。 下面的子部分重點介紹欄位組添加到資料類型的唯一屬性。

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
>您可以為在Experience Platform中定義的任何XDM架構生成示例JSON資料，以幫助直觀地顯示客戶同意和首選項資料的映射方式。 有關詳細資訊，請參閱以下文檔：
>
>* [在UI中生成示例資料](../../ui/sample.md)
>* [在API中生成示例資料](../../api/sample-data.md)


### `idSpecific`

`idSpecific` 當特定的同意或偏好並非普遍適用於客戶，而僅限於單個設備或ID時，可以使用。 例如，客戶可以選擇不接收到一個地址的電子郵件，同時可能允許在另一個地址上發送電子郵件。

>[!IMPORTANT]
>
>渠道級別的同意和偏好(即 `consents` 外 `idSpecific`)應用於該通道內的所有ID。 因此，所有通道級別的同意和首選項都直接影響是否滿足等同的ID或設備特定設定：
>
>* 如果客戶在渠道級別選擇退出，則在 `idSpecific` 忽略。
>* 如果未設定渠道級別的同意或首選項，或客戶已選擇加入，則 `idSpecific` 是榮譽。


中的每個鍵 `idSpecific` 對象表示由Adobe Experience Platform身份服務識別的特定身份命名空間。 雖然您可以定義自己的自定義命名空間以對不同的標識符進行分類，但建議您使用Identity Service提供的標準命名空間之一來減少即時客戶配置檔案的儲存大小。 有關標識命名空間的詳細資訊，請參見 [標識命名空間概述](../../../identity-service/namespaces.md) 中。

每個命名空間對象的鍵表示客戶為其設定首選項的唯一標識值。 每個標識值可以包含一組完整的同意和首選項，格式與 `consents`。

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

在 `marketing` 提供的對象 `idSpecific` 的子菜單。 `any` 和 `preferred` 不支援欄位。 這些欄位只能在用戶級別上配置。 另外， `idSpecific` 市場營銷首選項 `email`。 `sms`, `push` 不支援 `subscriptions` 的子菜單。

還有一個只能在 `idSpecific` 部分： `adID`。 此欄位在下文小節中介紹。

#### `adID`

的 `adID` 同意表示客戶同意是否可以使用廣告商ID（IDFA或GAID）將客戶連結到此設備上的多個應用。 此值只能在 `ECID` 標識命名空間 `idSpecific` ，不能為其他命名空間或此欄位組的用戶級別設定。

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
>您不應直接設定此值，因為Adobe Experience Platform移動SDK會在適當時自動設定該值。

## 使用欄位組接收資料 {#ingest}

為了使用 [!UICONTROL 同意和首選項] 欄位組以從客戶處接收同意資料，必須基於包含該欄位組的架構建立資料集。

請參閱上的教程 [在UI中建立架構](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) 有關如何將欄位組分配給欄位的步驟。 建立包含域的架構後 [!UICONTROL 同意和首選項] 欄位組，請參閱 [建立資料集](../../../catalog/datasets/user-guide.md#create) 在dataset使用手冊中，按照使用現有模式建立資料集的步驟進行操作。

>[!IMPORTANT]
>
>如果要將同意資料發送到 [!DNL Real-Time Customer Profile]，需要建立 [!DNL Profile]-enabled方案，基於 [!DNL XDM Individual Profile] 包含 [!UICONTROL 同意和首選項] 欄位組。 您基於該架構建立的資料集也必須為 [!DNL Profile]。 請參閱上面連結的教程，瞭解與 [!DNL Real-Time Customer Profile] 模式和資料集的要求。
>
>此外，您還必須確保將合併策略配置為將包含最新同意和首選項資料的資料集優先化，以便正確更新客戶配置檔案。 請參閱 [合併策略](../../../rtcdp/profile/merge-policies.md) 的子菜單。

## 處理同意和首選項更改

當客戶在您的網站上更改其同意或首選項時，應收集這些更改並立即使用 [Adobe Experience PlatformWeb SDK](../../../edge/consent/supporting-consent.md)。 如果客戶從資料收集中退出，則必須立即停止所有資料收集。 如果客戶選擇取消個性化，則他們訪問的下一頁上不應顯示個性化。

## 後續步驟

本文檔介紹了 [!UICONTROL 同意和首選項] 欄位組。 有關欄位組提供的其他欄位的詳細資訊，請參閱 [[!UICONTROL 隱私、個性化和市場營銷首選項的同意] 資料類型](../../data-types/consents.md)。
