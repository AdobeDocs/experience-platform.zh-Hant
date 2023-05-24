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

本文檔包含有關Adobe Experience Platform新功能的資訊 [!DNL Privacy Service]以及增強功能和重要的錯誤修復。

>[!NOTE]
>
>其他產品的最新發行說明 [!DNL Experience Platform] 可找到服務 [這裡](../release-notes/latest/latest.md)。

## 2020 年 9 月 9 日

### 新功能

| 功能 | 說明 |
| --- | --- |
| 支援LGPD（巴西） | 如今，在巴西的隱私政策下，可以創造隱私工作 [!DNL Lei Geral de Proteção de Dados] (LGPD)條例。 這些作業在法規代碼下被跟蹤 `lgpd_bra`。 |

## 2020年4月8日

### 新功能

| 功能 | 說明 |
| --- | --- |
| PDPA支援 | [!DNL Privacy] 現在，可以根據泰國的個人資料保護法(PDPA)建立和跟蹤請求。 在API中發出隱私請求時， `regulation` array接受值「pdpa_tha」。 |
| UI中的命名空間類型 | 現在，您可以在中的請求生成器中指定不同的命名空間類型 [!DNL Privacy Service] UI。 查看 [使用手冊](ui/user-guide.md) 的子菜單。 |
| 舊終結點棄用 | 舊API終結點(`data/privacy/gdpr`)已棄用。 |

## 2020年1月14日

### 新功能

| 功能 | 說明 |
| --- | --- |
| [!DNL Privacy Service] 重新標籤 | 以前名為「 GDPR服務」已重新標籤為 [!DNL Privacy Service] 隨著服務的發展，除了GDPR外，還支援其他法規。 |
| 新API終結點 | 的基本路徑 [!DNL Privacy Service] API已從 `/data/privacy/gdpr` 至 `/data/core/privacy/jobs` |
| 需要新建 `regulation` 屬性 | 在中建立新作業時 [!DNL Privacy Service] API, a `regulation` 必須在請求負載中提供屬性，以指示跟蹤作業的法規。 接受的值為 `gdpr` 和 `ccpa`。 查看上的文檔 [隱私作業](api/privacy-jobs.md) 的 [!DNL Privacy Service] API指南，瞭解詳細資訊。 |
| 支援Adobe Primetime身份驗證 | [!DNL Privacy Service] 現在接受來自Adobe Primetime身份驗證的訪問/刪除請求，使用 `primetimeAuthentication` 作為產品價值。 查看 [黃金時段驗證文檔](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) 的子菜單。 |

### 增強功能

* [!DNL Privacy Service] UI增強：
   * 為GDPR和CCPA管理法規分開作業跟蹤頁。
   * 新建 *規則類型* 下拉菜單，在GDPR和CCPA的跟蹤資料之間切換。

## 2019年7月25日

### 新功能

| 功能 | 說明 |
| --- | --- |
| 請求度量儀表板 | 中的新度量儀表板 [!DNL Privacy Service] UI提供了對已提交、出錯和已完成的GDPR請求的可見性。 |
| 請求生成器 | 要為具有提交GDPR請求的技術和非技術用戶的組織提供服務，已將「建立請求」功能添加到UI中。 JSON檔案提交功能仍可在 [!DNL Privacy Service] 用於那些希望繼續使用它的組織的UI。 |
| GDPR作業事件通知 | 有關GDPR作業狀態的事件通知是許多工作流的關鍵元素。 以前使用單個電子郵件通知發送通知時， GDPR事件通知是利用Adobe I/O事件的消息，這些事件會發送到配置的webhook以促進作業請求自動化。 [!DNL Privacy Service] UI用戶可以訂閱Adobe I/OGDPR事件，以在產品或GDPR作業完成後接收更新。 |

## 2019年4月18日

### 增強功能

* 中狀態表的預設範圍 [!DNL Privacy Service] UI已修改為7天範圍。
* 更好的內部異常處理。
* 通過為具有低資料更改率的常見內部調用引入快取，提高了效能。

### 錯誤修正

* 已為的已篩選查詢添加缺少的日誌記錄資訊 `GET /` 端點 [!DNL Privacy Service] API。

## 2019 年 4 月 11 日

### 增強功能

* 已更新UI，以支援測試版客戶的新功能
* 支援測試版中UI 2.0功能的新指標API

## 2019 年 4 月 9 日

### 增強功能

* 已將所有查找(GET)API調用更新為預設的30天回望範圍
* 限制的API使用，其最大回望範圍為45天

## 2019 年 2 月 14 日

### 增強功能

* 強制 `include` 的子菜單。
* 強制 `include` 上載JSON時的欄位。

### 錯誤修正

* 修復客戶無法載入的問題 [!DNL Privacy Service] UI。
