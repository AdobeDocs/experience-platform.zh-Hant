---
title: Adobe Experience 平台發行說明
description: Adobe Experience Platform的最新發行說明。
source-git-commit: 3a81a6f41b1e6acfe0e79dd56f01cf1bcd99417c
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 2 月 23 日**

Adobe Experience Platform 現有功能更新：

- [資料收集](#data-collection)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Identity Service]](#identity)
- [來源](#sources)

## 資料收集 {#data-collection}

平台提供一套技術，使您能夠收集客戶端客戶體驗資料並將其發送到Adobe Experience Platform邊緣網路，在該網路中，資料可以得到豐富、轉換並分發到Adobe或非Adobe目的地。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 用於資料流配置的改進的UI工作流 | 已在資料收集UI中建立新資料流的工作流已更新。 將服務添加到資料流時，選項清單中將只包含您有權訪問的服務。 請參閱上的指南 [配置資料流](../../edge/fundamentals/datastreams.md) 的子菜單。 |
| 資料收集的資料準備 | 如果您使用Adobe Experience PlatformWeb SDK，現在可以利用資料準備功能將資料映射到伺服器端的體驗資料模型(XDM)。 請參閱 [資料收集的資料準備](../../edge/fundamentals/datastreams.md#data-prep) 的子菜單。 |
| 第一方設備ID | 使用平台Web SDK收集客戶資料時，您現在可以將自己的設備ID發送到Adobe Experience Platform邊緣網路，這為最近對第三方Cookie生命週期的瀏覽器限制提供了一種解決方法。 請參閱上的指南 [第一方設備ID](../../edge/identity/first-party-device-ids.md) 的子菜單。 |

有關平台中資料收集的詳細資訊，請參閱 [資料收集概述](../../collection/home.md)。

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

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 新權限 `view-identity-graph` | 您現在可以使用 `view-identity-graph` 控制組織中的用戶是否能夠查看身份圖資料的權限。 未具有此權限的用戶將被禁止訪問UI中的標識圖查看器，或在訪問 [!DNL Identity Service] 返回標識的API。 查看 [訪問控制概述](../../access-control/home.md) 的子菜單。 |

有關 [!DNL Identity Service]，請參閱 [Identity Service概述](../../identity-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| Beta源移至GA | 已將以下源從beta升級為GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
