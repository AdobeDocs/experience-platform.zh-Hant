---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service 發行說明
description: Adobe Experience Platform Privacy Service 的最新發行說明。
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# [!DNL Privacy Service] 發行說明

本文件包含有關 Adob&#x200B;&#x200B;e Experience Platform [!DNL Privacy Service] 新功能、增強功能和重大錯誤修正的資訊。

>[!NOTE]
>
>其他 [!DNL Experience Platform] 服務的最新發行說明可以瀏覽[此處](../release-notes/latest/latest.md)。

## 2020 年 9 月 9 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| 支援 LGPD (巴西) | 隱私權作業現在可根據巴西的 [!DNL Lei Geral de Proteção de Dados] (LGPD) 法規來建立。這些作業會受到監管法規 `lgpd_bra` 的追蹤。 |

## 2020 年 4 月 8 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| PDPA 支援 | [!DNL Privacy] 請求現在可以根據泰國的個人資料保護法 (PDPA) 來建立和追蹤。在 API 中提出隱私權請求時，`regulation` 陣列會接受「pdpa_tha」值。 |
| UI 中的命名空間類型 | 您現在可於 [!DNL Privacy Service] UI 的請求產生器中指定不同的命名空間類型。若需要更多資訊，請參閱[使用手冊](ui/user-guide.md)。 |
| 舊端點不再使用不用 | 舊 API 端點 (`data/privacy/gdpr`) 已不再使用。 |

## 2020 年 1 月 14 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| [!DNL Privacy Service] 服務更名 | 隨著服務不斷發展以支援 GDPR 以外的其他法規，原先名為「GDPR Service」現已更名為 [!DNL Privacy Service]。 |
| 新的 API 端點 |  [!DNL Privacy Service] API 的基本路徑已從 `/data/privacy/gdpr` 更新為 `/data/core/privacy/jobs` |
| 新規定要提供 `regulation` 屬性 | 在 [!DNL Privacy Service] API 中建立新作業時，必須在請求承載中提供 `regulation` 屬性，以便指明是根據哪個規則追蹤該作業。接受的值為 `gdpr` 和 `ccpa`。請參閱 [!DNL Privacy Service] API 指南中有關[隱私權作業](api/privacy-jobs.md)的文件，了解更多資訊。 |
| Adob&#x200B;&#x200B;e Primetime 驗證支援 | [!DNL Privacy Service] 現在接受來自 Adob&#x200B;&#x200B;e Primetime 驗證的存取/刪除請求，並使用 `primetimeAuthentication` 為其產品值。請參閱 [Primetime 驗證文件](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)，了解更多資訊。 |

### 增強功能

* [!DNL Privacy Service] UI 增強功能：
   * GDPR 和 CCPA 法規的個別作業追蹤頁面。
   * 新的&#x200B;*監管類型*&#x200B;下拉式選單可在 GDPR 和 CCPA 追蹤資料之間切換。

## 2019 年 7 月 25 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| 請求量度儀表板 |  [!DNL Privacy Service] UI 的新量度儀表板可讓您看到已提交、有錯誤和已完成的 GDPR 請求。 |
| 請求產生器 | 為了服務組織中有提交 GDPR 請求的技術和非技術使用者，我們在 UI 中新增「建立請求」功能。[!DNL Privacy Service] UI 中仍提供 JSON 檔案提交功能，以便有些組織能繼續使用。 |
| GDPR 作業通知 | 有關 GDPR 作業狀態的事件通知是許多工作流程的關鍵要素。以前的通知是使用個別電子郵件通知來提供，而 GDPR 事件通知是指利用 Adob&#x200B;&#x200B;e I/O 事件的訊息，這些訊息會發送至設定的 Webhook，有利作業請求自動化。[!DNL Privacy Service] UI 使用者可以訂閱 Adob&#x200B;&#x200B;e I/O GDPR 事件，以便在產品或 GDPR 作業完成時接收更新通知。 |

## 2019 年 4 月 18 日

### 增強功能

*  [!DNL Privacy Service] UI 中狀態表的預設範圍已修改為 7 天期。
* 內部異常處理更順利。
* 透過為具有低資料變更率的常見內部呼叫引入快取來提高效能。

### 錯誤修正

* 針對 `GET /` API 中對 [!DNL Privacy Service] 端點的已篩選查詢，已新增遺失的記錄資訊。

## 2019 年 4 月 11 日

### 增強功能

* 已更新 UI 以支援 Beta 版客戶使用新功能
* 新量度 API 可支援 Beta 版 UI 2.0 功能

## 2019 年 4 月 9 日

### 增強功能

* 將所有查詢 (GET) API 呼叫更新為預設 30 天回溯範圍
* 限制 API 的使用，使其最大回溯範圍為 45 天

## 2019 年 2 月 14 日

### 增強功能

* 在每次 POST 提交中強制執行 `include` 欄位。
* 上傳 JSON 時強制執行 `include` 欄位。

### 錯誤修正

* 已修正客戶無法載入 [!DNL Privacy Service] UI 的問題。
