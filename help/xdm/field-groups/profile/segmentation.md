---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;segment;segmentMembership;segment membership;Schema design;map;Map;
solution: Experience Platform
title: Segment Membership Details Schema Field Group
topic-legacy: overview
description: This document provides an overview of the Segment Membership Details schema field group.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 2%

---


# [!UICONTROL 區段成員資格] 詳細資訊結構欄位群組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 有關詳細資訊，請參閱[欄位組名稱更新](../name-updates.md)上的文檔。

[!UICONTROL Segment Membership Details] is a standard schema field group for the [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). 欄位群組提供單一對應欄位，可擷取關於區段成員資格的資訊，包括個人所屬的區段、上次資格時間，以及成員資格有效到期的時間。

>[!WARNING]
>
>雖然必須使用此欄位組手動將`segmentMembership`欄位添加到您的配置檔案架構，但您不應嘗試手動填入或更新此欄位。 當執行分段作業時，系統會自動更新每個設定檔的`segmentMembership`對應。

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `segmentMembership` | 地圖 | 描述個人區段成員資格的映射物件。 The structure of this object is described in detail below. |

{style=&quot;table-layout:auto&quot;}

以下是系統已針對特定設定檔填入的範例`segmentMembership`對應。 Segment memberships are sorted by namespace, as indicated by the root-level keys of the object. 而每個命名空間下的個別索引鍵則代表設定檔所屬區段的ID。 每個區段物件包含數個子欄位，可提供成員資格的進一步詳細資料：

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
| `xdm:version` | The version of the segment that this profile qualified for. |
| `xdm:lastQualificationTime` | 此設定檔符合區段資格的上次時間時間戳記。 |
| `xdm:validUntil` | 不應再假設區段成員資格有效的時間戳記。 |
| `xdm:status` | 指出區段成員資格是否已在目前請求中實現。 接受下列值： <ul><li>`existing`:在請求前，設定檔已是區段的一部分，並會繼續保留其成員資格。</li><li>`realized`:設定檔會在目前請求中輸入區段。</li><li>`exited`: The profile is exiting the segment as part of the current request.</li></ul> |
| `xdm:payload` | 某些區段成員資格包含描述與成員資格直接相關的其他值的裝載。 Only one payload of a given type can be provided for each membership. `xdm:payloadType` indicates the type of payload (`boolean`, `number`, `propensity`, or `string`), while its sibling property provides the value for the payload type. |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
