---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service發行說明
description: Adobe Experience Platform Privacy Service最新發行說明。
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 5%

---

# [!DNL Privacy Service] 發行說明

本檔案包含Adobe Experience Platform [!DNL Privacy Service]新功能的相關資訊，以及增強功能和重大錯誤修正。

>[!NOTE]
>
>其他[!DNL Experience Platform]服務的最新發行說明可在[這裡](../release-notes/latest/latest.md)找到。

## 2020 年 9 月 9 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| 支援LGPD （巴西） | 隱私權工作現在可以根據巴西的[!DNL Lei Geral de Proteção de Dados] (LGPD)法規建立。 這些工作是根據法規代碼`lgpd_bra`進行追蹤。 |

## 2020年4月8日

### 新功能

| 功能 | 說明 |
| --- | --- |
| PDPA支援 | 在泰國，現在可以根據個人資料保護法(PDPA)建立及追蹤[!DNL Privacy]個要求。 在API中提出隱私權要求時，`regulation`陣列會接受值「pdpa_tha」。 |
| UI中的名稱空間型別 | 您現在可以在[!DNL Privacy Service] UI的「請求產生器」中指定不同的名稱空間型別。 如需詳細資訊，請參閱[使用手冊](ui/user-guide.md)。 |
| 棄用舊端點 | 已棄用舊的API端點(`data/privacy/gdpr`)。 |

## 2020年1月14日

### 新功能

| 功能 | 說明 |
| --- | --- |
| [!DNL Privacy Service]品牌重塑 | 先前名為「GDPR服務」的服務已更名為[!DNL Privacy Service]，因為服務已成長為支援GDPR以外的其他法規。 |
| 新API端點 | [!DNL Privacy Service] API的基礎路徑已從`/data/privacy/gdpr`更新為`/data/core/privacy/jobs` |
| 新的必要`regulation`屬性 | 在[!DNL Privacy Service] API中建立新工作時，必須在要求裝載中提供`regulation`屬性，以指出要追蹤其下的工作的法規。 接受的值為`gdpr`和`ccpa`。 如需詳細資訊，請參閱[!DNL Privacy Service] API指南中有關[隱私權工作](api/privacy-jobs.md)的檔案。 |
| 支援Adobe Primetime驗證 | [!DNL Privacy Service]現在接受來自Adobe Primetime驗證的存取/刪除要求，使用`primetimeAuthentication`作為其產品值。 如需詳細資訊，請參閱[Primetime驗證檔案](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)。 |

### 增強功能

* [!DNL Privacy Service]個UI增強功能：
   * GDPR和CCPA法規的個別工作追蹤頁面。
   * 新&#x200B;*法規型別*&#x200B;下拉式清單，可切換GDPR和CCPA的追蹤資料。

## 2019年725日

### 新功能

| 功能 | 說明 |
| --- | --- |
| 請求量度控制面板 | [!DNL Privacy Service] UI中的新量度儀表板可讓您檢視已提交、有錯誤和已完成的GDPR請求。 |
| 請求產生器 | 若要透過提交GDPR請求的技術和非技術使用者為組織提供服務，UI已新增「建立請求」功能。 對於想要繼續使用JSON檔案提交功能的組織，[!DNL Privacy Service] UI中仍會提供該功能。 |
| GDPR工作事件通知 | 有關GDPR工作狀態的事件通知是許多工作流程的關鍵元素。 雖然通知先前是使用個別電子郵件通知來提供，但GDPR事件通知是運用Adobe I/O事件的訊息，這些通知會傳送至已設定的webhook，以促進工作請求自動化。 [!DNL Privacy Service]個UI使用者可以訂閱Adobe I/OGDPR事件，以便在產品或GDPR工作完成時接收更新。 |

## 2019年4月18日

### 增強功能

* [!DNL Privacy Service] UI中狀態表格的預設範圍已修改為7天跨度。
* 改善內部例外狀況處理。
* 針對低資料變更率的常見內部呼叫引入快取，以提升效能。

### 錯誤修正

* 已在[!DNL Privacy Service] API中新增`GET /`端點之篩選查詢的遺漏記錄資訊。

## 2019年4月11日

### 增強功能

* 更新UI以支援Beta版客戶的新功能
* 新量度API可在Beta版中支援UI 2.0功能

## 2019 年 4 月 9 日

### 增強功能

* 將所有查詢(GET) API呼叫更新為預設的30天回顧範圍
* 限制使用API的回顧範圍上限為45天

## 2019年2月14日

### 增強功能

* 在每個POST提交中強制執行`include`欄位。
* 上傳JSON時強制執行`include`欄位。

### 錯誤修正

* 修正客戶無法載入[!DNL Privacy Service] UI的問題。
