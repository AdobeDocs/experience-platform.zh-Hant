---
title: 使用NPM套件安裝網頁SDK
description: 使用NPM套件來安裝和參考網頁SDK程式庫。
exl-id: 4c70ec5d-33fd-4ef7-ba9e-5b92ff6c3e86
source-git-commit: 8b6c958613923127880263679ce00ce359151300
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 使用NPM套件安裝網頁SDK

Adobe Experience Platform Web SDK是以[NPM套件](https://www.npmjs.com)的形式提供。 安裝NPM套件可讓您控制Adobe Experience Platform Web SDK JavaScript程式庫的建置流程。 NPM套件會公開要在瀏覽器中執行的EcmaScript 5版模組或EcmaScript 2015版(ES6)模組。

```bash
npm install @adobe/alloy
```

Adobe Experience Platform Web SDK的NPM套件會公開`createInstance`函式。 傳遞給函式的名稱選項可控制記錄中使用的首碼。 以下是使用套件的範例。

## 將套件用作ECMAScript 2015 (ES6)模組

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("configure", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM套件仰賴CommonJS模組；因此，使用套件組合時，請確定套件組合支援CommonJS模組。 某些套件組合（例如[Rollup](https://rollupjs.org)）需要提供CommonJS支援的[外掛程式](https://www.npmjs.com/package/@rollup/plugin-commonjs)。

## 將套件用作ECMAScript 5模組

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("configure", { ... });
alloy("sendEvent", { ... });
```
