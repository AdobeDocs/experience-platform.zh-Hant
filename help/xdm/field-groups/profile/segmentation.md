---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；個人配置檔案；欄位；模式；模式；段；段；段成員；段成員；段成員；模式設計；映射；
solution: Experience Platform
title: 段成員身份詳細資訊架構欄位組
description: 本文檔提供「段成員身份詳細資訊」架構欄位組的概述。
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---


# [!UICONTROL 段成員身份詳細資訊] 架構欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 查看上的文檔 [欄位組名稱更新](../name-updates.md) 的子菜單。

[!UICONTROL 段成員身份詳細資訊] 是標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md)。 欄位組提供單個映射欄位，該欄位捕獲有關段成員身份的資訊，包括個人所屬的段、上次資格時間以及成員身份有效到期的時間。

>[!WARNING]
>
>當 `segmentMembership` 必須使用此欄位組將欄位手動添加到配置檔案架構中，您不應嘗試手動填充或更新此欄位。 系統會自動更新 `segmentMembership` 在執行分段作業時為每個配置檔案映射。

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `segmentMembership` | 地圖 | 描述個人段成員身份的映射對象。 此對象的結構在下面詳細描述。 |

{style="table-layout:auto"}

下面是一個示例 `segmentMembership` 映射系統已為特定配置檔案填充的內容。 段成員資格按命名空間排序，如對象的根級鍵所示。 然後，每個命名空間下的各個鍵代表配置檔案所屬的段的ID。 每個段對象都包含幾個子欄位，這些子欄位提供了有關成員身份的詳細資訊：

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "realized",
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
| `xdm:version` | 此配置檔案限定的段的版本。 |
| `xdm:lastQualificationTime` | 此配置檔案上次限定段的時間的時間戳。 |
| `xdm:validUntil` | 不再假定段成員資格有效的時間戳。 對於外部受眾，如果未設定此欄位，則段成員資格將僅保留30天 `lastQualificationTime`。 |
| `xdm:status` | 一個字串欄位，指示是否已將段成員資格作為當前請求的一部分實現。 接受以下值： <ul><li>`realized`:配置檔案符合段的條件。</li><li>`exited`:配置檔案作為當前請求的一部分退出段。</li></ul> |
| `xdm:payload` | 某些段成員身份包括描述與成員身份直接相關的附加值的負載。 每個成員只能提供給定類型的一個負載。 `xdm:payloadType` 指示負載類型(`boolean`。 `number`。 `propensity`或 `string`)，而其sibling屬性為負載類型提供值。 |

{style="table-layout:auto"}

>[!NOTE]
>
>位於 `exited` 超過30天的狀態，根據 `lastQualificationTime`，將被刪除。

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
