---
title: Adobe Experience 平台發行說明
description: Adobe Experience Platform的最新發行說明。
source-git-commit: 641fcab89b849d91a075fa5058421950bc7fecd7
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 9%

---

# Adobe Experience Platform 發行說明

**發行日期：2021 年 1 月 26 日**

Adobe Experience Platform 現有功能更新：

- [警報](#alerts)
- [資料準備](#data-prep)
- [沙盒](#sandboxes)
- [分段服務](#segmentation)

## 警報 {#alerts}

Experience Platform允許您訂閱各種平台活動的基於事件的警報。 您可以通過 [!UICONTROL 警報] 頁籤，並可以選擇在UI本身或通過電子郵件通知接收警報消息。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 新警報規則 | 現在，幾個新的警報規則可用於與資料接收、身份、配置檔案、分段和激活相關的工作流。 請參閱 [警報規則](../../observability/alerts/rules.md) 的子菜單。 |

有關平台中警報的詳細資訊，請參閱 [警報概述](../../observability/alerts/overview.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 整合的映射體驗 | 平台UI中的新映射介面為您提供了一致的映射體驗，讓您能夠利用智慧映射建議案、手動配置映射規則以及調試映射集上發生的任何錯誤。 有關詳細資訊，請參見 [[!DNL Data Prep] UI指南](../../data-prep/home.md)。 |

有關 [!DNL Data Prep]，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform的建設旨在在全球範圍內豐富數字型驗應用。 公司通常並行運行多個數字型驗應用程式，需要滿足這些應用程式的開發、測試和部署需要，同時確保操作合規性。 為了滿足這一需要，Experience Platform提供了沙箱，可將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| Sandboxes UI增強 | 沙盒指示器現在整合在所有平台UI應用程式的標頭中。 沙盒指示器顯示沙盒名稱、區域和類型，還允許您訪問下拉菜單以在沙盒之間切換。 有關詳細資訊，請參見 [沙盒UI指南](../../sandboxes/ui/user-guide.md)。 |

有關沙箱的詳細資訊，請參閱 [箱概述](../../sandboxes/home.md)。

## 分段服務 {#segmentation}

[!DNL Segmentation Service] 通過描述區分客戶群中可銷售人員組的標準來定義特定配置檔案子集。 段可以基於記錄資料（如人口統計資訊）或表示客戶與您品牌的交互的時間序列事件。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 段匹配 | 段匹配是一種資料協作服務，允許兩個或更多平台用戶以安全、受管理和隱私友好的方式基於公共標識符交換資料。 有關詳細資訊，請參見 [段匹配概述](../../segmentation/ui/segment-match/overview.md)。 |

有關 [!DNL Segmentation Service]，請參閱 [分段概述](../../segmentation/home.md)。
