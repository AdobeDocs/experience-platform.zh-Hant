---
title: edgbasePath
description: 用來與Adobe服務互動的端點基本路徑。
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 1fa7b48f99948a5252635dc1a8c5142fea5df57b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# `edgeBasePath`

當您與Adobe服務互動時，`edgeBasePath`屬性會變更目的地路徑。 如果您參與Alpha或Beta程式以收集資料，Adobe可能會要求您變更此變數。 大多陣列織不需要設定或變更此屬性。

執行`edgeBasePath`命令時設定`configure`文字欄位。 如果您省略此屬性，其預設值為`ee`。 Adobe建議您在大部分的設定中省略此屬性。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```

## 使用Web SDK標籤擴充功能的Edge基本路徑

設定標籤延伸時，此欄位的Web SDK標籤延伸對應項位於[進階組態設定](/help/tags/extensions/client/web-sdk/configure/advanced-settings.md)之下。
