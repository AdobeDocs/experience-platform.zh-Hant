---
title: 使用NPM套件安裝Web SDK
description: 使用NPM套件來安裝和參考Web SDK程式庫。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# 使用NPM套件安裝Web SDK

Adobe Experience Platform Web SDK現已推出 [NPM套件](https://www.npmjs.com). 安裝NPM套件可讓您控制Adobe Experience Platform Web SDK JavaScript程式庫的建置流程。 NPM套件會公開要在瀏覽器中執行的EcmaScript 5版模組或EcmaScript 2015版(ES6)模組。

```bash
npm install @adobe/alloy
```

Adobe Experience Platform Web SDK的NPM套件會公開 `createInstance` 函式。 傳遞給函式的名稱選項可控制記錄中使用的首碼。 以下是使用套件的範例。

## 將套件用作ECMAScript 2015 (ES6)模組

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM套件仰賴CommonJS模組；因此，使用套件組合時，請確定套件組合支援CommonJS模組。 部分套件組合，例如 [統計](https://rollupjs.org)，需要 [外掛程式](https://www.npmjs.com/package/@rollup/plugin-commonjs) 提供CommonJS支援。

## 將套件用作ECMAScript 5模組

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```
