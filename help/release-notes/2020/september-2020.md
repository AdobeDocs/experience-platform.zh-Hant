---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年9月9日
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 23c7a0d82cb849568d6411c1a09c7a16b86d4954
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 5%

---


# Adobe Experience Platform 發行說明

**發行日期: 2020 年 9 月 9 日**

Adobe Experience Platform現有功能的更新：

* [[!DNL資料治理]](#governance)
* [[!DNL目標]](#destinations)
* [[!DNL隱私服務]](#privacy)
* [[!DNL源]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform資料治理是一系列策略和技術，用於管理客戶資料並確保符合適用於資料使用的法規、限制和政策。 它在各個層級中都扮演了關 [!DNL Experience Platform] 鍵角色，包括編目、資料傳承、資料使用標籤、資料存取政策，以及對行銷動作資料的存取控制。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 資料集標籤UI增強功能 | 為了讓處理大型結構描述更輕鬆，在資料集標籤UI時新增了數種排序和篩選控制項： <ul><li>根據完整方案路徑，依字母順序排序欄位。</li><li>對欄位路徑名執行部分搜索。</li><li>篩選沒有標籤的欄位、選取的標籤或標籤類別。</li></ul> |

如需服務 [的詳細資訊](../../data-governance/home.md) ，請參閱資料管理概觀。

## 目的地 {#destinations}

在 [Adobe即時客戶資料平台中](../../rtcdp/overview.md)，目標是與目標平台預先建立的整合，以順暢的方式將資料啟動給這些合作夥伴。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| UX改進 | 使用者可存取內嵌表格動作，以更輕鬆地存取主要動作，例如新增資料、編輯排程和新增區段。 如需詳細 [資訊，請參閱目標工作區](../../rtcdp/destinations/destinations-workspace.md) 檔案。 |

若要進一步瞭解，請造訪目 [標總覽](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Privacy Service] {#privacy}

數項法律和組織法規授予使用者在要求時從資料存放區存取或刪除其個人資料的權利。 Adobe Experience Platform提 [!DNL Privacy Service] 供REST風格的API和使用者介面，可協助您管理客戶的這些資料要求。 您可 [!DNL Privacy Service]以提交要求，以便從Adobe Experience Cloud應用程式存取和刪除私人或個人客戶資料，以利自動符合法律和組織的隱私權法規。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 支援LGPD（巴西） | 現在，可以根據巴西的(LGPD)法規創 [!DNL Lei Geral de Proteção de Dados] 造隱私崗位。 這些工作是根據法規代碼進行跟蹤的 `lgpd_bra`。 |

如需服務 [的詳細資訊](../../privacy-service/home.md) ，請參閱隱私權服務概觀。

## 來源 {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時讓您使用服務來建構、標示和增強該資 [!DNL Platform] 料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 自動對應 | [!DNL Platform] 根據使用者選擇的目標架構或資料集，提供在資料擷取工作流程期間自動對應的智慧建議。 您可以手動調整有彈性的自動對應規則，以符合您的使用案例。 |
| UX改進 | 使用者可存取內嵌表格動作，以更輕鬆地存取主要動作，例如新增資料、編輯排程和新增區段。 有關詳細信 [息，請參見](../../sources/tutorials/ui/monitor.md) 「監視資料流」文檔。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。
