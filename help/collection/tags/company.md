---
title: 公司
description: 取得擁有已實作標籤屬性之IMS組織的相關資訊。
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 3%

---

# `company`

`_satellite.company`物件會顯示擁有標籤屬性之IMS組織的相關資訊。

```ts
readonly _satellite.company: Company
```

## 可用欄位

呼叫此物件時，可使用下列欄位：

```json
{
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "dynamicCdnEnabled": true,
  "cdnAllowList": [
    "assets.adoberesources.cn",
    "assets.adobedtm.com"
  ]
}
```

| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **`orgId`** | `string` | 標籤屬性的IMS組織ID。 |
| **`dynamicCdnEnabled`** | `boolean` | 決定您的標籤屬性是否使用Adobe的動態CDN切換功能。 若設為`true`，則會根據訪客的位置自動切換訪客要求您標籤的CDN。 |
| **`cdnAllowList`** | `string[]` | 允許載入您標籤屬性的CDN。 |

`_satellite._container.company`中也包含類似的資訊。 如需詳細資訊，請參閱[`_container`](container.md)。
