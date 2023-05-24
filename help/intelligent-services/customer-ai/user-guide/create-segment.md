---
keywords: Experience Platform；洞察力；客戶ai；熱門主題；客戶ai段
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 使用預測分數建立客戶段
description: 當預測運行完成時，預測傾向分數由Profiles自動消耗。 利用客戶AI分數豐富配置檔案允許建立客戶段，以便根據其傾向分數查找受眾。 本節提供了使用段生成器建立段的步驟。
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 建立具有預測分值的客戶段

當預測運行完成時，預測傾向分數由Profiles自動消耗。 利用客戶AI分數豐富配置檔案允許建立客戶段，以便根據其傾向分數查找受眾。 本節提供了使用段生成器建立段的步驟。 有關建立段的更強健的教程，請參見 [段生成器使用手冊](../../../segmentation/ui/segment-builder.md)。

>[!IMPORTANT]
>
>為了利用此方法，需要為資料集啟用即時客戶配置檔案。

在平台UI中，按一下 **[!UICONTROL 段]** ，然後按一下 **[!UICONTROL 建立段]**。

![](../images/user-guide/segments.png)

的 **段生成器** 的子菜單。 左起 **[!UICONTROL 欄位]** 列和 **[!UICONTROL 屬性]** 頁籤，按一下名為 **[!UICONTROL XDM個人配置檔案]** 然後，按一下具有組織名稱空間的資料夾。 名為的資料夾 **[!UICONTROL 客戶AI]** 包含預測運行的結果，並以分值所屬的實例命名。 按一下實例資料夾以訪問其所需實例的結果。

![](../images/user-guide/results.png)

位於段生成器的中心，拖放 **[!UICONTROL 得分]** 屬性 *規則生成器畫布* 的子菜單。

右下 *段屬性* 列，提供段的名稱。

![](../images/user-guide/properties.png)

在左手上方 *欄位* 列，按一下 **齒輪** 表徵圖並選擇 *合併策略* 從下拉清單中。 按一下 **[!UICONTROL 保存]** 的子菜單。

![](../images/user-guide/merge_policy.png)

## 後續步驟

通過本教程，您已使用段生成器根據受眾的傾向得分成功找到受眾。 現在，您可以通過將受眾激活到目標來瞄準他們。 查看 [目標概述](../../../destinations/home.md) 的子菜單。
