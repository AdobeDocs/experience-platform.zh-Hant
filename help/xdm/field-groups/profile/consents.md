---
solution: Experience Platform
title: 同意與偏好設定架構欄位群組
description: 了解「同意與偏好設定綱要」字段群組。
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: be35c5398cd96cdfe424c5088db288ba4061ac4a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# [!UICONTROL 同意與偏好設定] 欄位群組

[!UICONTROL 同意和偏好設定]是用于捕獲單個客戶的同意和偏好信息的類](../../classes/individual-profile.md)的標準[[!DNL XDM Individual Profile] 字段群組。

>[!NOTE]
>
>由於此欄位群組僅與 相容 [!DNL XDM Individual Profile]，因此無法用於 [!DNL XDM ExperienceEvent] 架構。 如果您想在體驗事件綱要中包含同意和偏好數據，請改為使用[自定義欄位群組](../../ui/resources/field-groups.md#create)將隱私[[!UICONTROL 、個人化和行銷偏好設定]](../../data-types/consents.md)同意數據類型添加到綱要。

## 欄位群組結構 {#structure}

“ [!UICONTROL 同意和偏好設定] ”字段群組提供單個物件類型字段 ， `consents`以捕獲同意和首選項信息。 此欄位擴展 [[!UICONTROL 了隱私、個人化和行銷同意偏好設定] 數據類型](../../data-types/consents.md)，刪除該 `adID` 欄位並添加 `idSpecific` 映射欄位。

![](../../images/field-groups/consent.png)

>[!TIP]
>
>請參閱有關流覽XDM資源](../../ui/explore.md)指南[，瞭解如何在Platform UI中查找任何XDM資源並檢查其結構的步驟。

下列JSON顯示[!UICONTROL 同意和偏好設定]欄位群組可以處理的資料型別範例。 如需有關如何使用欄位群組所提供之大部分欄位的資訊，請參閱[同意和偏好設定資料型別](../../data-types/consents.md)的指南。 以下子區段著重於欄位群組新增至資料型別的獨特屬性。

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
>您可以為您在Experience Platform中定義的任何XDM結構描述產生範例JSON資料，以視覺化方式對應您的客戶同意和偏好設定資料。 如需詳細資訊，請參閱下列檔案：
>
>* [在UI中產生範例資料](../../ui/sample.md)
>* [Generate sample data in the API](../../api/sample-data.md)

### `idSpecific`

當特定同意或偏好設定不普遍適用於客戶，但僅限於單一裝置或ID時，可以使用`idSpecific`。 例如，客戶可以選擇退出接收到一個地址的电子郵件，同時可能允許另一個地址上的电子郵件。

>[!IMPORTANT]
>
>管道層級的同意和偏好設定（亦即`idSpecific`以外的`consents`底下提供的同意和偏好設定）套用至該管道內的所有ID。 因此，無論遵循對等的ID或裝置特定設定，所有管道層級同意和偏好設定都會直接生效：
>
>* 如果客戶已在頻道層級選擇退出，則會忽略`idSpecific`中的任何對等同意或偏好設定。
>* 如果未設定管道層級的同意或偏好設定，或客戶已選擇加入，則會接受`idSpecific`中相等的同意或偏好設定。

`idSpecific`物件中的每個索引鍵代表Adobe Experience Platform Identity服務可辨識的特定身分名稱空間。 雖然您可以定義自己的自定義命名空間來對不同的標識符進行分類，但建議您使用Identity Service 提供的標準命名空間之一來減少即時客戶配置檔的儲存大小。 有關身份命名空間的更多資訊，請參閱 [身份服務文檔中的身份命名空間概述](../../../identity-service/features/namespaces.md) 。

每個命名空間對象的鍵表示客戶為其設置首選項的唯一標識值。 每個身分值都可以包含一組完整的同意和偏好設定，其格式與 相同 `consents`。

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

在本節提供`idSpecific`的物件中`marketing`，`any`不支援and `preferred` 欄位。這些欄位只能在用戶層級設定。 此外， `idSpecific` 行銷偏好 `email`設定、 `sms`和 `push` 不支援 `subscriptions` 字段。

還有一個只能在以下 `idSpecific` 部分中 `adID`提供的同意：。 以下小節將介紹此欄位。

#### `adID`

同意表示 `adID` 客戶同意是否可以使用廣告商 ID（IDFA 或 GAID）在此裝置的应用之間連結客戶。 此值只能在部分中的`idSpecific`標識命名空間下`ECID`配置，不能為其他命名空間設置，也不能在此欄位群組的用戶級別設置。

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
>您不必直接設定此值，因為 Adobe Experience Platform Mobile SDK 會在適當的時候自動設定此值。

## 使用欄位群組引入數據 {#ingest}

為了使用“同意和偏好設定]”字段群組從[!UICONTROL 客戶引入同意數據，必須基於包含該欄位群組的綱要創建資料集。

如需如何將欄位群組指派給欄位的步驟，請參閱有關[在UI](https://www.adobe.com/go/xdm-schema-editor-tutorial-en)中建立結構描述的教學課程。 建立包含具有[!UICONTROL 同意和偏好設定]欄位群組的欄位的結構描述後，請參閱資料集使用指南中有關[建立資料集](../../../catalog/datasets/user-guide.md#create)的章節，然後依照步驟使用現有結構描述建立資料集。

>[!IMPORTANT]
>
>若要將同意資料傳送至[!DNL Real-Time Customer Profile]，您必須根據包含[!UICONTROL 同意和偏好設定]欄位群組的[!DNL XDM Individual Profile]類別，建立啟用[!DNL Profile]的結構描述。 您根據該結構描述建立的資料集也必須為[!DNL Profile]啟用。 請參閱上述連結的教學課程，以瞭解結構描述和資料集[!DNL Real-Time Customer Profile]需求的相關特定步驟。
>
>此外，您也必須確保合併原則已設定為優先處理包含最新同意和偏好設定資料的資料集，以便客戶設定檔能夠正確更新。 如需詳細資訊，請參閱[合併原則](../../../rtcdp/profile/merge-policies.md)的概觀。

## 處理同意和偏好設定變更

當客戶在您的網站上變更其同意或偏好設定時，應使用[Adobe Experience Platform Web SDK](../../../web-sdk/commands/setconsent.md)收集並立即強制執行這些變更。 如果客戶選擇退出資料收集，所有資料收集必須立即停止。 如果客戶選擇退出個人化，則他們載入的下一個頁面上應該不會出現個人化。

## 後續步驟

此檔案涵蓋[!UICONTROL 同意和偏好設定]欄位群組的結構和使用。 如需欄位群組所提供其他欄位的詳細資訊，請參閱[[!UICONTROL 隱私權同意、Personalization和行銷偏好設定]資料型別](../../data-types/consents.md)的檔案。
