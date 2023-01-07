---
keywords: Experience Platform；首頁；熱門主題；API;API;XDM;XDM系統；體驗資料模型；資料模型；ui；工作區；必要；欄位；
title: 在UI中定義必要欄位
description: 了解如何在Experience Platform使用者介面中定義必要的XDM欄位。
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 在UI中定義必填欄位

在Experience Data Model(XDM)中，必填欄位指出必須提供有效值，才能在資料擷取期間接受特定記錄或時間序列事件。 必要欄位的常見使用案例包括使用者身分資訊和時間戳記。

>[!IMPORTANT]
>
>無論架構欄位是否為必要，Platform都不接受 `null` 或任何擷取欄位的空白值。 如果記錄或事件中沒有特定欄位的值，則應從擷取裝載中排除該欄位的金鑰。

當 [定義新欄位](./overview.md#define) 在Adobe Experience Platform使用者介面中，您可以選取 **[!UICONTROL 必填]** 核取方塊。 選擇 **[!UICONTROL 套用]** 將更改應用到架構。

![必要核取方塊](../../images/ui/fields/required/root.png)

如果欄位是租用戶ID物件下的根層級屬性，其路徑會立即顯示在 **[!UICONTROL 必填欄位]** 在左側邊欄。

![根級必填欄位](../../images/ui/fields/required/applied.png)

但是，如果在未標示為必要本身的物件中巢狀內嵌必要欄位，則巢狀欄位不會顯示在下方 **[!UICONTROL 必填欄位]** 在左側邊欄。

在以下範例中， `internalSKU` 欄位設為必要，但其上層物件 `SKUs` 不是。 在此情況下，若 `SKUs` 即使子欄位，擷取資料時仍會排除 `internalSKU` 已標示為必要。 換句話說， `SKUs` 為選用項目，必須包含 `internalSKU` 欄位。

![巢狀必填欄位](../../images/ui/fields/required/nested.png)

如果您希望結構中的巢狀欄位一律為必要欄位，您也必須視需要設定所有父欄位（租用戶ID物件除外）。

![父欄位和子欄位](../../images/ui/fields/required/parent-and-child.png)

## 後續步驟

本指南說明如何在UI中定義必要欄位。 請參閱 [定義UI中的欄位](./overview.md#special) 若要了解如何定義 [!DNL Schema Editor].
