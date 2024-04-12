---
keywords: RTCDP；CDP；Real-time Customer Data Platform；即時客戶資料平台；real time cdp；cdp；rtcdp
title: Real-time Customer Data Platform B2B版本的範例使用案例
description: 此範例情境提供您實作 Adobe Real-Time Customer Data Platform B2B Edition 設定的範例。
feature: Get Started, Use Cases, B2B
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 2%

---

# Real-time Customer Data Platform B2B版本的範例使用案例

Real-time Customer Data Platform B2B版本擴充了現有的Real-Time CDP和Adobe Experience Platform產品，以支援B2B資料和工作流程。 本檔案提供的範例使用案例會示範B2B版本提供的其他優點。 包括:

- 結合來自不同獨立資料來源的個人和帳戶資料，以產生全面檢視，從而更好地瞭解客戶並更準確地劃分。 請參閱以下檔案： [建立XDM結構描述關係](./schemas/b2b.md) 用於各種B2B來源，以取得詳細資訊。
- 根據相關實體的屬性來細分對象。 這包括客戶、商機、行銷活動和行銷清單。 對象不再侷限於「人員」屬性和「體驗事件」。 請參閱 [B2B分段檔案](./segmentation/b2b.md) 以取得建立B2B特定對象的更多範例。
- 原生支援與多個帳戶相關之個人的使用案例。

## 使用案例

Bodea是一家技術公司，推出一項新產品，並且想要透過電子郵件和LinkedIn廣告行銷活動同時鎖定客戶。 為了最大化行銷活動的效率，Bodea也想要將目標鎖定於與該現有帳戶相關聯的人員，這些人員先前在其產品上花費超過100萬美元，且上個月造訪過新產品頁面。

不過，Bodea有兩個不同的業務領域。 Bodea的第一項業務「第1項」為汽車產業建立軟體。 其第二項業務「Line 2」銷售製造汽車零件的3D印表機。 由於Bodea的業務分為兩個部門，因此從Bodea客戶帳戶產生的收入資料並未統一於單一檢視中。

每個業務線都有自己的銷售系統：「CRM 1」和「CRM 2」。 這兩種CRM銷售系統皆已連線至其專屬的行銷自動化平台「Marketo 1」和「Marketo 2」。 來自CRM 1的資料只會同步至Marketo 1，而來自CRM2的資料只會同步至Marketo 2。 最終，他們的資料會儲存在不同的企業資訊獨立單位中。

## 目前的資料狀況

由於Bodea的兩項業務都銷售給Townsend公司，因此Townsend業務資料會記錄為每個銷售系統中的兩個獨立帳戶。

在Marketo 1中，Townsend會記錄為「帳戶1」。 在CRM 1中，它有兩個相關人員(p1@townsend.com和p2@townsend.com)以及一個已成交的20萬美元商機（「商機1」）。 該資料會從CRM 1同步至Marketo 1。

在Marketo 2中，Townsend會記錄為「帳戶2」。 帳戶2在CRM 2中也有2個相關人員(p2@townsend.com和p3@townsend.com)和1個已結束的90萬美元商機（「商機2」）。 該資料會從CRM 2同步至Marketo 2。

為了整合和其他企業控制目的，Bodea也有一個主要資料管理(MDM)系統，在此維護一筆記錄，指出Marketo 1中的帳戶1 （和CRM 1）和Marketo 2中的帳戶2 （和CRM 2）是同一公司。

在上個月， `p2@townsend.com` 造訪新產品頁面，而Marketo 1記錄了網頁造訪。

![帳戶資訊圖表](./assets/account-info.png)

## 問題

第1行剛剛推出新的軟體產品，希望向Bodea現有的頂級客戶群進行追加銷售。 Bodea會針對特定目標對象啟動行銷活動。

由於相關的Townsend資訊在Marketo 1中記錄為「帳戶1」，在Marketo 2中記錄為「帳戶2」，因此Bodea的行銷團隊無法有效利用定址資訊。

這可防止Bodea的行銷團隊有效率地利用這個新機會鎖定這些公司的特定業務聯絡人。

到目前為止，Townsend在其所有帳戶中累計在Bodea產品上花費超過一百萬美元。 不過，使用舊系統建立的受眾不會包含來自Townsend的任何人，除非在單一銷售系統中花費的總額超過100萬美元。 這是因為收入資料是儲存在不同銷售系統下的帳戶中。

由於Townsend的開支分散於不同的銷售系統，且個別而言的總金額不超過100萬，因此區段定義無法在Marketo 1或Marketo 2中找到符合資格的人員。

### Real-Time CDP B2B版本如何解決問題

有了Real-Time CDP B2B Edition，Bodea的行銷團隊可以：

- 將來自所有不同來源(多個Marketo和CRM執行個體以及主要資料管理)的資料合併到Real-Time CDP B2B版本中。

透過RT-CDP B2B Edition，Bodea可以使用Marketo Engage來源聯結器將來自Marketo 1和Marketo 2的B2B資料帶入Experience Platform，並使用平台連線的應用程式保持此資料最新。 請參閱 [Marketo來源聯結器](../sources/connectors/adobe-applications/marketo/marketo.md) 檔案以取得詳細資訊。

來自CRM1的B2B資料（人員、帳戶、機會和活動）會同步至Marketo 1。 同樣地，來自CRM 2的所有B2B資料都會同步至Marketo 2。 透過Marketo來源聯結器將其同步至Adobe Experience Platform。 但是，如果Bodea想要從CRM將其他資料引入Experience Platform，則他們可以使用現有的CRM聯結器。

為了簡單起見，以及此範例的目的，系統會透過電子郵件識別使用者的身分。 此範例的合併帳戶資料如下所示：

| 人員 |
|---|
| p1@townsend.com |
| p2@townsend.com （上個月造訪過新產品頁面的訪客） |
| p3@townsend.com |

| 商機（成功） |
|---|
| 商機1，$20萬 |
| 機會2，$900,000 |

- 針對不同的行銷方案，使用此彙總資料建立唯一受眾。 在此範例中，區段定義會尋找符合以下條件的所有人員：

   - 擁有相關商機（跨所有帳戶）超過一百萬美元的價值
   - AND
   - 在上個月造訪過產品頁面

- 建立受眾，使其成為Bodea新行銷活動最有效的收件者。 在此範例中，RT-CDP， B2B Edition將協助行銷人員識別 `p2@townsend.com` 作為此行銷活動的正確目標。

藉由使用Marketo Engage和LinkedIn目的地，Bodea為其行銷團隊提供端對端客戶體驗管理(CXM)解決方案。 在Experience Platform中建立的對象會推送至Marketo目的地，並在其中顯示為靜態清單。 然後，此對象會自動新增至Marketo行銷活動。 同時，受眾也可以透過RT-CDP B2B Edition傳送到LinkedIn行銷活動。

## 後續步驟

閱讀本檔案後，您現在已瞭解可以使用Real-Time CDP B2B Edition解決的目標和問題型別。

建議您參閱下列檔案，以進一步瞭解B2B的特定功能：

- [Real-time Customer Data Platform B2B Edition端對端教學課程](./b2b-tutorial.md)
- [Real-time Customer Data Platform B2B Edition中的來源](./sources/b2b.md)
- [Real-time Customer Data Platform B2B版本中的結構描述](./schemas/b2b.md)
- [B2B分段範例](./segmentation/b2b.md)
- [帳戶設定檔概述](./accounts/account-profile-overview.md)
- [Real-time Customer Data Platform B2B Edition中的目的地](./destinations/b2b.md)
- [設定LinkedIn相符的受眾目的地](../destinations/catalog/social/linkedin.md)
