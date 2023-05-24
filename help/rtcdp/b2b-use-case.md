---
keywords: RTCDP;CDP;Real-time Customer Data Platform；即時客戶資料平台；即時cdp;cdp;rtcdp
title: Real-time Customer Data PlatformB2B版示例用例
description: 此範例情境提供您實作 Adobe Real-Time Customer Data Platform B2B Edition 設定的範例。
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 2%

---

# Real-time Customer Data PlatformB2B版示例用例

Real-time Customer Data PlatformB2B版擴展了現有的Real-Time CDP和Adobe Experience Platform產品，以支援B2B資料和工作流。 本文檔提供了一個示例使用案例，演示B2B版提供的附加優勢。 包括:

- 將來自不同獨立資料源的人員和帳戶資料結合起來，可生成一個全面的視圖，使客戶能夠更好地瞭解客戶並更準確地進行細分。 請參閱 [建立XDM架構關係](./schemas/b2b.md) 供各種B2B源使用，以獲取更多資訊。
- 根據相關實體的屬性對受眾進行分段。 這包括帳戶、機會、市場活動和市場營銷清單。 段不再僅限於人員屬性和體驗事件。 查看 [B2B分段文檔](./segmentation/b2b.md) 更多建立特定於B2B的受眾的示例。
- 本機支援與多個帳戶相關的一個人的使用案例。

## 使用案例

科技公司Bodea有一款新產品，希望同時通過電子郵件和LinkedIn的廣告活動瞄準客戶。 為了最大限度地提高營銷活動的效率，Bodea還希望瞄準那些與現有客戶相關的人員，這些人以前在其產品上花費了100萬美元，AND公司在上個月訪問了新產品頁面。

然而，Bodea有兩項業務。 Bodea公司的第一條業務線&quot;1&quot;為汽車行業創造軟體。 第二行&quot;二號線&quot;銷售製造汽車零件的3D打印機。 由於Bodea的兩項業務，從Bodea的客戶帳戶生成的收入資料在單一視圖中不統一。

每個業務部門都有自己的銷售系統：「CRM 1」和「CRM 2」。 該等CRM銷售系統均連接其自有之營銷自動化平台「Marketo1」及「Marketo2」。 來自CRM 1的資料僅同步到Marketo1，來自CRM2的資料僅同步到Marketo2。 最終，他們的資料被維護在不同的公司資訊庫中。

## 當前資料情況

由於Bodea的兩項業務都出售給湯森公司，湯森公司的業務資料在每個銷售系統中記錄為兩個單獨的帳戶。

在Marketo1，湯森德被記為帳戶1。 它有兩名相關人員(p1@townsend.com和p2@townsend.com)，在CRM 1中有一個價值20萬美元（「機會1」）的閉門銷售機會。 該資料從CRM 1同步到Marketo1。

在Marketo2，湯森德被記錄為帳戶2。 客戶2還有兩個相關人員(p2@townsend.com和p3@townsend.com)，在CRM 2中有一個成交額為90萬美元（「機會2」）的機會。 該資料從CRM 2同步到Marketo2。

為了整合和其他公司控制目的，Bodea公司還有一個主資料管理(MDM)系統，在該系統中保存一個記錄，表明Marketo1的帳戶1（和CRM 1）和Marketo2的帳戶2（和CRM 2）是同一家公司。

上個月， `p2@townsend.com` 訪問了新產品頁面，Marketo1號記錄了訪問內容。

![帳戶資訊圖表](./assets/account-info.png)

## 問題

第1行剛剛發佈了一種新軟體產品，希望將其追加銷售給Bodea公司現有的頂級客戶群。 Bodea發起營銷活動時要考慮到特定目標受眾。

由於相關湯森德資訊記錄為Marketo1的帳戶1和Marketo2的帳戶2,Bodea的營銷團隊無法有效地利用單獨的資訊。

這禁止Bodea的營銷團隊利用這一新機會有效地瞄準這些公司的特定商業聯繫人。

迄今為止，湯森德在所有客戶的Bodea產品上累計支出超過100萬美元。 但是，使用舊系統建立的部門不包括來自湯森德的任何人，除非在一個銷售系統內的總支出超過100萬美元。 這是因為收入資料位於不同銷售系統下的帳戶中。

由於湯森德的支出分為不同的銷售系統，且個人總支出不超過100萬，因此該部門找不到Marketo1或Marketo2的合格客戶。

### Real-Time CDPB2B版如何解決問題

借助Real-Time CDPB2B版，Bodea的營銷團隊可以：

- 將來自所有不同源(多個Marketo和CRM實例以及主資料管理)的資料合併到Real-Time CDPB2B版。

借助RT-CDP B2B版，Bodea可以使用Marketo Engage源連接器將Marketo1和Marketo2的B2B資料引入Experience Platform，並使用平台連接的應用程式保持此資料的最新。 查看 [Marketo源連接器](../sources/connectors/adobe-applications/marketo/marketo.md) 的子菜單。

CRM1中的B2B資料（人員、帳戶、機會和活動）同步到Marketo1。 同樣，CRM 2中的所有B2B資料都同步到Marketo2。 他們通過Marketo源連接器同步到Adobe Experience Platform。 但是，如果Bodea希望將CRM中的其他資料引入Experience Platform中，他們可以使用現有的CRM連接器。

為了簡單起見，為了本例的目的，人們被他們的電子郵件識別出來。 此示例的合併帳戶資料如下所示：

| 人員 |
|---|
| p1@townsend.com |
| p2@townsend.com（上個月訪問了新產品頁面） |
| p3@townsend.com |

| 機會（閉門） |
|---|
| 機會1,20萬美元 |
| 機會2,90萬美元 |

- 使用此聚合資料為不同的市場營銷計畫建立獨特的細分市場。 在此示例中，該段將查找以下所有人員：

   - 相關機會（跨所有客戶）的價值超過100萬美元
   - 和
   - 在上個月訪問過產品頁

- 建立受眾，他們是Bodea新營銷活動最有效的受眾。 在此示例中，RT-CDP B2B版將幫助營銷人員確定 `p2@townsend.com` 作為此市場營銷活動的正確目標。

通過使用Marketo Engage和LinkedIn目的地，Bodea為其營銷團隊提供了端到端客戶體驗管理(CXM)解決方案。 以Experience Platform建立的受眾將推送到Marketo目標，該目標顯示為靜態清單。 然後，這些受眾將自動被添加到Marketo市場營銷活動中。 同時，RT-CDP B2B版還可以將觀眾送到LinkedIn的營銷活動中。

## 後續步驟

通過閱讀本檔案，您現在已介紹了使用Real-Time CDPB2B版可解決的目標和問題的類型。

建議使用以下文檔來提高您對B2B特定功能的瞭解：

- [Real-time Customer Data PlatformB2B版端到端教程](./b2b-tutorial.md)
- [Real-time Customer Data PlatformB2B版來源](./sources/b2b.md)
- [Real-time Customer Data PlatformB2B版中的架構](./schemas/b2b.md)
- [B2B分段示例](./segmentation/b2b.md)
- [帳戶配置檔案概述](./accounts/account-profile-overview.md)
- [Real-time Customer Data PlatformB2B版目的地](./destinations/b2b.md)
- [配置LinkedIn匹配的受眾目標](../destinations/catalog/social/linkedin.md)
