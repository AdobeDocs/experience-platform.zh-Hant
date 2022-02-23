---
keywords: Experience Platform；身份；身份服務；疑難解答；guardrails;guidentity;identity service;troubleshooting;guardrails;guidelines;limit;
title: 標識服務的護欄
description: 本文檔提供有關Identity Service資料的使用和費率限制的資訊，以幫助您優化對身份圖的使用。
source-git-commit: b36ace84acdb13b89deb6f77a02c298acade8d8e
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 3%

---

# 用於 [!DNL Identity Service] 資料

本文檔提供有關使用和費率限制的資訊 [!DNL Identity Service] 資料，幫助您優化標識圖形的使用。 在查看以下護欄時，假定您已正確建模了資料。 如果您對如何建模資料有疑問，請與客戶服務代表聯繫。

## 快速入門

以下Experience Platform服務涉及對身份資料建模：

* [身份](home.md):將不同資料源的標識插入平台時進行橋接。
* [[!DNL Real-time Customer Profile]](../profile/home.md):使用來自多個源的資料建立統一的使用者配置檔案。

## 資料模型限制

下表提供了靜態限制的護欄以及標識命名空間要考慮的驗證規則。

### 靜態限制

下表概述了應用於標識資料的靜態限制。

| 瓜德賴爾 | 限制 | 附註 |
| --- | --- | --- |
| 圖中的恆等式數 | 150 | 一旦達到限制，將不會更新標識圖。 |
| XDM記錄中的標識數 | 20 | 所需的XDM記錄的最小數量為2。 |
| 自定義命名空間數 | None | 可以建立的自定義命名空間數目沒有限制。 |
| 圖數 | 無 | 您可以建立的標識圖數沒有限制。 |
| 命名空間顯示名稱或標識符號的字元數 | 無 | 命名空間顯示名稱或標識符號的字元數沒有限制。 |

### 標識值驗證

下表概述了必須遵循的現有規則，以確保成功驗證您的標識值。

| 命名空間 | 驗證規則 | 違反規則時的系統行為 |
| --- | --- | --- |
| ECID | <ul><li>ECID的標識值必須正好是38個字元。</li><li>ECID的標識值必須只包含數字。</li></ul> | <ul><li>如果ECID的標識值不是正好38個字元，則跳過記錄。</li><li>如果ECID的標識值包含非數字字元，則跳過記錄。</li></ul> |
| 非ECID | 標識值不能超過1024個字元。 | 如果標識值超過1024個字元，則跳過記錄。 |

## 後續步驟

有關 [!DNL Identity Service]:

* [[!DNL Identity Service] 概觀](home.md)
* [標識圖形查看器](ui/identity-graph-viewer.md)
