---
title: Adobe Experience 平台發行說明
description: Adobe Experience Platform的最新發行說明。
source-git-commit: 762a4b7336f1c26b79883db9484d8f5fc7bff53c
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 8%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 2 月 23 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Identity Service]](#identity)
- [來源](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Data Prep] 支援Adobe Analytics源連接器 | Adobe Analytics源連接器現在支援資料準備功能，允許您在建立資料流時將分析報告套件資料映射到目標XDM架構。 請參閱上的教程 [建立分析源連接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 的子菜單。 |

有關 [!DNL Data Prep]，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## [!DNL Identity Service] {#identity}

提供相關數字型驗需要全面瞭解您的客戶。 當您的客戶資料分散在不同的系統中，導致每個客戶都顯示有多個「身份」時，這就變得更加困難了。

Adobe Experience Platform [!DNL Identity Service] 通過跨設備和系統橋接身份，幫助您更好地瞭解客戶及其行為，讓您能夠即時提供有影響的個人數字型驗。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 新權限 `view-identity-graph` | 您現在可以使用 `view-identity-graph` 控制組織中的用戶是否能夠查看身份圖資料的權限。 未具有此權限的用戶將被禁止訪問UI中的標識圖查看器，或在訪問 [!DNL Identity Service] 返回標識的API。 查看 [訪問控制概述](../../access-control/home.md) 的子菜單。 |

有關 [!DNL Identity Service]，請參閱 [Identity Service概述](../../identity-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

| 功能 | 說明 |
| --- | --- |
| Beta源移至GA | 已將以下源從beta升級為GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
