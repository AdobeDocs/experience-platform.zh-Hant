---
title: Identity Service中的刪除
description: 本檔案概述您可以在Experience Platform中刪除身分資料的各種機制，並清楚說明身分圖表可能受到哪些影響。
exl-id: 0619d845-71c1-4699-82aa-c6436815d5b3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 1%

---

# Identity Service中的刪除

Adobe Experience Platform Identity Service會透過決定性地連結個別人員跨裝置和系統的身分，以產生身分圖表。 在同一資料列中收到兩個或多個標籤的身分時，會建立身分圖表連結。

即時客戶個人檔案會運用身分圖表，針對客戶屬性和行為建立完整且單一檢視，讓您即時向使用者（而非裝置）提供具影響力的個人數位體驗。

本檔案概述您可以在Experience Platform中刪除身分資料的各種機制，並清楚說明身分圖表可能受到哪些影響。

## 快速入門

以下檔案參考Experience Platform的下列功能：

* [身分識別服務](../home.md)：透過跨裝置和系統橋接身分，以更清楚瞭解個別客戶及其行為。
   * [身分圖表](./identity-graph-viewer.md)：身分圖表是特定客戶不同身分之間關係的對應，可讓您以視覺化方式呈現客戶如何跨不同管道與您的品牌互動。
   * [身分識別名稱空間](./namespaces.md)：身分識別名稱空間是Identity Service的元件，用來做為身分識別相關內容的指標。 例如，它們區分「name<span>@email.com」作為電子郵件地址或「443522」作為數字CRMID的值。
