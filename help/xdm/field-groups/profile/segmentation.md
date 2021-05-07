---
keywords: Experience Platform;home；熱門主題；架構；架構；XDM；個人配置檔案；欄位；架構；架構；segment;segmentMembership;segment成員資格；架構設計；map；映射；
solution: Experience Platform
title: 區段成員資格詳細資料結構欄位群組
topic-legacy: overview
description: 本檔案提供「區段成員資格詳細資訊結構」欄位群組的概述。
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 1%

---


# [!UICONTROL Segment Membership Details] 方案欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 如需詳細資訊，請參閱[欄位群組名稱updates](../name-updates.md)上的檔案。

[!UICONTROL Segment Membership Details] 是類的標準方案欄位 [[!DNL XDM Individual Profile] 組](../../classes/individual-profile.md)。欄位群組提供單一對應欄位，可擷取區段成員資格的相關資訊，包括個人所屬的區段、最後的資格時間，以及會籍的有效期到。

>[!WARNING]
>
>雖然`segmentMembership`欄位必須使用此欄位群組手動新增至您的描述檔架構，但您不應嘗試手動填入或更新此欄位。 當執行分段作業時，系統會自動更新每個描述檔的`segmentMembership`對應。

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `segmentMembership` | 地圖 | 描述個人區段成員資格的映射對象。 此對象的結構將在下面詳細說明。 |

以下是系統已為特定配置檔案填入的`segmentMembership`映射示例。 區段成員資格會依命名空間排序，如物件的根層級索引鍵所示。 反過來，每個名稱空間下的個別索引鍵代表描述檔所屬區段的ID。 每個區段物件包含數個子欄位，可提供成員資格的進一步詳細資訊：

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
| `xdm:payload` | 部分區段成員資格包含描述與會籍直接相關之其他值的裝載。 每個會籍只能提供一個指定類型的裝載。 `xdm:payloadType` 指出裝載的類型(`boolean`、 `number`、 `propensity` `string`或)，而其sibling屬性則提供裝載類型的值。 |

有關欄位組的詳細資訊，請參閱公用XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
