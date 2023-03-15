---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service發行說明
description: Adobe Experience Platform Privacy Service的最新發行說明。
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 5%

---

# [!DNL Privacy Service] 發行說明

本檔案包含Adobe Experience Platform新功能的相關資訊 [!DNL Privacy Service]，以及增強功能和重大錯誤修正。

>[!NOTE]
>
>其他 [!DNL Experience Platform] 可找到服務 [此處](../release-notes/latest/latest.md).

## 2020 年 9 月 9 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| 支援LGPD（巴西） | 如今，巴西可以創造隱私工作 [!DNL Lei Geral de Proteção de Dados] (LGPD)規則。 這些工作會在法規程式碼下追蹤 `lgpd_bra`. |

## 2020年4月8日

### 新功能

| 功能 | 說明 |
| --- | --- |
| PDPA支援 | [!DNL Privacy] 現在可根據泰國的個人資料保護法(PDPA)建立及追蹤請求。 在API中提出隱私權要求時， `regulation` array接受「pdpa_tha」值。 |
| UI中的命名空間類型 | 您現在可以在「請求產生器」中指定不同的命名空間類型，位於 [!DNL Privacy Service] UI。 請參閱 [使用手冊](ui/user-guide.md) 以取得更多資訊。 |
| 淘汰舊端點 | 舊的API端點(`data/privacy/gdpr`)已過時。 |

## 2020年1月14日

### 新功能

| 功能 | 說明 |
| --- | --- |
| [!DNL Privacy Service] 品牌重塑 | 先前名為「GDPR服務」的品牌已重新命名為 [!DNL Privacy Service] 隨著服務逐漸發展，除了GDPR以外，還可支援其他法規。 |
| 新API端點 | 的基本路徑 [!DNL Privacy Service] API已從 `/data/privacy/gdpr` to `/data/core/privacy/jobs` |
| 新增必要項目 `regulation` 屬性 | 在 [!DNL Privacy Service] API, a `regulation` 必須在要求裝載中提供屬性，以指出要追蹤工作的法規。 接受的值為 `gdpr` 和 `ccpa`. 請參閱 [隱私權工作](api/privacy-jobs.md) 在 [!DNL Privacy Service] API指南，以了解詳細資訊。 |
| 支援Adobe Primetime驗證 | [!DNL Privacy Service] 現在接受來自Adobe Primetime驗證的存取/刪除請求，使用 `primetimeAuthentication` 作為其產品價值。 請參閱 [Primetime驗證檔案](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) 以取得更多資訊。 |

### 增強功能

* [!DNL Privacy Service] UI增強功能：
   * 區隔GDPR和CCPA法規的工作追蹤頁面。
   * 新增 *規範類型* 下拉式清單，在GDPR和CCPA的追蹤資料之間切換。

## 2019年7月25日

### 新功能

| 功能 | 說明 |
| --- | --- |
| 請求量度控制面板 | 中的新量度控制面板 [!DNL Privacy Service] UI可顯示已提交、已錯誤及已完成的GDPR請求。 |
| 請求產生器 | 為了為同時提交GDPR請求的技術使用者和非技術使用者服務組織，UI已新增「建立請求」功能。 JSON檔案提交功能仍可在 [!DNL Privacy Service] 供偏好繼續使用的組織的UI。 |
| GDPR工作事件通知 | GDPR工作狀態的事件通知是許多工作流程的關鍵元素。 雖然之前會使用個別電子郵件通知提供通知，但GDPR事件通知是運用Adobe I/O事件的訊息，這些事件會傳送至已設定的Webhook，以利工作要求自動化。 [!DNL Privacy Service] UI使用者可訂閱Adobe I/OGDPR事件，以在產品或GDPR工作完成時收到更新。 |

## 2019年4月18日

### 增強功能

* 狀態表的預設範圍，在 [!DNL Privacy Service] UI已修改為7天範圍。
* 更好的內部例外處理。
* 針對資料變更率低的常見內部呼叫引入快取，以改善效能。

### 錯誤修正

* 已新增 `GET /` 端點 [!DNL Privacy Service] API。

## 2019 年 4 月 11 日

### 增強功能

* 更新UI以支援測試版客戶的新功能
* 支援測試版UI 2.0功能的新量度API

## 2019 年 4 月 9 日

### 增強功能

* 將所有查詢(GET)API呼叫更新為30天回顧範圍
* 限制API使用，使回顧範圍上限為45天

## 2019 年 2 月 14 日

### 增強功能

* 執行 `include` 欄位。
* 執行 `include` 欄位。

### 錯誤修正

* 修正客戶無法載入 [!DNL Privacy Service] UI。
