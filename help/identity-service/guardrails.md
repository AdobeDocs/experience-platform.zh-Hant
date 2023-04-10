---
keywords: Experience Platform；身分；身分服務；疑難排解；護欄；准則；限制；
title: Identity Service的護欄
description: 本檔案提供Identity Service資料的使用和比率限制資訊，協助您最佳化身分圖表的使用。
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 2%

---

# 的護欄 [!DNL Identity Service] 資料

本檔案提供的使用和費率限制資訊 [!DNL Identity Service] 資料可協助您最佳化身分圖表的使用方式。 檢閱下列護欄時，會假設您已正確模型化資料。 若您對如何建立資料模型有任何疑問，請連絡您的客戶服務代表。

## 快速入門

下列Experience Platform服務與模型身分資料有關：

* [身分](home.md):擷取不同資料來源的身分並匯整至Platform中時，將其橋接。
* [[!DNL Real-Time Customer Profile]](../profile/home.md):使用來自多個來源的資料建立統一的消費者設定檔。

## 資料模型限制

下表提供靜態限制護欄的指引，以及要針對身分命名空間考慮的驗證規則。

### 靜態限制

下表概述套用至身分資料的靜態限制。

| 瓜德拉伊 | 限制 | 附註 |
| --- | --- | --- |
| 圖表中的身分數 | 150 | 此限制會套用至沙箱層級。 一旦達到限制，就不會更新身分圖表。 **附註**:身分圖中的身分數上限 **個別合併的設定檔** 是50。 根據身分圖表（具有超過50個身分）合併的設定檔，會從「即時客戶設定檔」中排除。 如需詳細資訊，請參閱 [設定檔資料的護欄](../profile/guardrails.md). |
| XDM記錄中的身分數 | 20 | 所需的XDM記錄最少為2個。 |
| 自訂命名空間數量 | None | 您可以建立的自訂命名空間數目沒有限制。 |
| 圖數 | None | 您可以建立的身分圖數沒有限制。 |
| 命名空間顯示名稱或標識符號的字元數 | None | 命名空間顯示名稱或標識符號的字元數沒有限制。 |

### 身分值驗證

下表概述您必須遵循的現有規則，以確保身分值的驗證成功。

| 命名空間 | 驗證規則 | 違反規則時的系統行為 |
| --- | --- | --- |
| ECID | <ul><li>ECID的身分值必須恰好為38個字元。</li><li>ECID的身分值只能由數字組成。</li></ul> | <ul><li>如果ECID的身分值不是確切的38個字元，則會略過記錄。</li><li>如果ECID的身分值包含非數字字元，系統會略過記錄。</li></ul> |
| 非ECID | 身分值不能超過1024個字元。 | 如果標識值超過1024個字元，則跳過該記錄。 |

### 身分命名空間擷取

自2023年3月31日起，Identity Service將封鎖新客戶擷取Adobe Analytics ID(AAID)的程式。 此身分識別通常會透過 [Adobe Analytics來源](../sources/connectors/adobe-applications/analytics.md) 和 [Adobe Audience Manager來源](../sources//connectors/adobe-applications/audience-manager.md) 且是多餘的，因為ECID代表相同的Web瀏覽器。 如果您想要變更此預設設定，請連絡您的Adobe帳戶團隊。

## 後續步驟

如需詳細資訊，請參閱下列檔案 [!DNL Identity Service]:

* [[!DNL Identity Service] 概覽](home.md)
* [身分圖表檢視器](ui/identity-graph-viewer.md)
