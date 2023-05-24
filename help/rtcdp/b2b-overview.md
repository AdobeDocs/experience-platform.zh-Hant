---
keywords: RTCDP;CDP;B2B版；Real-time Customer Data Platform；即時客戶資料平台；即時cdp;b2b;cdp；客戶AI
title: Real-Time CDPB2B版概述
description: Real-Time Customer Data Platform B2B Edition 帳戶總覽
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 1%

---

# Real-time Customer Data PlatformB2B版概述

Real-Time CDPB2B版本以Adobe Real-time Customer Data Platform(Real-Time CDP)為基礎，專門為以企業對企業服務模式運營的營銷人員而設計。 它將來自多個來源的資料匯集在一起，並將其合併到人員和帳戶配置檔案的單個視圖中。 此統一資料使營銷人員能夠精確地瞄準特定受眾，並跨所有可用渠道接觸這些受眾。

Real-Time CDPB2B版與其B2C版的Adobe Experience Platform能力有所提高。 這些改進包括對B2B使用案例的體驗資料模型(XDM)的改進、對身份解析和配置檔案分段的升級，以及定製的連接器和目標 [!DNL Marketo Engage]。 的 [!DNL Marketo] 連接器允許B2B品牌將其業界領先的B2B接觸資料與行為資訊相連，以培育銷售線索並增強基於客戶的營銷操作。

使用Real-Time CDPB2B版，您可以：

* 將從多個來源收集的資料合併到單個視圖中，以建立整體的人員和帳戶配置檔案。
* 從統一帳戶配置檔案的集中儲存中豐富、分段和導出所有跨源資料。
* 使用集中化流程的每個步驟都提供的資料治理工具管理資料，以確保資料符合法律法規和業務策略。

有關Real-Time CDPB2B版本改進的更全面詳情，分為以下各節。

## XDM

Real-Time CDPB2B版提供了幾種新的XDM架構類、欄位組和關係類型，以捕獲和構造資料，並專門用於B2B目的。 請參閱 [Real-Time CDPB2B版XDM](./schemas/b2b.md) 以細分這些增強功能。

通過使用預配置的B2B架構，您可以以標準化、可操作的結構導入資料。 許多新架構類幾乎直接映射到主流CRM中遇到的類。 [!DNL Salesforce]。 [!DNL Microsoft Dynamics]。 [!DNL Marketo]以及其他B2B資料源。 使用Real-Time CDPB2B版，您可以以直觀的方式將來自B2B源的資料帶入平台，並獲得易於審核的結果。

這些XDM增強功能使您能夠通過以B2B為中心的源和目標來更好地接收和激活資料，從而改進了資料的統一和呈現，以實現更多種、更靈活的使用情形。

## 身份解析

在定義了模式並接收了符合這些模式的資料之後，Real-Time CDPB2B版通過一個功能強大的即時身份解析系統識別代表真實世界人物和企業的源記錄。

身份解析系統提供以下功能：

* B2B和B2C人員記錄組合
* 多級帳戶層次結構
* 多對多、人員對客戶連接
* 即時解決人員和帳戶身份

身份解決系統已經擴大，以支援更多層面的人員分類。 該系統允許人們被確定為商業機會中的領導者以及客戶。

由源CRM同步並通過系統內的多個路徑連接的帳戶記錄由平台合併在一起。 該系統將那些與商業機會相關的人和那些記錄為客戶的人匯集在一起，但如果他們可以識別的話，還能將他們之間的區別保留為屬性。

匹配標識符用於連結在一起並合併來自多個系統的帳戶記錄。 帳戶層次結構將在整個流程中保留。 使用獨特優勢來仔細檢查人員是否與帳戶關聯，並在需要時提供將他們與帳戶分離的能力。

## 概況和分段

一旦Real-Time CDPB2B版吸收了與人、公司、屬性和行為相關的資料和已解析的身份，該資料將用於構建配置檔案。 然後，可以將這些簡檔分割成可瀏覽的受眾，這些受眾隨後可被激活到各種目的地。

當正確實施時，系統使用唯一的主標識符來跟蹤人員，而不是使用可更改的屬性（如電子郵件地址）。 這意味著當有人更換工作時，系統仍會跟蹤他們。 該人仍是同一個實體，但他們與一個新帳戶相關聯。 此本機功能提供了擴展到新帳戶的強大向量，因為系統將這些人作為個體，包括他們的所有屬性和行為。

## B2B源

平台允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 的 [!DNL Marketo] 源允許您將B2B資料流式傳輸到平台中，並使用與平台連接的應用程式保持此資料的最新。 它支援任意數量的 [!DNL Marketo] （這對具有多個實例的大型公司有利），並將資料合併到單個組織中。

>[!NOTE]
>
>的 [!DNL Marketo] 源 **不** 必須使用Real-Time CDPB2B版。

查看 [Real-Time CDPB2B版](./sources/b2b.md) 文檔，瞭解有關Marketo和將B2B資料引入平台的更多資訊。

## B2B目標

Experience Platform目的地，如Google客戶匹配，Facebook,LinkedIn,Marketo Engage,AmazonS3,Google顯示和視頻360,Google廣告和Google廣告經理等，均由Real-Time CDPB2B版提供並完全支援。 Marketo Engage目的地還將段成員身份資料從平台中流出，並將其作為Marketo的清單提供。

請參閱 [Marketo Engage目標](../destinations/catalog/adobe/marketo-engage.md) 的子菜單。

對於具有多個CRM的公司，Real-Time CDPB2B版提供了將目標連接器配置為Marketo或CRM獨立實例的選項。 如果需要，您可以配置每個實例的目標連接器，並獨立地將受眾發送到每個CRM實例。

## 後續步驟

現在，您更好地瞭解了Real-Time CDPB2B版為營銷人員帶來的好處，以及它與Real-Time CDP的不同之處，您就可以瞭解如何將這些功能應用到您自己的組織。

要瞭解Real-Time CDPB2B版如何使您的企業對企業服務模式受益，請參閱以下文檔以幫助您入門：

* [Real-Time CDPB2B版的一個示例用例](./b2b-use-case.md)
* [Real-time Customer Data PlatformB2B版的端到端教程](./b2b-tutorial.md)
* [如何攝取資料](./sources/b2b.md)
* [如何訪問配置檔案](./profile/profile-overview.md)
* [Real-time Customer Data PlatformB2B版中的架構](./schemas/b2b.md)
* [如何構建段](./segmentation/b2b.md)
* [如何將段激活到目標](./destinations/b2b.md)
* [如何定義和實施資料治理策略](./privacy/data-governance-overview.md)
