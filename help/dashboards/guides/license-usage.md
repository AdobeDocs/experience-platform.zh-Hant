---
keywords: Experience Platform；用戶介面；UI；自定義；許可證使用儀表板；儀表板；許可證使用；權益；衝減
title: 授權使用儀表板
description: Adobe Experience Platform提供儀表板，您可透過儀表板檢視貴組織授權使用的重要資訊。
topic: 指南
type: 文件
translation-type: tm+mt
source-git-commit: 3908011b31dd24b13a58a2bc5ad5137dd3af5f63
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 3%

---


# （測試版）授權使用控制面板{#license-usage-dashboard}

>[!IMPORTANT]
>
>本檔案中概述的控制面板功能目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform用戶介面(UI)提供一個儀表板，通過該儀表板可以查看有關組織許可證使用情況的重要資訊（在每日快照中捕獲）。 本指南概述如何存取和使用UI中的授權使用控制面板，並提供有關控制面板中顯示視覺化的詳細資訊。

有關平台UI的一般概述，請訪問[Experience PlatformUI指南](../../landing/ui-guide.md)。

## 授權使用資料板資料

授權使用控制面板會顯示貴組織授權相關資料的快照以供Experience Platform。 儀表板中的資料與拍攝快照時在特定時間點顯示的資料完全相同。 換言之，快照不是資料的近似值或範例，而且控制面板不會即時更新。

>[!NOTE]
>
>自快照建立以來對資料所做的任何變更或更新，在下一個快照建立之前，不會反映在控制面板中。

## 探索授權使用儀表板

若要導覽至平台UI中的授權使用控制面板，請在左側導軌中選取「**[!UICONTROL 授權使用]**」。 此時會開啟&#x200B;**[!UICONTROL 概述]**&#x200B;標籤，顯示控制面板。

![](../images/license-usage/dashboard-overview.png)

### 選取沙盒

若要選擇要在儀表板中查看的沙盒，請選擇[!UICONTROL Production]或[!UICONTROL Development]。 選取的沙盒會以沙盒名稱旁的選項按鈕來指示。

>[!NOTE]
>
>相同類型的所有沙盒會累積沙盒的耗用量報告。 換言之，選擇[!UICONTROL Production]或[!UICONTROL Development]可分別針對所有生產或開發沙盒提供消費報表。

![](../images/license-usage/select-sandbox.png)

### 選擇日期範圍

選取沙盒後，您可以使用日期範圍下拉式清單來選取要在控制面板中顯示的時段。 有三種可用選項：[!UICONTROL 最近30天]、[!UICONTROL 最近90天]和[!UICONTROL 最近12個月]。 預設會選取最近30天。

![](../images/license-usage/select-date-range.png)

## 介面工具集

授權使用控制面板由Widget組成，其中顯示唯讀量度，提供有關貴組織授權使用的重要資訊。 可見度量取決於您組織的特定授權（如需詳細資訊，請參閱[可用度量](#available-metrics)一節）。

每個介面工具集都會顯示折線圖，比較貴組織的實際數量與貴組織的授權可用總數，並提供總使用量的百分比。

![](../images/license-usage/widgets.png)

## 可用量度

授權使用控制面板目前提供4個度量：

* [!UICONTROL 可定址對象] （依描述檔數量測量）
* [!UICONTROL 平均個人檔案豐富性]
* [!UICONTROL 已消耗的儲存總量]
* [!UICONTROL 每個區段的掃描資料]

這些量度的定義視貴組織已購買的授權而定。 如需每個度量的詳細定義，請參考適當的產品說明檔案：

| 授權 | 產品說明 |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD標準</li><li>Adobe Experience Platform:OD重</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>RT客戶資料平台：OD</li><li>RT客戶資料平台：OD PRFL到10M</li><li>RT客戶資料平台：OD PRF到50M</li></ul> | [即時客戶資料平台](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>AEP:OD啟動</li><li>AEP:OD啟動PRF至10M</li><li>AEP:OD啟動PRF最多50M</li></ul> | [Adobe Experience Platform啟動](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform情報](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |

## 後續步驟

閱讀本檔案後，您可以找到授權使用儀表板並選取要檢視的沙盒。 您也可以根據組織購買的授權，找到有關組織可用量度的更多資訊。

若要進一步瞭解Experience PlatformUI中的其他功能，請參閱[平台UI指南](../../landing/ui-guide.md)。