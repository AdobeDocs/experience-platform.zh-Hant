---
solution: Experience Platform
title: 同意和偏好設定結構描述欄位群組
description: 瞭解同意和偏好設定結構描述欄位群組。
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# [!UICONTROL 同意和偏好設定] 欄位群組

[!UICONTROL 同意和偏好設定] 是的標準欄位群組 [[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md) 擷取個別客戶的同意和偏好設定資訊。

>[!NOTE]
>
>由於此欄位群組僅與 [!DNL XDM Individual Profile]，無法用於 [!DNL XDM ExperienceEvent] 結構描述。 如果您想要在體驗事件結構描述中包含同意和偏好設定資料，請新增 [[!UICONTROL 隱私、個人化和行銷偏好設定的同意] 資料型別](../../data-types/consents.md) 透過使用至結構描述 [自訂欄位分組](../../ui/resources/field-groups.md#create) 而非。

## 欄位群組結構 {#structure}

此 [!UICONTROL 同意和偏好設定] 欄位群組提供單一物件型別欄位， `consents`，以擷取同意和偏好設定資訊。 此欄位會擴充 [[!UICONTROL 隱私、個人化和行銷偏好設定的同意] 資料型別](../../data-types/consents.md)，移除 `adID` 欄位並新增 `idSpecific` 對應欄位。

![](../../images/field-groups/consent.png)

>[!TIP]
>
>請參閱以下指南： [探索XDM資源](../../ui/explore.md) ，以瞭解如何在Platform UI中查詢任何XDM資源及檢查其結構的步驟。

以下JSON範例說明 [!UICONTROL 同意和偏好設定] 欄位群組可以處理。 有關如何使用欄位群組提供的大多數欄位的資訊，請參閱 [同意和偏好設定資料型別](../../data-types/consents.md). 以下子區段著重於欄位群組新增至資料型別的獨特屬性。

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
>您可以為您在Experience Platform中定義的任何XDM結構描述產生範例JSON資料，以協助視覺化客戶同意和偏好設定資料應如何對應。 如需詳細資訊，請參閱下列檔案：
>
>* [在UI中產生範例資料](../../ui/sample.md)
>* [在API中產生範例資料](../../api/sample-data.md)

### `idSpecific`

`idSpecific` 當特定同意或偏好設定不普遍適用於客戶，但限於單一裝置或ID時可使用。 例如，客戶可以選擇不接收某個地址的電子郵件，而可能允許另一個地址的電子郵件。

>[!IMPORTANT]
>
>管道層級的同意和偏好設定（即下方提供的同意和偏好設定） `consents` 外部 `idSpecific`)適用於該管道中的所有ID。 因此，無論遵循對等的ID或裝置特定設定，所有管道層級同意和偏好設定都會直接生效：
>
>* 如果客戶在管道層級選擇退出，則任何對等的同意或偏好設定在 `idSpecific` 都會被忽略。
>* 如果未設定管道層級的同意或偏好設定，或客戶已選擇加入，則中的對等同意或偏好設定會生效。 `idSpecific` 榮譽。

中的每一個索引鍵 `idSpecific` 物件代表Adobe Experience Platform Identity服務可辨識的特定身分名稱空間。 雖然您可以定義自己的自訂名稱空間來分類不同的識別碼，但建議您使用Identity Service提供的標準名稱空間之一，來減少即時客戶個人檔案的儲存大小。 如需身分識別名稱空間的詳細資訊，請參閱 [身分名稱空間總覽](../../../identity-service/features/namespaces.md) Identity Service檔案中。

每個名稱空間物件的索引鍵代表客戶已設定偏好設定的唯一身分值。 每個身分值都可以包含一組完整的同意和偏好設定，格式與相同 `consents`.

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

範圍 `marketing` 中提供的物件 `idSpecific` 區段， `any` 和 `preferred` 欄位不受支援。 這些欄位只能在使用者層級設定。 此外， `idSpecific` 的行銷偏好設定 `email`， `sms`、和 `push` 不支援 `subscriptions` 欄位。

此外，也只有在下列情況下才能提供同意： `idSpecific` 區段： `adID`. 以下小節將介紹此欄位。

#### `adID`

此 `adID` 同意代表客戶同意，廣告商ID （IDFA或GAID）是否可用來在此裝置上跨應用程式連結客戶。 此值只能在 `ECID` 中的身分名稱空間 `idSpecific` 區段，且無法針對其他名稱空間或此欄位群組的使用者層級設定。

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
>您不應直接設定此值，因為Adobe Experience Platform Mobile SDK會在適當時自動進行設定。

## 使用欄位群組擷取資料 {#ingest}

為了使用 [!UICONTROL 同意和偏好設定] 欄位群組若要從客戶擷取同意資料，您必須根據包含該欄位群組的結構描述建立資料集。

請參閱上的教學課程 [在UI中建立結構描述](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) 有關如何將欄位群組指派給欄位的步驟。 建立包含欄位的結構描述後，使用 [!UICONTROL 同意和偏好設定] 欄位群組，請參閱以下區段： [建立資料集](../../../catalog/datasets/user-guide.md#create) 請依照步驟，在資料集使用手冊中，使用現有結構描述建立資料集。

>[!IMPORTANT]
>
>如果您想要將同意資料傳送至 [!DNL Real-Time Customer Profile]，您必須建立 [!DNL Profile] — 啟用的結構描述，根據 [!DNL XDM Individual Profile] 包含 [!UICONTROL 同意和偏好設定] 欄位群組。 您根據該結構描述建立的資料集也必須啟用 [!DNL Profile]. 如需瞭解相關的具體步驟，請參閱上述教學課程 [!DNL Real-Time Customer Profile] 結構描述和資料集的需求。
>
>此外，您也必須確保合併原則已設定為優先處理包含最新同意和偏好設定資料的資料集，以便客戶設定檔能夠正確更新。 請參閱以下主題的概觀： [合併原則](../../../rtcdp/profile/merge-policies.md) 以取得詳細資訊。

## 處理同意和偏好設定變更

當客戶在您的網站上變更其同意或偏好設定時，應使用收集這些變更並立即執行 [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). 如果客戶選擇退出資料收集，所有資料收集必須立即停止。 如果客戶選擇退出個人化，則他們造訪的下一個頁面上應該不會出現個人化。

## 後續步驟

本檔案說明 [!UICONTROL 同意和偏好設定] 欄位群組。 如需欄位群組所提供其他欄位的詳細資訊，請參閱 [[!UICONTROL 隱私、個人化和行銷偏好設定的同意] 資料型別](../../data-types/consents.md).
