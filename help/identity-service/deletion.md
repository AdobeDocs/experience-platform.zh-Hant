---
title: Identity Service中的刪除內容
description: 本檔案概略介紹您可在Experience Platform中刪除身分資料的各種機制，並說明身分圖表可能受到哪些影響。
source-git-commit: 506d47035622e45f72a8d92aeff6c5ec4e3d0856
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 1%

---

# Identity Service中的刪除內容

Adobe Experience Platform Identity Service可決定性地連結個人的不同裝置和系統的身分，借此產生身分圖表。 當在同一資料行內接收到兩個或更多個標籤標識時，建立標識圖連結。

即時客戶個人檔案會運用身分圖表，建立客戶屬性和行為的全面且單一檢視，讓您能即時提供具影響力、個人的數位體驗，供使用者而非裝置使用。

本檔案概略介紹您可在Experience Platform中刪除身分資料的各種機制，並說明身分圖表可能受到哪些影響。

## 快速入門

以下文檔參考了以下Experience Platform功能：

* [Identity服務](home.md):跨裝置和系統橋接身分，以更全面了解個別客戶及其行為。
   * [身分圖](./ui/identity-graph-viewer.md):身分圖是特定客戶不同身分之間關係的地圖，可以透過視覺化呈現方式呈現客戶如何透過不同管道與品牌互動。
   * [身分識別命名空間](namespaces.md):身分識別命名空間是身分識別服務的元件，用作身分識別相關內容的指標。 例如，它們會區分「name」的值<span>@email.com」作為電子郵件地址，或「443522」作為數值CRM ID。
