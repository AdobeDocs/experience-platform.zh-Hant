---
keywords: Experience Platform；使用者介面；UI；自訂；授權使用控制面板；控制面板；授權使用；權限；耗用
title: 授權使用控制面板指南
description: Adobe Experience Platform提供控制面板，讓您透過該控制面板檢視貴組織的授權使用情況重要資訊。
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 255de9b9e83c11aeed747a3c0cdb7bd7a7949bd2
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 1%

---

# 授權使用控制面板 {#license-usage-dashboard}

Adobe Experience Platform使用者介面(UI)提供控制面板，您可透過控制面板檢視有關組織授權使用的重要資訊，如每日快照中所擷取。 本指南概述如何存取和使用UI中的授權使用情況控制面板，並提供控制面板中所顯示視覺效果的詳細資訊。

如需Platform UI的一般概觀，請造訪 [Experience PlatformUI指南](../../landing/ui-guide.md).

## 許可證使用儀表板資料

許可證使用儀表板顯示貴組織與許可證相關的資料的快照，以便Experience Platform。 控制面板中的資料與拍攝快照時在特定時間點顯示的資料完全相同。 換言之，快照不是資料的近似值或樣本，控制面板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新都不會反映在儀表板中，直到拍攝下一個快照。

## 探索授權使用控制面板

若要導覽至Platform UI中的授權使用控制面板，請選取 **[!UICONTROL 授權使用]** 在左側邊欄。 這會開啟 **[!UICONTROL 概述]** 標籤來顯示控制面板。

>[!NOTE]
>
>預設不會啟用授權使用控制面板。 必須授予使用者「檢視授權使用量控制面板」權限，才能檢視控制面板。 有關授予訪問權限以查看許可證使用控制面板的步驟，請參閱 [控制面板權限指南](../permissions.md).

![「許可證使用情況」儀表板概述頁簽。](../images/license-usage/dashboard-overview.png)

### 選取沙箱

若要選擇要在控制面板中檢視的沙箱，請選取 [!UICONTROL 生產] 或 [!UICONTROL 開發]. 選取的沙箱會以沙箱名稱旁的選項按鈕指出。

相同類型的所有沙箱的耗用量報表都是累計的。 換句話說，選取 [!UICONTROL 生產] 或 [!UICONTROL 開發] 分別為所有生產或開發沙箱提供耗用量報表。

![反白顯示沙箱選取器時，「授權使用情況」控制面板「概述」標籤。](../images/license-usage/select-sandbox.png)

>[!WARNING]
>
>必須在沙箱層級指定檢視授權使用情況控制面板的權限。 這表示檢視控制面板的權限必須新增至每個個別沙箱。 此限制將於未來版本中解決。 同時，提供下列因應措施：
>
>1. 在Adobe Admin Console中建立產品設定檔。
>2. 在「沙箱」類別的「權限」下，新增您要在授權使用控制面板中檢視的所有沙箱。
>3. 在「使用者控制面板權限」類別下，新增「檢視授權使用控制面板」權限。


### 選擇日期範圍

選取沙箱後，您可以使用日期範圍下拉式清單，選取要在控制面板中顯示的時段。 有多個可用選項，包括過去30天的預設值。

![「授權使用情況」控制面板「概述」標籤，並反白顯示日期範圍下拉式清單。](../images/license-usage/select-date-range.png)

您也可以選取 **[!UICONTROL 自訂日期]** 來選擇顯示的時段。

![「授權使用控制面板概述」標籤，並反白顯示自訂日期範圍選項。](../images/license-usage/select-custom-date.png)

## 介面工具集

授權使用控制面板由Widget組成，Widget會顯示唯讀量度，提供貴組織授權使用的重要資訊。 可見的量度取決於貴組織的特定授權(請參閱 [可用量度](#available-metrics) 一節以取得詳細資訊)。

每個Widget都會顯示一個折線圖，比較貴組織的實際數量與貴組織授權時可用的總數，並提供總使用量的百分比。

![「許可證使用情況」儀表板「概述」頁簽，其中突出顯示「示例許可證使用情況」度量Widget的線形圖。](../images/license-usage/widgets.png)

## 可用量度

授權使用控制面板會報告四個關鍵量度，並在後續版本中新增更多量度。 可用的量度包括：

* [!UICONTROL 可定址對象]
* [!UICONTROL 平均設定檔豐富度]
* [!UICONTROL 每個細分比例的掃描資料]
* [!UICONTROL 總消耗儲存]

這些量度的可用性和每個量度的特定定義會因貴組織已購買的授權而異。 如需每個量度的詳細定義，請參閱適當的產品說明檔案：

| 授權 | 產品說明 |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD沈重</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform、應用程式服務與Intelligent Services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT客戶資料平台：OD</li><li>RT客戶資料平台：OD PRFL至10M</li><li>RT客戶資料平台：OD PRFL至50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD啟用</li><li>AEP:OD激活PRFL至10米</li><li>AEP:OD激活PRFL最多50米</li></ul> | [Adobe Experience Platform Activation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform情報](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>Journey Optimizer SELECT:OD</li><li>Journey Optimizer PRIME:OD</li><li>Journey Optimizer ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP Real-Time CDP:OD PROFILE ORCHESTRATION</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>授權使用控制面板只會報告貴組織已布建的最新授權。 如果為貴組織布建的最新授權未出現在上表中，則可能無法正確顯示授權使用控制面板。 未來版本預計會支援單一組織中的其他授權和多個授權。

## 後續步驟

閱讀本檔案後，您可以找到授權使用控制面板，並選取要檢視的沙箱。 您也可以根據組織已購買的授權，找到有關組織可用量度的詳細資訊。

若要進一步了解Experience PlatformUI中的其他可用功能，請參閱 [Platform UI指南](../../landing/ui-guide.md).
