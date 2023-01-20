---
keywords: RTCDP; CDP;Real-time Customer Data Platform；即時客戶資料平台；real time cdp;cdp;rtcdp
title: Real-time Customer Data Platform B2B版的範例使用案例
description: 此範例情境提供您實作 Adobe Real-Time Customer Data Platform B2B Edition 設定的範例。
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 2%

---

# Real-time Customer Data Platform B2B版的範例使用案例

Real-time Customer Data Platform B2B版擴充了現有的Real-Time CDP和Adobe Experience Platform產品，以支援B2B資料和工作流程。 本檔案提供範例使用案例，示範B2B版本提供的其他優點。 包括:

- 結合來自不同獨立資料來源的人員和帳戶資料，以產生全面的檢視，讓您更清楚了解客戶，並更精確地劃分區段。 請參閱 [建立XDM架構關係](./schemas/b2b.md) 以用於各種B2B來源，以取得詳細資訊。
- 根據相關實體的屬性劃分受眾。 這包括帳戶、機會、行銷活動和行銷清單。 區段不再僅限於人員屬性和體驗事件。 請參閱 [B2B區段檔案](./segmentation/b2b.md) 如需建立B2B特定對象的詳細範例。
- 原生支援一個人員與多個帳戶相關的使用案例。

## 使用案例

科技公司Bodea有一項新產品，並想同時透過電子郵件和LinkedIn廣告促銷活動鎖定客戶。 為了最大化行銷活動的效率，Bodea也想要鎖定先前在其產品上花費超過100萬美元、過去一個月曾造訪過新產品頁面的現有帳戶相關人員。

然而，Bodea有兩種不同的業務。 Bodea的第一項業務「1號線」為汽車行業創造了軟體。 其第二行「2號線」銷售3D打印機，用於製造汽車部件。 由於Bodea的兩項業務，從Bodea的客戶帳戶產生的收入資料在單一視圖中並不統一。

每個業務部門都有自己的銷售系統：「CRM 1」和「CRM 2」。 該兩個CRM銷售系統均連接至其本身的行銷自動化平台「Marketo 1」及「Marketo 2」。 來自CRM 1的資料只會同步至Marketo 1，而來自CRM2的資料只會同步至Marketo 2。 最終，他們的資料被維護在不同的公司資訊孤島中。

## 當前資料情況

由於Bodea的兩行業務都向Townsend公司銷售，Townsend業務資料被記錄為每個銷售系統中的兩個單獨帳戶。

在Marketo 1中，Townsend記錄為帳戶1。 它有兩個相關人員(p1@townsend.com和p2@townsend.com)，在CRM 1中有一個以20萬美元（「機會1」）的閉門銷售機會。 該資料會從CRM 1同步至Marketo 1。

在Marketo 2中，Townsend記錄為帳戶2。 客戶2還有兩名相關人員(p2@townsend.com和p3@townsend.com)，在CRM 2中有一個以90萬美元（「機會2」）成交的機會。 該資料會從CRM 2同步至Marketo 2。

為了進行整合及進行其他公司控制，Bodea還設有主資料管理(MDM)系統，其中維護記錄，指出Marketo 1中的帳戶1（和CRM 1）和Marketo 2中的帳戶2（和CRM 2）是同一家公司。

上個月， `p2@townsend.com` 瀏覽了新產品頁面，而Marketo 1記錄了該網站瀏覽。

![帳戶資訊圖表](./assets/account-info.png)

## 問題

第1行剛剛發佈了一款新的軟體產品，希望向Bodea現有的頂級客戶群追加銷售。 Bodea會啟動行銷活動，同時銘記該特定目標對象。

由於相關湯森資訊記錄為Marketo 1的帳戶1和Marketo 2的帳戶2，因此Bodea的行銷團隊無法有效運用孤立的資訊。

這禁止Bodea的行銷團隊利用這個新機會，以這些公司的特定業務聯絡人為目標。

迄今為止，Townsend在所有客戶中累計花費了超過100萬美元購買Bodea產品。 不過，使用舊系統建立的區段，除非單一銷售系統的總花費超過100萬美元，否則不會包括Townsend的任何人。 這是因為收入資料會分列在不同銷售系統的帳戶中。

由於Townsend的支出分散於不同的銷售系統，且個別總計不超過100萬，因此該區段找不到任何符合Marketo 1或Marketo 2資格的人。

### Real-Time CDP B2B版如何解決此問題

有了Real-Time CDP B2B版，Bodea的行銷團隊可以：

- 將來自所有不同來源(多個Marketo和CRM執行個體，以及主資料管理)的資料合併到Real-Time CDP B2B Edition。

透過RT-CDP B2B Edition,Bodea可使用Marketo Engage來源連接器，將Marketo 1和Marketo 2的B2B資料匯入Experience Platform，並透過與Platform連線的應用程式，讓此資料保持最新。 請參閱 [Marketo來源連接器](../sources/connectors/adobe-applications/marketo/marketo.md) 檔案以取得詳細資訊。

CRM1的B2B資料（人員、帳戶、機會和活動）會同步至Marketo 1。 同樣地，來自CRM 2的所有B2B資料都會同步至Marketo 2。 它們會透過Marketo來源連接器同步至Adobe Experience Platform。 不過，如果Bodea想將CRM的其他資料帶入Experience Platform，他們可以使用現有的CRM連接器。

為了簡單起見，為了這個範例的目的，人們被他們的電子郵件識別。 此範例的合併帳戶資料如下所示：

| 人員 |
|---|
| p1@townsend.com |
| p2@townsend.com（上個月瀏覽過新產品頁面） |
| p3@townsend.com |

| 機會（閉門） |
|---|
| 機會1,20萬美元 |
| 機會2,90萬美元 |

- 使用這個匯總資料，建立不重複的區段，供各種行銷活動使用。 在此範例中，區段會找出符合下列條件的所有人：

   - 擁有相關機會（所有客戶）超過100萬美元
   - 和
   - 在上個月瀏覽過產品頁面

- 建立受眾，成為Bodea新行銷活動最有效的收件者。 在此範例中， RT-CDP、B2B Edition將協助行銷人員識別 `p2@townsend.com` 作為此行銷活動的正確目標。

借由使用Marketo Engage和LinkedIn目的地，Bodea為其行銷團隊提供端對端客戶體驗管理(CXM)解決方案。 在「Experience Platform」中建立的對象會推送至Marketo目的地，其會以靜態清單顯示。 然後，此對象會自動新增至Marketo行銷活動。 同時，RT-CDP B2B Edition也可將對象傳送至LinkedIn行銷活動。

## 後續步驟

閱讀本檔案後，您現在已了解可使用Real-Time CDP B2B版解決的目標與問題類型。

建議您參考下列檔案，以進一步了解B2B特定功能：

- [Real-time Customer Data Platform B2B版端對端教學課程](./b2b-tutorial.md)
- [Real-time Customer Data Platform B2B版中的來源](./sources/b2b.md)
- [Real-time Customer Data Platform B2B版中的結構描述](./schemas/b2b.md)
- [B2B區段範例](./segmentation/b2b.md)
- [帳戶設定檔概述](./accounts/account-profile-overview.md)
- [Real-time Customer Data Platform B2B版目的地](./destinations/b2b.md)
- [設定LinkedIn相符的對象目的地](../destinations/catalog/social/linkedin.md)
