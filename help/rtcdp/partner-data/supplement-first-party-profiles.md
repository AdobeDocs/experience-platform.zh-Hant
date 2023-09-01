---
title: 使用合作夥伴提供的屬性補充第一方設定檔
description: 了解如何使用受信任資料合作夥伴的屬性來補充第一方設定檔，以改善您的資料基礎，對客戶群取得新的分析，以及更佳的對象最佳化。
source-git-commit: 9dd305be4dcb45c290a2b8ee0476191949369adc
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 100%

---

# 使用合作夥伴提供的屬性補充第一方設定檔

>[!AVAILABILITY]
>
>* 此功能可供已獲得 Real-Time CDP (應用程式服務)、Adobe Experience Platform Activation、Real-time CDP、Real-Time CDP Prime、Real-Time CDP Ultimate 授權的客戶使用。如需詳細資訊，請閱讀[產品說明](https://helpx.adobe.com/legal/product-descriptions.html)中有關這些套件的詳細資料，並和您的 Adob&#x200B;&#x200B;e 代表聯絡。

使用受信任資料合作夥伴的屬性來補充第一方設定檔，以改善您的資料基礎並對客戶群取得新的分析，而且獲致更佳的對象最佳化。

![使用合作夥伴提供的屬性使用案例高層級視覺化概觀擴充設定檔。](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-overview.png)

## 必要條件和規劃 {#prerequisites-and-planning}

考慮使用資料合作夥伴的屬性來補充您自己的第一方設定檔時，您應該和該資料合作夥伴討論並解決有關資料擴充循環的以下詳細資料：

* 考慮從 Real-Time CDP 匯出對象清單的位置，以便和資料廠商共用。該位置需要能支援檔案匯出。
* 資料廠商期望有哪些識別碼，以便他們可在額外屬性上分層堆放？
* 如何將包含合作夥伴提供之屬性的檔案擷取回 Real-time CDP？例如，可透過雲端儲存空間來源連接器 (如 [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) 或 [SFTP](/help/sources/connectors/cloud-storage/sftp.md)) 擷取檔案。
* 您期望將合作夥伴提供之屬性帶回 Real-Time CDP 並重新整理的節奏為何？

>[!WARNING]
>
>擷取至 Real-Time CDP 的合作夥伴提供之額外屬性會影響您的&#x200B;*平均設定檔豐富度*。如需有關設定檔豐富度的詳細資訊，請閱讀 [Real-Time Customer Data Platform 產品說明](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)。

## 如何實現使用案例：高層級概觀 {#achieve-the-use-case-high-level}

![使用合作夥伴提供的屬性使用案例高層級視覺化概觀擴充設定檔。](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-steps.png)

1. 身為&#x200B;**客戶**，您會向&#x200B;**資料合作夥伴**&#x200B;取得授權。
2. 身為&#x200B;**客戶**，您會擴充您的設定檔資料和治理模式以和&#x200B;**合作夥伴**&#x200B;提供的屬性相符。
3. 身為&#x200B;**客戶**，您要吸引想使用資料合作夥伴擴充的對象。一般來說，會刪去這些對象的個人可識別資訊 (PII) 之類的輸入識別碼，例如電子郵件、姓名、地址等。
4. **合作夥伴**&#x200B;會為其可相匹配的設定檔附加已授權的屬性。另一個選擇是可將[合作夥伴 ID](/help/identity-service/namespaces.md) 納入並擷取至合作夥伴範圍的 ID 命名空間中。
5. 身為&#x200B;**客戶**，您可以將資料合作夥伴的屬性載入至 Real-Time CDP 中的客戶設定檔。

## 如何實現使用案例：逐步說明 {#step-by-step-instructions}

詳閱以下章節，其中包含指向更多文件的連結，以完成上述高層級概觀中的每個步驟。

### 來自合作夥伴的授權屬性 {#license-attributes-from-partner}

此步驟包含在[必要條件](#prerequisites-and-planning)中，而且 Adobe 假定您已和受信任的資料廠商簽訂適合的合約協議，以增強您的第一方設定檔。

### 擴充您的設定檔資料和治理模式以和合作夥伴提供的屬性相符。 {#extend-governance-model}

此刻，您正要擴充 Real-Time CDP 中的資料管理架構，以和合作夥伴提供的屬性相符。

您可選擇建立 **[!UICONTROL XDM 個別設定檔]**&#x200B;類別的新綱要，或擴充相同類型的現有綱要以包含合作夥伴提供的屬性。Adobe 強烈建議使用一組最能代表資料廠商的額外屬性的新欄位群組建立新綱要。這可確保您的資料綱要未使用過且彼此都可獨立地發展。

若要在綱要中包含合作夥伴提供的屬性，您可以使用期望的屬性建立新的欄位群組，也可以使用 Adob&#x200B;&#x200B;e 提供的其中一個預先設定的欄位群組。

如需詳細資訊，請閱讀以下文件頁面：

* [綱要組合的基本](/help/xdm/schema/composition.md)
* [[!UICONTROL XDM 個別設定檔]類別的概觀](/help/xdm/classes/individual-profile.md)
* [在 UI 中建立和編輯綱要](/help/xdm/ui/resources/schemas.md)
* [在 UI 中建立和編輯綱要欄位](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

此外，在此步驟中，請考慮隨著您擴大資料管理策略以包含合作夥伴提供的協力廠商資料時，您的資料治理模式會如何變更。探索以下文件連結中的考量事項：

* (**即將推出**) 將協力廠商資料保存在單獨的資料集中，以便可輕鬆進行刪除及還原整合。
* (**即將推出**) 對於購買了資料清理附加元件的用戶端，在資料集上使用[資料集到期](/help/hygiene/ui/dataset-expiration.md)功能。
* (**即將出**) 建立引入協力廠商資料的衍生資料集時需謹慎小心，因為一旦混合在一起，若要移除協力廠商資料，唯一的解決方案是刪除整個衍生資料集。

>[!TIP]
>
>如果您選擇使用資料廠商提供的個人型識別碼來補充您的客戶設定檔，您可以建立類型為&#x200B;**[[!UICONTROL 合作夥伴 ID]](/help/identity-service/namespaces.md)** 的新身分類型。
>
>如需有關合作夥伴 ID 的詳細資訊，請閱讀[身分類型章節](/help/identity-service/namespaces.md)。
>閱讀有關在 Experience Platform 使用者介面中[如何定義身分欄位](/help/xdm/ui/fields/identity.md)的資訊。

### 匯出您在刪去個人可識別資訊 (PII) 或雜湊 PII 時要擴充的對象 {#export-audiences}

匯出您要合作夥伴擴充的對象。使用 Real-time CDP 提供的雲端儲存空間目的地，例如 Amazon S3 或 SFTP。閱讀以下文件頁面以完成此步驟：

* [Amazon S3 目的地](/help/destinations/catalog/cloud-storage/amazon-s3.md)文件頁面
* [SFTP 目的地](/help/destinations/catalog/cloud-storage/sftp.md)文件頁面
* 如何[連線至目的地](/help/destinations/ui/connect-destination.md)
* 如何[將資料匯出到雲端儲存空間目的地](/help/destinations/ui/activate-batch-profile-destinations.md)

### 您的資料合作夥伴會為其可相匹配的設定檔附加已授權的屬性 {#partner-appends-attributes}

在此步驟中，您的資料合作夥伴會為匯出的對象附加授權的屬性。輸出通常會以平面檔案的形式提供，可供擷取回 Real-Time CDP。閱讀有關[將檔案擷取至 Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file) 的詳細資訊。

### Real-Time CDP 會將擴充的屬性附加到客戶設定檔中。 {#ingest-data}

您現在需要透過來源連接器從合作夥伴擷取資料，以將擴充的資料帶回 Real-Time CDP 並使用合作夥伴提供的資料補充您的設定檔。

為此目的推薦的一些來源連接器可能包括：

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## 限制和疑難排解 {#limitations-and-troubleshooting}

當您探索本頁說明的使用案例時，請注意下列限制：

* 如果您選擇使用合作夥伴 ID，請注意在建置您的[身分識別圖](/help/identity-service/ui/identity-graph-viewer.md)時不要使用這些 ID。

## 其他透過合作夥伴資料支援封存的使用案例 {#other-use-cases}

探索透過 Real-Time CDP 中的合作夥伴資料支援啟用的更多使用案例：

* 使用 Real-Time CDP 的協力廠商資料支援，透過資料合作夥伴的潛在客戶設定檔來[擴大您的設定檔庫，並與其互動以獲取或接觸新客戶。](/help/rtcdp/partner-data/prospecting.md)
* [利用合作夥伴輔助識別，不需要使用者驗證或之前使用您的品牌的紀錄，即可在造訪期間提供個人化的現場體驗](/help/rtcdp/partner-data/onsite-personalization.md)。
* [擴大啟用潛在客戶個人資料和潛在客戶對象](/help/destinations/ui/activate-prospect-audiences.md)以選取目的地。