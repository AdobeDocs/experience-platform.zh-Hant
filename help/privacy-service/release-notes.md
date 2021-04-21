---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service發行說明
topic-legacy: release notes
description: Adobe Experience Platform Privacy Service的最新發行說明。
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---

# [!DNL Privacy Service] 發行說明

本檔案包含有關Adobe Experience Platform[!DNL Privacy Service]的新功能，以及增強功能和重要錯誤修正的資訊。

>[!NOTE]
>
>其他[!DNL Experience Platform]服務的最新發行說明位於[此處](../release-notes/latest/latest.md)。

## 2020 年 9 月 9 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| 支援LGPD（巴西） | 現在，可以根據巴西的[!DNL Lei Geral de Proteção de Dados](LGPD)法規建立隱私工作。 這些作業在規則代碼`lgpd_bra`下被追蹤。 |

## 2020 年 4 月 8 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| PDPA支援 | [!DNL Privacy] 現在，您可以根據泰國的個人資料保護法(PDPA)來建立和追蹤要求。在API中提出隱私權要求時，`regulation`陣列接受值&quot;pdpa_tha&quot;。 |
| UI中的名稱空間類型 | 您現在可以在[!DNL Privacy Service] UI的「請求產生器」中指定不同的命名空間類型。 如需詳細資訊，請參閱[使用指南](ui/user-guide.md)。 |
| 淘汰舊端點 | 舊API端點(`data/privacy/gdpr`)已過時。 |

## 2020 年 1 月 14 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| [!DNL Privacy Service] 品牌再造 | 由於服務已發展為支援除GDPR外的其他管理法規，原名為「GDPR服務」的品牌已重新命名為[!DNL Privacy Service]。 |
| 新的API端點 | [!DNL Privacy Service] API的基本路徑已從`/data/privacy/gdpr`更新為`/data/core/privacy/jobs` |
| 新的必需`regulation`屬性 | 在[!DNL Privacy Service] API中建立新作業時，請求裝載中必須提供`regulation`屬性，以指出要追蹤作業的規則。 接受的值為`gdpr`和`ccpa`。 如需詳細資訊，請參閱[!DNL Privacy Service]開發人員指南中有關[隱私權工作](api/privacy-jobs.md)的檔案。 |
| 支援Adobe Primetime驗證 | [!DNL Privacy Service] 現在可接受來自Adobe Primetime驗證的存取／刪除請求，並 `primetimeAuthentication` 將其作為產品值。如需詳細資訊，請參閱[黃金時段驗證檔案](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)。 |

### 增強功能

* [!DNL Privacy Service] UI增強功能：
   * 針對GDPR和CCPA法規分開工作追蹤頁面。
   * 新的&#x200B;*規則類型*&#x200B;下拉式清單，可切換GDPR和CCPA的追蹤資料。

## 2019 年 7 月 25 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| 請求量度控制面板 | [!DNL Privacy Service] UI中的新量度控制面板可洞察已提交、已錯誤和已完成的GDPR請求。 |
| 請求產生器 | 為了同時為技術和非技術使用者提交GDPR要求的組織提供服務，UI中已新增「建立要求」功能。 對於想要繼續使用JSON檔案的組織，[!DNL Privacy Service] UI中仍提供JSON檔案提交功能。 |
| GDPR工作事件通知 | 有關GDPR工作狀態的事件通知是許多工作流程的重要元素。 雖然之前會使用個別電子郵件通知來傳送通知，但GDPR事件通知是運用Adobe I/O事件的訊息，這些事件會傳送至已設定的網頁掛接，以協助工作要求自動化。 [!DNL Privacy Service] UI使用者可訂閱Adobe I/OGDPR事件，以在產品或GDPR工作完成時收到更新。 |

## 2019 年 18 月 4 日

### 增強功能

* [!DNL Privacy Service] UI中狀態表的預設範圍已修改為7天範圍。
* 更好的內部異常處理。
* 針對低資料變更率的常見內部呼叫引入快取，以改善效能。

### 錯誤修正

* 已新增[!DNL Privacy Service] API中`GET /`端點的篩選查詢遺失記錄資訊。

## 2019 年 4 月 11 日

### 增強功能

* 更新的UI可支援測試版客戶的新功能
* 支援測試版UI 2.0功能的新量度API

## 2019 年 4 月 9 日

### 增強功能

* 將所有查閱(GET)API呼叫更新為預設的30天回顧範圍
* 限制API使用，使其最大回顧範圍為45天

## 2019 年 2 月 14 日

### 增強功能

* 在每個POST提交中強制執行`include`欄位。
* 上傳JSON時強制執行`include`欄位。

### 錯誤修正

* 修正客戶無法載入[!DNL Privacy Service] UI的問題。
