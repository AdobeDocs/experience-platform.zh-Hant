---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 隱私權服務發行說明
topic: release notes
translation-type: tm+mt
source-git-commit: 4cfa64e3371496e2408fe8fee64d49883334917c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 5%

---


# [!DNL Privacy Service] 發行說明

本檔案包含Adobe Experience Platform新功能的相關資訊， [!DNL Privacy Service]以及增強功能和重大錯誤修正。

>[!NOTE]
>
>如需其他服務的最 [!DNL Experience Platform] 新發行說明，請 [參閱](../release-notes/latest/latest.md)。

## 2020 年 4 月 8 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| PDPA支援 | [!DNL Privacy] 現在，您可以根據泰國的個人資料保護法(PDPA)來建立和追蹤要求。 在API中提出隱私權要求時， `regulation` 陣列接受&quot;pdpa_tha&quot;值。 |
| UI中的名稱空間類型 | 您現在可以在UI的「請求產生器」中指定不同的命名空 [!DNL Privacy Service] 間類型。 如需詳細 [資訊，請參閱](ui/user-guide.md) 「使用指南」。 |
| 淘汰舊端點 | 舊API端點(`data/privacy/gdpr`)已過時。 |

## 2020 年 1 月 14 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| [!DNL Privacy Service] 品牌再造 | 由於該服務已發展為支援除GDPR外的其他管 [!DNL Privacy Service] 理法規，原名「GDPR服務」已重新命名。 |
| 新的API端點 | API的基本路 [!DNL Privacy Service] 徑已從更新 `/data/privacy/gdpr` 為 `/data/core/privacy/jobs` |
| 新的必要 `regulation` 屬性 | 在 [!DNL Privacy Service] API中建立新工作時，請求裝載中必 `regulation` 須提供屬性，以指出要追蹤工作的規則。 接受的值是 `gdpr` 和 `ccpa`。 如需詳細資訊，請 [參閱開發人員指南](api/privacy-jobs.md)[!DNL Privacy Service] 中有關隱私權工作的檔案。 |
| 支援Adobe Primetime驗證 | [!DNL Privacy Service] 現在可接受Adobe Primetime驗證的存取／刪除要求， `primetimeAuthentication` 並視其產品價值而定。 See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### 增強功能

* [!DNL Privacy Service] UI增強功能：
   * 針對GDPR和CCPA法規分開工作追蹤頁面。
   * 新的 _規則類型下拉式清單_ ，可在GDPR和CCPA的追蹤資料之間切換。

## 2019 年 7 月 25 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| 請求量度控制面板 | UI中的新量度控制面板 [!DNL Privacy Service] 可讓您洞悉已提交、已錯誤及已完成的GDPR要求。 |
| 請求產生器 | 為了同時為技術和非技術使用者提交GDPR要求的組織提供服務，UI中已新增「建立要求」功能。 UI中仍提供JSON檔案提交功能，供偏好 [!DNL Privacy Service] 繼續使用的組織使用。 |
| GDPR工作事件通知 | 有關GDPR工作狀態的事件通知是許多工作流程的重要元素。 雖然之前會使用個別電子郵件通知來傳送通知，但GDPR事件通知是運用Adobe I/O事件的訊息，這些事件會傳送至已設定的網頁掛接，以協助工作要求自動化。 [!DNL Privacy Service] UI使用者可訂閱Adobe I/O GDPR事件，以在產品或GDPR工作完成時收到更新。 |

## 2019 年 4 月 18 日

### 增強功能

* UI中狀態表的預設范 [!DNL Privacy Service] 圍已修改為7天範圍。
* 更好的內部異常處理。
* 針對低資料變更率的常見內部呼叫引入快取，以改善效能。

### 錯誤修正

* 已新增API中已篩選查詢端點 `GET /` 的遺失記錄 [!DNL Privacy Service] 資訊。

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

* 在每次POST `include` 提交中強制執行欄位。
* 上傳JSON `include` 時強制執行欄位。

### 錯誤修正

* 修正客戶無法載入UI的 [!DNL Privacy Service] 問題。