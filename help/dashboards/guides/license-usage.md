---
keywords: Experience Platform；用戶介面；UI；自定義；許可證使用面板；儀表板；許可證使用；權利；消耗
title: 許可證使用儀表板指南
description: Adobe Experience Platform提供了一個儀表板，您可以通過該儀表板查看有關組織許可證使用情況的重要資訊。
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 1%

---

# 許可證使用儀表板 {#license-usage-dashboard}

Adobe Experience Platform用戶介面(UI)提供了一個儀表板，您可以通過該儀表板查看有關組織許可證使用情況的重要資訊，這些資訊在每日快照中捕獲。 本指南概述了如何訪問和使用UI中的許可證使用儀表板，並提供了有關儀表板中顯示的可視化效果的詳細資訊。

有關平台UI的一般概述，請訪問 [Experience PlatformUI指南](../../landing/ui-guide.md)。

## 許可證使用儀表板資料

許可證使用儀表板顯示您組織與許可證相關的資料的快照，以便Experience Platform。 儀表板中的資料與拍攝快照時在特定時間點顯示的資料完全相同。 換句話說，快照不是資料的近似值或示例，儀表板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新不會反映在儀表板中，直到拍攝下一個快照。

## 瀏覽許可證使用儀表板

要導航到平台UI中的許可證使用儀表板，請選擇 **[!UICONTROL 許可證使用]** 左欄。 開啟 **[!UICONTROL 概述]** 頁籤。

>[!NOTE]
>
>預設情況下，未啟用許可證使用儀表板。 必須向用戶授予「查看許可證使用儀表板」權限才能查看儀表板。 有關授予訪問權限以查看許可證使用儀表板的步驟，請參閱 [儀表板權限指南](../permissions.md)。

![「許可證使用情況」儀表板「概述」頁籤。](../images/license-usage/dashboard-overview.png)

### 選擇沙盒

要選擇要在儀表板中查看的沙盒，請選擇 [!UICONTROL 生產] 或 [!UICONTROL 開發]。 所選沙盒由沙盒名稱旁邊的單選按鈕指示。

對於同一類型的所有沙箱，沙箱的消耗報告是累積的。 換句話說， [!UICONTROL 生產] 或 [!UICONTROL 開發] 分別為所有生產或開發沙箱提供消耗報告。

![突出顯示了沙盒選擇器的「許可證使用情況」儀表板「概述」頁籤。](../images/license-usage/select-sandbox.png)

>[!WARNING]
>
>必須在沙盒級別指定查看許可證使用儀表板的權限。 這意味著必須將查看儀表板的權限添加到每個沙箱。 這一限制將在以後的版本中解決。 同時，還提供了以下解決方法：
>
>1. 在Adobe Admin Console建立產品配置檔案。
>2. 在「沙盒」類別的「權限」下，添加您希望在許可證使用儀表板中查看的所有沙盒。
>3. 在「用戶儀表板權限」類別下，添加「查看許可證使用情況儀表板」權限。


### 選擇日期範圍

選擇沙盒後，可以使用日期範圍下拉清單選擇要在儀表板中顯示的時間段。 有多個可用選項，包括過去30天的預設值。

![「許可證使用情況」面板「概述」頁籤，其中突出顯示了日期範圍下拉清單。](../images/license-usage/select-date-range.png)

也可以選擇 **[!UICONTROL 自定義日期]** 來修改選定線條的屬性。

![「許可證使用情況」面板「概述」頁籤，其中突出顯示了自定義日期範圍選項。](../images/license-usage/select-custom-date.png)

## 小部件

許可證使用儀表板由小部件組成，這些部件顯示只讀度量，提供有關您組織的許可證使用情況的重要資訊。 可見的指標取決於您組織的特定許可(請參閱 [可用度量](#available-metrics) 的子菜單。

每個小部件都顯示一個折線圖，將組織的實際數字與組織許可的可用總數進行比較，並提供總使用量的百分比。

![「許可證使用情況」面板「概述」頁籤，其中突出顯示了「示例許可證使用情況」度量構件的線形圖。](../images/license-usage/widgets.png)

## 可用度量

許可證使用控制板報告四個關鍵指標，並在後續版本中添加更多指標。 可用度量包括：

* [!UICONTROL 可定址的受眾]
* [!UICONTROL 平均配置檔案豐富度]
* [!UICONTROL 每分段比率掃描的資料]
* [!UICONTROL 已消耗的儲存總量]

這些指標的可用性以及這些指標的具體定義會因貴組織購買的許可而有所不同。 有關每個指標的詳細定義，請參閱相應的產品說明文檔：

| 許可證 | 產品說明 |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD標準</li><li>Adobe Experience Platform:OD重</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform、應用服務和智慧服務](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT客戶資料平台：OD</li><li>RT客戶資料平台：OD PRFL到10M</li><li>RT客戶資料平台：OD PRFL到50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD激活</li><li>AEP:OD激活PRFL至10M</li><li>AEP:OD激活率最高達50米</li></ul> | [Adobe Experience Platform激活](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD智慧</li></ul> | [Adobe Experience Platform情報](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>Journey Optimizer選擇：OD</li><li>Journey Optimizer首相：OD</li><li>Journey Optimizer旗艦：OD</li><li>UNP AJO首要入門：OD</li><li>UNP AJO終極入門：OD</li><li>UNPReal-Time CDP:OD配置檔案業務流程</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/tw/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>許可證使用儀表板僅報告為您的組織設定的最新許可證。 如果為您的組織設定的最新許可證未顯示在上表中，則許可證使用儀表板可能無法正確顯示。 計畫在未來發佈對單個組織中的額外許可證和多個許可證的支援。

## 後續步驟

閱讀此文檔後，您可以找到許可證使用儀表板並選擇要查看的沙盒。 您還可以根據您的組織購買的許可證，找到有關組織可用指標的詳細資訊。

要瞭解有關Experience PlatformUI中其他功能的詳細資訊，請參閱 [平台UI指南](../../landing/ui-guide.md)。
