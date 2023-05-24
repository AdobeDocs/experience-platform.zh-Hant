---
keywords: Experience Platform；首頁；熱門主題；api;API;XDM;XDM系統；經驗資料模型；資料模型；ui;workspace;required;field;
title: 在UI中定義必填欄位
description: 瞭解如何在Experience Platform用戶介面中定義所需的XDM欄位。
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 在UI中定義必填欄位

在「體驗資料模型」(XDM)中，必填欄位指示必須提供一個有效值，以便在資料接收期間接受特定記錄或時間序列事件。 必填欄位的常用用例包括用戶標識資訊和時間戳。

>[!IMPORTANT]
>
>無論是否需要架構欄位，平台都不接受 `null` 或任何已接收欄位的空值。 如果記錄或事件中沒有特定欄位的值，則應將該欄位的鍵從接收負載中排除。

當 [定義新欄位](./overview.md#define) 在Adobe Experience Platform用戶介面中，通過選擇 **[!UICONTROL 必需]** 的子菜單。 選擇 **[!UICONTROL 應用]** 將更改應用到架構。

![必需複選框](../../images/ui/fields/required/root.png)

如果欄位是租戶ID對象下的根級屬性，則其路徑將立即顯示在 **[!UICONTROL 必填欄位]** 左欄。

![根級別必填欄位](../../images/ui/fields/required/applied.png)

但是，如果必需欄位嵌套在未標籤為必需的對象中，則嵌套欄位不會顯示在 **[!UICONTROL 必填欄位]** 左欄。

在下面的示例中， `internalSKU` 欄位設定為必需，但其父對象 `SKUs` 不。 在這種情況下，如果 `SKUs` 在接收資料時被排除，即使子欄位 `internalSKU` 標籤為必需。 換句話說， `SKUs` 是可選的，它必須包含 `internalSKU` 的子菜單。

![嵌套的必填欄位](../../images/ui/fields/required/nested.png)

如果希望方案中始終需要嵌套欄位，則還必鬚根據需要設定所有父欄位（租戶ID對象除外）。

![父欄位和子欄位](../../images/ui/fields/required/parent-and-child.png)

## 後續步驟

本指南介紹如何在UI中定義必需欄位。 請參閱 [定義UI中的欄位](./overview.md#special) 瞭解如何在 [!DNL Schema Editor]。
