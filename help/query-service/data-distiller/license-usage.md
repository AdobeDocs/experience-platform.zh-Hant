---
title: 監視批次查詢授權使用情況
description: Adobe Experience Platform UI提供控制面板，讓您檢視有關組織Data Distiller授權使用情況的重要資訊。
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: f3542105e423633e2bdf0f8e8501c1a1dc200f32
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 監視批次查詢授權使用情況 {#monitor-license-usage}

授權使用儀表板提供關於貴組織查詢服務授權使用情況和每個所購買產品使用量度的詳細報告。 若要進一步瞭解儀表板中顯示的可用量度，請造訪[授權使用儀表板指南](../../dashboards/guides/license-usage.md#available-metrics)。

控制面板提供每個已購買產品的使用量度、所有生產或開發沙箱中量度的整合使用量，以及特定沙箱的使用量度。 此處顯示的資訊是在Platform執行個體的每日快照期間擷取。

>[!NOTE]
>
>授權使用儀表板預設為未啟用。 必須授予使用者「檢視授權使用儀表板」許可權才能檢視儀表板。 如需授與存取許可權以檢視授權使用儀表板的步驟，請參閱[儀表板許可權指南](../../dashboards/permissions.md)。

## 計算時數 {#compute-hours}

[!UICONTROL 計算時數]量度僅適用於擁有Data Distiller授權進行批次查詢的客戶。 [!UICONTROL 計算時數]是查詢服務引擎在執行批次查詢時，讀取、處理及將資料寫入資料湖所花費的時間測量值。

>[!NOTE]
>
>**[!UICONTROL 計算時數]資料有限制**：資料從2023年10月1日開始，沒有趨勢。

![已反白計算時數量度的授權使用儀表板。](../images/data-distiller/compute-hours.png)

若要根據貴組織購買的授權，尋找貴組織可用量度的詳細資訊，請參閱[授權使用儀表板指南](../../dashboards/guides/license-usage.md)。
