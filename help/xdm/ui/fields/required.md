---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；必要；欄位；
title: 在UI中定義必填欄位
description: 瞭解如何在Experience Platform使用者介面中定義必要的XDM欄位。
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 在UI中定義必填欄位

在Experience Data Model (XDM)中，必填欄位指出必須提供有效值，才能在資料擷取期間接受特定記錄或時間序列事件。 必填欄位的常見使用案例包括使用者身分資訊和時間戳記。

>[!IMPORTANT]
>
>無論結構描述欄位是否為必要欄位，Experience Platform都不會接受任何已擷取欄位的`null`或空白值。 如果記錄或事件中沒有特定欄位的值，則應該從擷取裝載中排除該欄位的索引鍵。

在Adobe Experience Platform使用者介面中定義[新欄位](./overview.md#define)時，您可以選取右側邊欄中的&#x200B;**[!UICONTROL 必要]**&#x200B;核取方塊，將其設定為必要欄位。 選取&#x200B;**[!UICONTROL 套用]**&#x200B;以套用變更至結構描述。

![必要的核取方塊](../../images/ui/fields/required/root.png)

如果欄位是租使用者ID物件下的根層級屬性，則其路徑會立即顯示在左側邊欄的&#x200B;**[!UICONTROL 必要欄位]**&#x200B;下。

![根級必要欄位](../../images/ui/fields/required/applied.png)

但是，如果必要欄位巢狀內嵌在未標籤為必要本身的物件中，則巢狀欄位不會出現在左側邊欄的&#x200B;**[!UICONTROL 必要欄位]**&#x200B;下。

在下列範例中，`internalSKU`欄位已設定為必要，但其父物件`SKUs`不是。 在此情況下，如果擷取資料時排除`SKUs`，即使子欄位`internalSKU`標籤為必要，也不會發生驗證錯誤。 換言之，雖然`SKUs`是選擇性的，但它必須包含事件中的`internalSKU`欄位。

![巢狀必要欄位](../../images/ui/fields/required/nested.png)

如果您希望結構描述中一律需要巢狀欄位，您也必須視需要設定所有父欄位（租使用者ID物件除外）。

![父項和子項必要欄位](../../images/ui/fields/required/parent-and-child.png)

## 後續步驟

本指南說明如何在UI中定義必要欄位。 請參閱[在UI](./overview.md#special)中定義欄位的概觀，瞭解如何在[!DNL Schema Editor]中定義其他XDM欄位型別。