* [目錄服務](../../catalog/home.md)：探索資料湖中的資料譜系、中繼資料、檔案說明、目錄和資料集。
* [資料衛生](../../hygiene/home.md)：排程自動化資料集有效期，或從單一資料集或所有資料集中刪除個別記錄，以管理您儲存的消費者資料。
* [Adobe Experience Platform Privacy Service](../../privacy-service/home.md)：管理客戶透過Adobe Experience Cloud應用程式存取、選擇退出銷售或刪除其個人資料的請求。
* [即時客戶個人檔案](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶個人檔案。

## 單一身分刪除

單一身分刪除請求可讓您刪除圖表中的身分，導致移除與身分名稱空間關聯的單一使用者身分相關聯的連結。 您可以使用[Privacy Service](../../privacy-service/home.md)提供的機制來處理使用案例，例如客戶要求刪除資料以及遵循隱私權法規(例如一般資料保護規範(GDPR))的要求。

以下各節會概述您可以在Experience Platform中用於單一身分刪除請求的機制。

### Privacy Service中的單一身分刪除

Privacy Service會根據一般資料保護規範(GDPR)和加州消費者隱私保護法(CCPA)等隱私權法規，處理客戶存取、選擇退出銷售或刪除其個人資料的請求。 透過Privacy Service，您可以使用API或UI提交工作請求。 當Experience Platform收到來自Privacy Service的刪除請求時，Experience Platform會向Privacy Service傳送確認訊息，確認已收到請求並標籤要刪除受影響的資料。 個人身分的刪除是根據提供的名稱空間和/或ID值。 此外，刪除也會針對與指定組織相關聯的所有沙箱進行。 如需詳細資訊，請參閱在Identity Service[&#128279;](../privacy.md)中處理隱私權要求的指南。

下表提供Privacy Service中單一身分刪除的劃分資訊：

| 單一身分刪除 | Privacy Service |
| --- | --- |
| 接受的使用案例 | 僅限資料隱私權請求(GDPR、CCPA)。 |
| 預估延遲 | 數天至數週 |
| 受影響的服務 | Privacy Service中的單一身分刪除可讓您選擇資料將會從身分服務、即時客戶設定檔或資料湖中刪除。 |
| 刪除模式 | 從Identity Service刪除身分。 |

{style="table-layout:auto"}

## 資料集刪除

以下各節概述了可用來刪除Experience Platform中的資料集和相關身份關聯的機制。

### 目錄服務中的資料集刪除

您可以使用目錄服務來提交資料集刪除請求。 如需如何使用目錄服務刪除資料集的詳細資訊，請參閱使用目錄服務API[&#128279;](../../catalog/api/delete-object.md)刪除物件的指南。 或者，您可以使用Experience Platform UI來提交資料集刪除請求。 如需詳細資訊，請閱讀[資料集使用手冊](../../catalog/datasets/user-guide.md#delete-a-dataset)。

### 資料衛生中的資料集有效期

Adobe Experience Platform UI中的[[!UICONTROL 資料衛生]工作區](../../hygiene/ui/overview.md)可讓您排程資料集的到期時間。 當資料集到達其到期日時，資料湖、身分服務和即時客戶設定檔會開始個別程式，從各自的服務中移除資料集的內容。 如需詳細資訊，請參閱[使用[!UICONTROL 資料衛生]工作區](../../hygiene/ui/dataset-expiration.md)管理資料集有效期的指南。

下表提供目錄服務和資料衛生中資料集刪除之間的差異明細：

| 資料集刪除 | 目錄服務 | 資料衛生 |
| --- | --- | --- |
| 接受的使用案例 | 刪除Experience Platform中的完整資料集及其相關身分資訊。 | 管理Experience Platform中儲存的資料。 |
| 預估延遲 | 日 | 日 |
| 受影響的服務 | 透過目錄服務刪除資料集將會從Identity Service、即時客戶設定檔和資料湖中刪除資料。 | 透過資料檢疫刪除資料集將會從身分服務、即時客戶設定檔和資料湖中刪除資料。 |
| 刪除模式 | 從由特定資料集建立的Identity Service中刪除連結的身分。 | 根據到期日排程，從由特定資料集建立的Identity Service中刪除連結的身分。 |

{style="table-layout:auto"}

## 刪除後身分圖表的不同狀態

所有身分圖表刪除都會移除兩個或多個身分之間的連結，如刪除請求所指定。 對於資料集刪除請求，會移除指定資料集建立的所有身分連結，而且不一定會將身分從圖形中移除。 對於單一身份刪除請求，會移除指定身份的身份連結，因此會從所有身份圖形中移除身份值本身。 沒有單一連結到另一個身分的身分不會儲存在Identity Service中。

以下概述刪除可能對身分圖狀態產生的影響。

| 身分圖表狀態 | 說明 |
| --- | --- |
| 部分更新 | 成功處理刪除請求後，圖形內至少有兩個身分保持連結，就會發生圖形的部分更新。 刪除後，其餘的身分連結可能會維持彼此連線，或者根據被刪除的身分，這些連結可能會分割成兩個或多個個別的圖表。 |
| 完全移除 | 圖表必須至少有兩個連結的身分才能存在。 因此，如果刪除請求導致移除圖表內的所有現有連結，則圖表將被完全移除。 |
| 無變更 | 如果特定刪除請求包含未與圖表任何成員相關聯的身分或資料集，圖表將不會受到影響。 此外，即使刪除請求確實刪除了資料集或身分資料集組合之間的連結，圖表也不會更新，因為該連結是由未刪除的其他連結所建立。 這表示如果連結存在於兩個不同的資料集中，圖表將不會更新，因為僅會移除其中一個資料集。 |

{style="table-layout:auto"}

## 後續步驟

本檔案說明可用來刪除Experience Platform上身分和資料集的各種機制。 本檔案也概述身分識別與資料集刪除如何影響身分識別圖形。 若要了解更多有關身分識別服務的資訊，請閱讀「[身分識別服務概觀](../home.md)」。

<!--

You can use [Data hygiene](../hygiene/home.md) for data cleansing, removing anonymous data, or data minimization for the data that you have collected.

### Single identity deletion in the [!UICONTROL Data Hygiene] workspace

The [[!UICONTROL Data Hygiene] workspace](../hygiene/ui/overview.md) in the Experience Platform UI allows you to delete consumer records that are participating in Identity Service and Real-Time Customer Profile. For a comprehensive guide on using the [!UICONTROL Data Hygiene] workspace, see the tutorial on [deleting consumer records](../hygiene/ui/record-delete.md).

The table below provides a breakdown of differences between single identity deletion in Privacy Service and Data hygiene:

| Single identity deletion | Privacy Service | Data hygiene |
| --- | --- | --- |
| Accepted use cases | Data privacy requests (GDPR, CCPA) only. | Management of data stored in Experience Platform. |
| Estimated latency | Days to weeks | Days |
| Services impacted | Single identity deletion in Privacy Service allows you to select whether data will be deleted from Identity Service, Real-Time Customer Profile, or data lake. | Single identity deletion in Data hygiene deletes the selected data across Identity Service, Real-Time Customer Profile, and data lake. |
| Deletion patterns | Delete an identity from Identity Service. | Delete an identity from Identity Service. |

-->
