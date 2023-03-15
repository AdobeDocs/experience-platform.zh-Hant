---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個別設定檔；欄位；結構；結構；區段；segmentMembership；區段成員資格；結構設計；對應；對應；
solution: Experience Platform
title: 區段成員資格詳細資訊結構欄位群組
description: 本檔案概述「區段成員資訊詳細資料」結構欄位群組。
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: fda47171cde3f58f48ee721357923017918a7d4e
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---


# [!UICONTROL 區段成員資格詳細資料] 方案欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 請參閱 [欄位群組名稱更新](../name-updates.md) 以取得更多資訊。

[!UICONTROL 區段成員資格詳細資料] 是的標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md). 欄位群組提供單一對應欄位，可擷取關於區段成員資格的資訊，包括個人所屬的區段、上次資格時間，以及成員資格有效到期的時間。

>[!WARNING]
>
>若 `segmentMembership` 欄位必須使用此欄位群組手動新增至您的設定檔架構，您不應嘗試手動填入或更新此欄位。 系統會自動更新 `segmentMembership` 會執行分段作業時對應每個設定檔。

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `segmentMembership` | 地圖 | 描述個人區段成員資格的映射物件。 此物件的結構將於下文詳細說明。 |

{style="table-layout:auto"}

以下是範例 `segmentMembership` 映射系統已為特定配置檔案填入的。 區段成員資格會依命名空間排序，如物件的根層級索引鍵所示。 而每個命名空間下的個別索引鍵則代表設定檔所屬區段的ID。 每個區段物件包含數個子欄位，可提供成員資格的進一步詳細資料：

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "existing",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `xdm:version` | 此設定檔符合資格的區段版本。 |
| `xdm:lastQualificationTime` | 此設定檔符合區段資格的上次時間時間戳記。 |
| `xdm:validUntil` | 不應再假設區段成員資格有效的時間戳記。 若為外部對象，若未設定此欄位，則只會從 `lastQualificationTime`. |
| `xdm:status` | 字串欄位，指出區段成員資格是否已在目前請求中實現。 接受下列值： <ul><li>`existing`:在請求前，設定檔已是區段的一部分，並會繼續保留其成員資格。</li><li>`realized`:設定檔會在目前請求中輸入區段。</li><li>`exited`:設定檔會隨著目前請求退出區段。</li></ul> |
| `xdm:payload` | 某些區段成員資格包含描述與成員資格直接相關的其他值的裝載。 每個成員只能提供指定類型的一個有效負載。 `xdm:payloadType` 指出裝載的類型(`boolean`, `number`, `propensity`，或 `string`)，而其同層級屬性則提供裝載類型的值。 |

{style="table-layout:auto"}

>[!NOTE]
>
>任何位於 `exited` 狀態超過30天，根據 `lastQualificationTime`，將會遭刪除。

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
