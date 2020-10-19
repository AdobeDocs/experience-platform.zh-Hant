---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;segment;segmentMembership;segment membership;Schema design;map;Map;
solution: Experience Platform
title: 描述檔分段混合
topic: overview
description: 本文檔概述了XDM Individual Profile類。
translation-type: tm+mt
source-git-commit: 53575488c08f73a65a7f1cc5f803f9ead707ae48
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---


# [!UICONTROL 描述檔分段] mixin

[!UICONTROL 描述檔分段] 是類別的標準混合 [[!DNL XDM Individual Profile] 檔](../../classes/individual-profile.md)。 混音提供單一地圖欄位，擷取關於區段成員資格的資訊，包括個人所屬的區段、最後的資格時間，以及會籍有效到的時間。

>[!WARNING]
>
>雖然必 `segmentMembership` 須使用此混音手動將欄位新增至您的描述檔結構，但您不應嘗試手動填入或更新此欄位。 當執行分段作業時，系 `segmentMembership` 統會自動更新每個描述檔的地圖。

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `segmentMembership` | 地圖 | 描述個人區段成員資格的映射對象。 此對象的結構將在下面詳細說明。 |

以下是系統已為 `segmentMembership` 特定配置檔案填入的示例映射。 區段成員資格會依命名空間排序，如物件的根層級索引鍵所示。 反過來，每個名稱空間下的個別索引鍵代表描述檔所屬區段的ID。 每個區段物件包含數個子欄位，可提供成員資格的進一步詳細資訊：

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
| `xdm:version` | 此描述檔符合的區段版本。 |
| `xdm:lastQualificationTime` | 此描述檔上次符合區段條件的時間戳記。 |
| `xdm:validUntil` | 區段成員資格不再視為有效的時間戳記。 |
| `xdm:status` | 指出區段成員資格是否已作為目前請求的一部分而實現。 接受下列值： <ul><li>`existing`:描述檔在要求之前已是區段的一部分，並會持續保留其會籍。</li><li>`realized`:描述檔會在目前請求中輸入區段。</li><li>`exited`:描述檔會退出區段作為目前請求的一部分。</li></ul> |
| `xdm:payload` | 部分區段成員資格包含描述與會籍直接相關之其他值的裝載。 每個會籍只能提供一個指定類型的裝載。 `xdm:payloadType` 指出裝載的類型(`boolean`、 `number`、 `propensity``string`或)，而其sibling屬性則提供裝載類型的值。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
