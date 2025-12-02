---
title: _container
description: 檢視單一物件中的整個標籤容器。
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# `_container`

`_satellite._container`物件包含頁面上載入之標籤屬性的完整組態和執行階段內容。 此物件提供所有資訊，例如規則、資料元素、擴充功能和環境。 其主要用途是協助您對實作進行偵錯，讓您能夠確切瞭解已公開或發佈的邏輯。

```ts
readonly _satellite._container: {
  buildInfo: BuildInfo;
  company: Company;
  dataElements: { [name: string]: DataElement };
  environment: Environment;
  extensions: { [name: string]: Extension };
  property: Property;
  rules: Rule[];
}
```

>[!IMPORTANT]
>
>此物件僅供偵錯之用。 請勿將生產邏輯連結至此物件、在實施中參考此物件，或編輯此物件內的值。 Adobe可隨時變更此物件中屬性或名稱的可用性。

## 可用欄位

下列物件可供參考：

```json
{
  "buildInfo": {
    "minified": true,
    "buildDate": "YYYY-06-13T01:22:12Z"
  },
  "company": {
    "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
    "dynamicCdnEnabled": true,
    "cdnAllowList": [ "assets.adobedtm.com" ]
  },
  "dataElements": { ... },
  "environment": {
    "id": "EN6b2...d6ff2",
    "stage": "production"
  },
  "extensions": {
    "adobe-alloy": { ... },
    "core": { ... },
    "common-web-sdk-plugins": { ... }
  },
  "property": {
    "name": "Example tag property",
    "settings": {
      "domains": [ "example.com" ],
      "undefinedVarsReturnEmpty": false,
      "ruleComponentSequencingEnabled": true
    },
    "id": "PR845...6cf92"
  },
  "rules": [ { ... } ]
}
```

## `buildInfo`

`_satellite._container.buildInfo`物件包含[`_satellite.buildInfo`](buildinfo.md)的復本。

```ts
readonly _satellite._container.buildInfo: {
  minified: boolean;
  buildDate: string;
  turbineBuildDate: string;
  turbineVersion: string;
}
```

## `company`

`_satellite._container.company`物件包含[`_satellite.company`](company.md)的復本。

```ts
readonly _satellite._container.company: {
  orgId: string;
  dynamicCdnEnabled: boolean;
  cdnAllowList: string[];
}
```

## `dataElements`

`_satellite._container.dataElements`物件提供標籤屬性中所有資料元素的參考。

```ts
readonly _satellite._container.dataElements: {
  [name: string]: {
    modulePath: string;
    settings: Settings; // Varies by data element type
  }
}
```

每個資料元素都包含下列屬性：

| 名稱 | 類型 | 說明 |
|---|---|---|
| **`modulePath`** | `string` | 決定該資料元素型別邏輯的JavaScript檔案路徑。 |
| **`settings`** | `Settings` | 資料元素的設定。 此物件中的屬性取決於資料元素型別。 |

## `environment`

`_satellite._container.environment`物件包含[`_satellite.environment`](environment.md)的復本。

```ts
readonly _satellite._container.environment: {
  id: string;
  stage: string;
}
```

## `extensions`

`_satellite._container.extensions`物件會列出發佈至標籤屬性的所有延伸模組。

```ts
readonly _satellite._container.extensions: {
  [name: string]: {
    displayName: string;
    hostedLibFilesUrl: string;
    modules: Modules; // Extension-specific module definitions
  }
}
```

每個擴充功能包含下列屬性：

| 名稱 | 類型 | 說明 |
|---|---|---|
| **`displayName`** | `string` | 擴充功能的易記名稱。 |
| **`hostedLibFilesUrl`** | `string` | 擴充功能在CDN上的所在位置。 |
| **`modules`** | `Modules` | 擴充功能使用之所有事件、動作、條件和資料元素的JavaScript邏輯。 每個擴充功能的此物件內容不同。 |

## `property`

`_satellite._container.property`物件提供標籤屬性本身的相關資訊。

```ts
readonly _satellite._container.property: {
  id: string;
  name: string;
  settings: {
    domains: string[];
    ruleComponentSequencingEnabled: boolean;
    undefinedVarsReturnEmpty: boolean;
  };
}
```

| 名稱 | 類型 | 說明 |
|---|---|---|
| **`id`** | `string` | 標籤屬性的唯一識別碼。 |
| **`name`** | `string` | 標籤屬性的易記名稱。 |
| **`settings`** | `PropertySettings` | 此屬性的設定。 請參閱下表。 |

| 設定名稱 | 類型 | 說明 |
|---|---|---|
| **`domains`** | `string[]` | 屬性已設定的網域，如[設定標籤屬性](/help/tags/ui/administration/companies-and-properties.md)時所設定。 |
| **`ruleComponentSequencingEnabled`** | `boolean` | 決定設定標籤屬性時是否啟用核取方塊&#x200B;**[!UICONTROL Run rule components in sequence]**。 |
| **`undefinedVarsReturnEmpty`** | `boolean` | 決定設定標籤屬性時是否啟用核取方塊&#x200B;**[!UICONTROL Return an empty string for undefined data elements]**。 |

## `_container.rules`

`rules`物件陣列提供標籤屬性中所有規則的參考。

```ts
readonly _satellite._container.rules: {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}[]
```

每個規則都包含以下欄位：

| 名稱 | 類型 | 說明 |
|---|---|---|
| **`id`** | `string` | 規則的唯一識別碼。 |
| **`name`** | `string` | 規則的易記名稱。 |
| **`events`** | `Event[]` | 您已設定用來觸發規則的事件陣列。 |
| **`conditions`** | `Condition[]` | 您已設定用來觸發規則的條件陣列。 |
| **`actions`** | `Action[]` | 您已設定要在規則觸發時執行的一系列動作。 |
