---
keywords: Experience Platform；身份；身份服務；疑難解答；guardrails;guidentity;identity service;troubleshooting;guardrails;guidelines;limit;
title: 標識服務的護欄
description: 本文檔提供有關Identity Service資料的使用和費率限制的資訊，以幫助您優化對身份圖的使用。
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 2%

---

# 用於 [!DNL Identity Service] 資料

本文檔提供有關使用和費率限制的資訊 [!DNL Identity Service] 資料，幫助您優化標識圖形的使用。 在查看以下護欄時，假定您已正確建模了資料。 如果您對如何建模資料有疑問，請與客戶服務代表聯繫。

## 快速入門

以下Experience Platform服務涉及對身份資料建模：

* [身份](home.md):將不同資料源的標識插入平台時進行橋接。
* [[!DNL Real-Time Customer Profile]](../profile/home.md):使用來自多個源的資料建立統一的使用者配置檔案。

## 資料模型限制

下表提供了靜態限制的護欄以及標識命名空間要考慮的驗證規則。

### 靜態限制

下表概述了應用於標識資料的靜態限制。

| 瓜德賴爾 | 限制 | 附註 |
| --- | --- | --- |
| 圖中的恆等式數 | 150 | 該限制在沙盒級別應用。 一旦達到限制，將不會更新標識圖。 **注釋**:標識圖中的最大標識數 **用於單個合併的配置檔案** 是50 基於身份圖的合併配置式（具有50個以上身份）將從即時客戶配置式中排除。 有關詳細資訊，請閱讀上的指南 [配置檔案資料的護欄](../profile/guardrails.md)。 |
| XDM記錄中的標識數 | 20 | 所需的XDM記錄的最小數量為2。 |
| 自定義命名空間數 | None | 可以建立的自定義命名空間數目沒有限制。 |
| 圖數 | None | 您可以建立的標識圖數沒有限制。 |
| 命名空間顯示名稱或標識符號的字元數 | None | 命名空間顯示名稱或標識符號的字元數沒有限制。 |

### 標識值驗證

下表概述了必須遵循的現有規則，以確保成功驗證您的標識值。

| 命名空間 | 驗證規則 | 違反規則時的系統行為 |
| --- | --- | --- |
| ECID | <ul><li>ECID的標識值必須正好是38個字元。</li><li>ECID的標識值必須只包含數字。</li></ul> | <ul><li>如果ECID的標識值不是正好38個字元，則跳過記錄。</li><li>如果ECID的標識值包含非數字字元，則跳過記錄。</li></ul> |
| 非ECID | 標識值不能超過1024個字元。 | 如果標識值超過1024個字元，則跳過記錄。 |

### 標識名稱空間攝取

從2023年3月31日起，Identity Service將阻止新客戶接收Adobe AnalyticsID(AAID)。 此身份通常通過 [Adobe Analytics源](../sources/connectors/adobe-applications/analytics.md) 和 [Adobe Audience Manager源](../sources//connectors/adobe-applications/audience-manager.md) 且冗餘，因為ECID代表同一Web瀏覽器。 如果要更改此預設配置，請與Adobe帳戶團隊聯繫。

## 後續步驟

有關 [!DNL Identity Service]:

* [[!DNL Identity Service] 概覽](home.md)
* [標識圖形查看器](ui/identity-graph-viewer.md)