* [目錄服務](../catalog/home.md):在資料湖中探索資料處理歷程、中繼資料、檔案說明、目錄和資料集。
* [資料衛生](../hygiene/home.md):透過排程自動資料集的有效期，或從一個資料集或所有資料集中刪除個別記錄，管理您儲存的消費者資料。
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md):管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的請求。
* [即時客戶個人檔案](../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的客戶設定檔。

## 單一身份刪除

單一身分刪除請求可讓您刪除圖形中的身分，因此移除與單一使用者身分識別相關聯的連結，此身分識別命名空間與此身分識別相關聯。 您可以使用 [資料衛生](../hygiene/home.md) 針對資料清除、移除匿名資料，或針對您已收集的資料將資料最小化。 若是使用案例，例如客戶要求刪除資料及遵循隱私權法規(如一般資料保護規範(GDPR))，則您可以使用 [Privacy Service](../privacy-service/home.md).

以下各節將概述可在Experience Platform中用於單一身分刪除請求的機制。

### 在Privacy Service中刪除單一身分

Privacy Service會處理客戶要求存取、選擇退出銷售或刪除其個人資料的請求，如一般資料保護規範(GDPR)和加州消費者隱私法(CCPA)等隱私權法規所規定。 透過Privacy Service，您可以使用API或UI提交工作請求。 當Experience Platform從Privacy Service收到刪除請求時，Platform會傳送確認給Privacy Service，確認已收到請求，且受影響的資料已標示為刪除。 個別身分的刪除是根據提供的命名空間及/或ID值。 此外，會刪除與指定組織相關聯的所有沙箱。 如需詳細資訊，請參閱 [Identity Service中的隱私權要求處理](privacy.md).

### 在 [!UICONTROL 資料衛生] 工作區

此 [[!UICONTROL 資料衛生] 工作區](../hygiene/ui/overview.md) 在Platform UI中，您可以刪除參與Identity Service和即時客戶設定檔的消費者記錄。 有關使用的完整指南 [!UICONTROL 資料衛生] 工作區，請參閱 [刪除用戶記錄](../hygiene/ui/record-delete.md).

下表列出Privacy Service和資料衛生中單一身分刪除之間的差異：

| 單一身分刪除 | Privacy Service | 資料衛生 |
| --- | --- | --- |
| 接受的使用案例 | 僅限資料隱私權請求(GDPR、CCPA)。 | 管理儲存在Experience Platform中的資料。 |
| 預估延遲 | 天至周 | 日 |
| 受影響的服務 | Privacy Service中的單一身分刪除可讓您選取資料是從Identity Service、即時客戶個人檔案還是資料湖中刪除。 | 資料衛生中的單一身分刪除會刪除Identity Service、即時客戶設定檔和資料湖中選取的資料。 |
| 刪除模式 | 從Identity Service刪除身分。 | 從Identity Service、所有資料集或單一資料集中，完全刪除身分及其所有對應連結。 |

{style=&quot;table-layout:auto&quot;}

## 資料集刪除

以下各節將概述可用來刪除資料集和Experience Platform中相關身份連結的機制。

### 目錄服務中的資料集刪除

您可以使用目錄服務來提交刪除資料集的請求。 如需如何使用Catalog Service刪除資料集的詳細資訊，請參閱 [使用目錄服務API刪除對象](../catalog/api/delete-object.md). 或者，您也可以使用Platform UI提交刪除資料集的請求。 如需詳細資訊，請閱讀 [資料集使用指南](../catalog/datasets/user-guide.md#delete-a-dataset).

### 資料衛生中的資料集過期

此 [[!UICONTROL 資料衛生] 工作區](../hygiene/ui/overview.md) 在Adobe Experience Platform UI中，可讓您排程資料集的到期日。 當資料集到期日時，資料湖、身分服務和即時客戶設定檔會開始個別的程式，從各自的服務中移除資料集的內容。 如需詳細資訊，請參閱 [使用管理資料集過期時間 [!UICONTROL 資料衛生] 工作區](../hygiene/ui/dataset-expiration.md).

下表列出目錄服務中刪除資料集與資料衛生之間的差異：

| 資料集刪除 | 目錄服務 | 資料衛生 |
| --- | --- | --- |
| 接受的使用案例 | 刪除Platform中的完整資料集及其相關的身分資訊。 | 管理儲存在Experience Platform中的資料。 |
| 預估延遲 | 日 | 日 |
| 受影響的服務 | 透過目錄服務刪除資料集會從Identity Service、即時客戶個人檔案和資料湖中刪除資料。 | 透過資料衛生刪除資料集會刪除Identity Service、即時客戶設定檔和資料湖的資料。 |
| 刪除模式 | 從特定資料集建立的Identity Service中刪除連結的身分識別。 | 根據到期時間表，從特定資料集建立的Identity Service中刪除連結的身分。 |

{style=&quot;table-layout:auto&quot;}

## 刪除後身份圖的不同狀態

如刪除請求所指定，所有身分圖表刪除都會刪除兩個或更多身份之間的連結。 對於資料集刪除請求，指定資料集建立的所有身分連結都會遭到移除，且可能會或不會從圖形中移除身分。 對於單個身份刪除請求，會為指定身份刪除身份連結，因此，會從所有身份圖中刪除身份值本身。 沒有與其他身分連結的身分不會儲存在Identity Service中。

以下概述刪除可能對身份圖狀態產生的潛在影響。

| 身分圖表狀態 | 說明 |
| --- | --- |
| 部分更新 | 成功處理刪除請求後，當圖形內至少有兩個身分保持連結時，就會發生圖形的部分更新。 刪除後，剩餘的身份連結可以保持彼此連接，或者根據刪除的身份，它們可以拆分成兩個或更多個單獨的圖形。 |
| 完全移除 | 圖表必須至少有兩個連結的身分，才能存在。 因此，如果刪除請求導致移除圖表內的所有現有連結，則圖表將會完全移除。 |
| 無更改 | 如果特定刪除請求包含未與圖形任何成員關聯的身分或資料集，則圖形不會受到影響。 此外，即使刪除請求並未移除資料集或身分資料集組合之間的連結，由於該連結是由另一個未刪除的連結所建立，該圖表也不會更新。 這表示如果兩個不同的資料集中有連結，圖表將不會更新，因為只會移除其中一個資料集。 |

{style=&quot;table-layout:auto&quot;}

## 後續步驟

本檔案說明您可使用哪些機制來刪除Experience Platform上的身分和資料集。 本檔案也概述身分和資料集刪除對身分圖表的影響。 如需Identity Service的詳細資訊，請參閱 [Identity服務概述](home.md).