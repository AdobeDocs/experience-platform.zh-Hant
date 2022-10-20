---
keywords: RTCDP; CDP;B2B Edition;Real-time Customer Data Platform；即時客戶資料平台；即時cdp;b2b; CDP；客戶AI
title: Real-time CDP B2B Edition概述
description: Real-time Customer Data Platform B2B Edition 帳戶總覽
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---

# Real-time Customer Data Platform B2B版概述

Real-time CDP B2B Edition建置在Real-time Customer Data Platform(Real-time CDP)之上，專為以企業對企業服務模式運作的行銷人員而打造。 它匯集了來自多個來源的資料，並將其結合為人員和帳戶設定檔的單一檢視。 此統一的資料可讓行銷人員精確鎖定特定對象，並參與所有可用管道中的這些對象。

對各種Adobe Experience Platform功能進行了改進，將即時CDP B2B Edition與其B2C對應版本區分開來。 其中包括針對B2B使用案例改善Experience Data Model(XDM)、升級為身分解析和設定檔分段，以及自訂的連接器和目的地 [!DNL Marketo Engage]. 此 [!DNL Marketo] 連接器可讓B2B品牌將其領先業界的B2B參與資料與行為資訊連結，以培育銷售機會並增強以帳戶為基礎的行銷作業。

使用Real-time CDP B2B Edition，您可以：

* 將從多個來源收集的資料合併成單一檢視，以建立整體的人員和帳戶設定檔。
* 從統一帳戶設定檔的集中存放區，擴充、劃分及匯出所有跨來源資料。
* 使用集中化流程每個步驟都提供的資料管理工具來管理您的資料，以確保您的資料符合法律法規和業務策略。

有關為即時CDP B2B Edition所做改進的更全面的詳細資訊，分為以下幾節。

## XDM

Real-time CDP B2B Edition提供數種新的XDM架構類別、欄位群組和關係類型，可專門用於B2B用途擷取和建構您的資料。 請參閱 [即時CDP B2B版中的XDM](./schemas/b2b.md) 以劃分這些增強功能。

透過使用預先設定的B2B結構，您可以將資料匯入標準化、可操作的結構。 許多新結構類別幾乎直接對應至主流CRM中遇到的結構類別，例如 [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo]，以及其他B2B資料來源。 使用即時CDP B2B Edition，您可以以簡單明瞭的方式將B2B來源的資料帶入Platform，並取得易於稽核的結果。

這些XDM增強功能可讓您透過B2B為中心的來源和目的地，以更佳的方式擷取和啟用資料，並針對更多種化、更靈活的使用案例，改善資料統一和呈現方式。

## 身分解析

定義結構並擷取符合這些結構的資料後，即時CDP B2B Edition會透過功能強大的即時身分解析系統，識別代表真實人員和企業的來源記錄。

身份解析系統提供下列功能：

* B2B和B2C人員記錄組合
* 多級帳戶階層
* 多對多、人員對帳戶的關係
* 人員和帳戶身分可即時解析

已擴大身份解決系統，以支援更多層面的人員分類。 該系統允許將人員識別為商機中的銷售機會以及客戶。

由來源CRM同步並透過系統內多個路徑連接的帳戶記錄，會由Platform合併在一起。 該系統將那些與業務機會相關的人和那些記錄為客戶的人聚集在一起，但如果他們是可識別的，他們之間的區別也能夠保留。

匹配的標識符用於連結在一起並合併來自多個系統的帳戶記錄。 在整個過程中會保留帳戶層次結構。 使用獨特點會仔細檢查某人是否與某個帳戶相關聯，並在需要時提供將其與帳戶分開的能力。

## 設定檔與區段

一旦即時CDP B2B Edition擷取了與人員、公司、屬性和行為相關的資料和已解析的身分識別，該資料就會用來建立設定檔。 然後，這些設定檔可以分段為可瀏覽的對象，然後可以啟動至各種目的地。

正確實作時，系統會使用唯一的主要識別碼來追蹤使用者，而非可能變更的屬性，例如電子郵件地址。 這表示當有人變更工作時，系統仍會依循這些工作。 該人員仍是同一實體，但會連結至新帳戶。 此原生功能提供擴展至新帳戶的絕佳向量，因為系統會以個人身分跟隨這些人，包括其所有屬性和行為。

## B2B來源

Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加上標籤，以及增強傳入資料。 此 [!DNL Marketo] 來源可讓您將B2B資料串流至Platform，並使用與平台連線的應用程式讓此資料保持最新。 支援任意數量的例項 [!DNL Marketo] （這對具有多個執行個體的大型公司有好處）並拉進合併資料的單一IMS組織。

>[!NOTE]
>
>此 [!DNL Marketo] 來源為 **not** 需要，才能使用Real-time CDP B2B Edition。

請參閱 [即時CDP B2B版中的源](./sources/b2b.md) 檔案，以取得Marketo和將B2B資料匯入Platform的詳細資訊。

## B2B目的地

Experience Platform目的地(例如Google Customer Match、Facebook、LinkedIn、Marketo Engage、Amazon S3、Google Display &amp; Video 360、Google Ads和Google Ad Manager)均可供即時CDP B2B Edition使用，且完全受支援。 Marketo Engage目的地也會從Platform串流區段成員資格資料，並在Marketo中以清單形式提供。

請參閱 [Marketo Engage目標](../destinations/catalog/adobe/marketo-engage.md) 以取得更多資訊。

若公司有多個CRM,Real-time CDP B2B Edition提供可設定目標連接器以區隔Marketo或CRM的例項的選項。 如有需要，您可以設定每個例項的目的地連接器，並個別傳送對象至每個CRM例項。

## 後續步驟

現在您更清楚了解即時CDP B2B Edition為行銷人員提供的優點，以及它與即時CDP之間的差異，便能了解如何將這些功能套用至您自己的IMS組織。

要了解即時CDP B2B Edition如何使您的企業對企業服務模型受益，請參閱以下文檔以幫助您開始：

* [Real-time CDP B2B Edition的範例使用案例](./b2b-use-case.md)
* [Real-time Customer Data Platform B2B版的端對端教學課程](./b2b-tutorial.md)
* [如何內嵌資料](./sources/b2b.md)
* [如何存取設定檔](./profile/profile-overview.md)
* [Real-time Customer Data Platform B2B版中的結構描述](./schemas/b2b.md)
* [如何建立區段](./segmentation/b2b.md)
* [如何對目的地啟用區段](./destinations/b2b.md)
* [如何定義和實施資料控管政策](./privacy/data-governance-overview.md)
