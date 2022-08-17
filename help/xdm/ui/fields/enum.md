---
keywords: Experience Platform；首頁；熱門主題；api;API;XDM;XDM系統；經驗資料模型；資料模型；ui;workspace;enum;field;
solution: Experience Platform
title: 在UI中定義枚舉欄位
description: 瞭解如何在Experience Platform用戶介面中定義枚舉欄位。
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: f6fefda974d2ae6fd4b035ef3b5fe633311c9772
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---

# 在UI中定義枚舉欄位 {#enum}

>[!CONTEXTUALHELP]
>id="platform_xdm_enumsuggestedvalue"
>title="枚舉和建議值"
>abstract="枚舉將字串欄位限制為只允許接收與預定義值集匹配的資料。 或者，可以為欄位定義一組建議值，這些值不限制攝取，而是定義可在分段中選擇的屬性。 如需詳細資訊，請參閱文件。"

在經驗資料模型(XDM)中，枚舉欄位表示一個欄位，該欄位被約束為預定義的可接受值清單。

當 [定義新欄位](./overview.md#define) 在Adobe Experience Platform用戶介面中，通過選擇 **[!UICONTROL 枚舉]** 的子菜單。

![](../../images/ui/fields/special/enum.png)

選中該複選框後，將顯示附加控制項，允許您指定枚舉的值約束。 在 **[!UICONTROL 值]** 列中，必須提供要將欄位限制為的準確值。 此值必須符合 [!UICONTROL 類型] 已為枚舉欄位選擇。 您可以選擇提供人性化 **[!UICONTROL 標籤]** 也是。

要向枚舉添加其他約束，請選擇 **[!UICONTROL 添加行]**。

![](../../images/ui/fields/special/enum-add-row.png)

繼續將所需約束和可選標籤添加到枚舉。 完成後，選擇 **[!UICONTROL 應用]** 將更改應用到架構。

![](../../images/ui/fields/special/enum-configured.png)

畫布將更新以反映更改。 將來當您瀏覽此架構時，可以查看和編輯右欄中枚舉欄位的約束。

![](../../images/ui/fields/special/enum-applied.png)

## 後續步驟

本指南介紹了如何在UI中定義枚舉欄位。 請參閱 [定義UI中的欄位](./overview.md#special) 瞭解如何在 [!DNL Schema Editor]。
