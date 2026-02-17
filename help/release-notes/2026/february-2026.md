---
title: Adobe Experience Platform 發行說明 (2026 年 2 月)
description: Adobe Experience Platform 2026 年 2 月版發行說明。
source-git-commit: afb1e0266b4c5485ba574f95aab3a56485d176b3
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 46%

---

# Adobe Experience Platform 發行說明

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/latest)
>- [聯合客群構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期： 2026年2月17日**

Adobe Experience Platform 的新功能及現有功能更新：

- [警報](#alerts)
- [目的地](#destinations)
- [來源](#sources)

## 警報 {#alerts}

Experience Platform 可讓您訂閱各種 Experience Platform 活動的事件型警報。您可以透過Experience Platform使用者介面中的[!UICONTROL Alerts]標籤訂閱不同的警示規則，也可以選擇在UI本身或透過電子郵件通知接收警示訊息。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Slack]客戶相關警示的整合 | 您現在可以傳送客戶通知給[!DNL Slack]。 依照[逐步教學課程](../../observability/alerts/slack-integration.md)來設定[!DNL Slack]整合，並直接在您的[!DNL Slack]工作區中接收警示通知。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀 [[!DNL Observability Insights]  概觀](../../observability/home.md)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Experience Platform 的資料。您可以使用目標來啟用已知和未知的資料，以供跨通道行銷活動、電子郵件行銷活動、定向廣告及其他許多使用案例使用。

**全新或已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [[!DNL Snowflake] 批次](../../destinations/catalog/warehouses/snowflake-batch.md)一般可用 | [!DNL Snowflake]批次目的地現在已可供一般使用。 全球的Real-Time CDP客戶現在可以使用此聯結器，在其Snowflake帳戶中啟用資料，而不需要實際複製資料。 有限版本的所有限制均已解除（僅限美國客戶使用，僅支援屬於預設合併原則的對象）。 |

{style="table-layout:auto"}

**修正和改良**

| 修正 | 說明 |
| --- | --- |
| 超過啟用失敗率的警報 | 「啟動失敗率超過目的地」警報現在會正確使用您在評估及傳送警報時設定的臨界值。 以前，無論您設定的百分比為何，警報都會以1%的失敗率觸發。 如需此警示的詳細資訊，請參閱[標準警示規則](../../observability/alerts/rules.md#destinations)。 |
| Google Customer Match排除的身分報告 | 修正略過記錄計數邏輯的錯誤，此錯誤會導致Google Customer Match目的地顯示膨脹的排除設定檔計數。 啟用和匯出行為不受影響；只有報告的數字不正確。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**新的或更新來源**

| 來源 | 說明 |
| --- | --- |
| [!DNL Databricks]來源聯結器中的Unity Catalog支援 | [!DNL Databricks]來源聯結器現在支援Unity目錄。 閱讀更新的[[!DNL Databricks]](../../sources/connectors/databases/databricks.md)檔案，瞭解如何在設定來源連線時使用Unity Catalog。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
