---
title: 環境
description: 標籤屬性目前使用的組建環境。
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 6%

---

# `environment`

`_satellite.environment`物件會指出標籤屬性目前使用的組建環境。

```js
readonly _satellite.environment: Environment
```

## 可用欄位

呼叫此物件時，可使用下列欄位。

```json
{
  "id": "EN6b2...d6ff2",
  "stage": "production"
}
```

| 名稱 | 類型 | 說明 |
|---|---|---|
| **`id`** | `string` | 環境的唯一識別碼。 您可以在標籤UI中選取&#x200B;**[!UICONTROL Install]**&#x200B;下的[[!UICONTROL Environments]](/help/tags/ui/publishing/environments.md)圖示，以找出環境ID。 |
| **`stage`** | `development \| staging \| production` | 環境型別。 |
