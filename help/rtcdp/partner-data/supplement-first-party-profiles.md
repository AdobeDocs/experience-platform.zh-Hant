---
title: (Beta)使用合作夥伴提供的屬性來補充第一方記錄檔
description: 瞭解如何使用來自受信任資料合作夥伴的屬性來補充第一方設定檔，以改善您的資料基礎、獲得對客戶群的新洞察以及更好的受眾最佳化。
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 2a072ce9351a84263a50597967b994162de18d81
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# 使用合作夥伴提供的屬性來補充第一方設定檔

>[!AVAILABILITY]
>
>* 擁有授權Real-Time CDP （應用程式服務）、Adobe Experience Platform Activation、Real-time CDP、Real-Time CDP Prime、Real-Time CDP Ultimate的客戶可使用此測試版功能。 如需這些套件的詳細資訊，請參閱 [產品說明](https://helpx.adobe.com/legal/product-descriptions.html) 如需詳細資訊，請聯絡您的Adobe代表。

使用來自受信任資料合作夥伴的屬性來補充第一方設定檔，以改善您的資料基礎，並取得對客戶群的新見解，以及獲得更好的受眾最佳化。

![使用合作夥伴提供的屬性使用案例高階視覺化概觀，豐富設定檔。](/help/rtcdp/assets/partner-data/enrichment-use-case-overview.png)

## 先決條件與規劃 {#prerequisites-and-planning}

當您考慮使用資料合作夥伴的屬性來補充您自己的第一方設定檔時，您應該與資料合作夥伴討論並解決下列有關資料擴充回圈的詳細資料：

* 請思考對象清單會從Real-Time CDP匯出的位置，以便與資料供應商共用。 此位置需要支援檔案匯出。
* 資料供應商期望哪些識別碼可以棧疊在其他屬性上？
* 如何將包含合作夥伴提供的屬性的檔案擷取回Real-time CDP？ 例如，可透過雲端儲存空間來源聯結器(例如 [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) 或 [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* 您預期將合作夥伴提供的屬性帶回Real-Time CDP並更新的步調為何？

>[!WARNING]
>
>擷取到Real-Time CDP中的其他合作夥伴提供的屬性會影響 *平均設定檔豐富度*. 閱讀 [Real-time Customer Data Platform產品說明](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 有關設定檔豐富度的詳細資訊。

## 如何達成使用案例：高階概覽 {#achieve-the-use-case-high-level}

![使用合作夥伴提供的屬性使用案例高階視覺化概觀，豐富設定檔。](/help/rtcdp/assets/partner-data/enrichment-use-case-steps.png)

1. As a **客戶**，您可從中授權屬性， **資料合作夥伴**.
2. As a **客戶**，您可擴充設定檔資料和管理模型，以適應 **合作夥伴**&#x200B;提供的屬性。
3. As a **客戶**，即可瞭解您想要透過資料合作夥伴擴充的受眾。 一般而言，這些對象不會輸入識別碼，例如個人識別資訊(PII)元素，例如電子郵件、姓名、地址或其他。
4. 此 **合作夥伴** 為可比對的設定檔附加授權屬性。 （可選）a [合作夥伴ID](/help/identity-service/namespaces.md) 可包含並內嵌至合作夥伴範圍ID名稱空間。
5. As a **客戶**，即可將屬性從資料合作夥伴載入到Real-Time CDP中的客戶設定檔中。

## 如何達成使用案例：逐步指示 {#step-by-step-instructions}

請閱讀以下章節，其中包含進一步檔案的連結，以完成上述高階概觀中的每個步驟。

### 來自合作夥伴的授權屬性 {#license-attributes-from-partner}

此步驟的說明請參閱 [必備條件](#prerequisites-and-planning) 而Adobe則假設您與受信任的資料廠商達成適當的合約協定，以擴充您的第一方設定檔。

### 擴充您的設定檔資料和治理模型，以配合合作夥伴提供的屬性。 {#extend-governance-model}

此時，您需要在Real-Time CDP中擴充資料管理架構，以符合合作夥伴提供的屬性。

您可以選擇建立 **[!UICONTROL XDM個別設定檔]** 類別，或擴充相同型別的現有結構描述以包含合作夥伴提供的屬性。 Adobe強烈建議使用最能代表資料供應商其他屬性的新欄位群組集來建立新結構描述。 這可確保您的資料架構整潔且可彼此獨立演化。

若要將合作夥伴提供的屬性納入結構描述中，您可以使用預期的屬性來建立新的欄位群組，也可以使用Adobe提供的其中一個預先設定的欄位群組。

如需詳細資訊，請閱讀以下檔案頁面：

* [結構描述組合的基本概念](/help/xdm/schema/composition.md)
* [概述 [!UICONTROL XDM個別設定檔] 類別](/help/xdm/classes/individual-profile.md)
* [在UI中建立和編輯結構描述](/help/xdm/ui/resources/schemas.md)
* [在UI中建立和編輯結構描述欄位群組](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

此外，在此步驟中，請思考當您將資料管理策略擴展至包含合作夥伴提供的第三方資料時，您的資料治理模式會如何變更。 探索以下檔案連結中的考量事項：

* (**即將推出**)將協力廠商資料儲存在個別的資料集中，以便輕鬆刪除和還原整合。
* (**即將推出**)使用 [存留時間(TTL)](/help/hygiene/ui/dataset-expiration.md) 已購買資料衛生附加元件之客戶的資料集上。
* (**即將推出**)建立提取協力廠商資料的衍生資料集時請務必小心，因為混合在一起後，移除協力廠商資料的唯一解決方案是刪除整個衍生資料集。

>[!TIP]
>
>如果您選擇使用資料供應商提供的個人識別碼來補充您的客戶設定檔，則可以建立該型別的新身分型別 **[[!UICONTROL 合作夥伴ID]](/help/identity-service/namespaces.md)**.
>
>如需有關合作夥伴ID的詳細資訊，請參閱 [身分型別段落](/help/identity-service/namespaces.md).
>閱讀關於 [如何定義身分欄位](/help/xdm/ui/fields/identity.md) 在Experience Platform使用者介面中。

### 匯出您想在關閉個人識別資訊(PII)或雜湊PII鍵時擴充的受眾 {#export-audiences}

匯出您希望合作夥伴擴充的對象。 使用Real-time CDP提供的雲端儲存空間目標，例如Amazon S3或SFTP。 請閱讀下列檔案頁面，以完成此步驟：

* [Amazon S3目的地](/help/destinations/catalog/cloud-storage/amazon-s3.md) 檔案頁面
* [SFTP目的地](/help/destinations/catalog/cloud-storage/sftp.md) 檔案頁面
* 操作說明 [連線到目的地](/help/destinations/ui/connect-destination.md)
* 操作說明 [將資料匯出至雲端儲存空間目的地](/help/destinations/ui/activate-batch-profile-destinations.md)

### 您的資料合作夥伴會為能夠比對的設定檔附加授權屬性 {#partner-appends-attributes}

在此步驟中，您的資料合作夥伴會為匯出的受眾附加授權屬性。 輸出通常能以平面檔案的形式提供，並可擷取回Real-Time CDP。 深入瞭解 [將檔案擷取至Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP會將擴充的屬性附加至客戶設定檔 {#ingest-data}

您現在需要透過來源聯結器從合作夥伴擷取資料，以將擴充的資料匯回Real-Time CDP，並使用合作夥伴提供的資料補充您的設定檔。

為此目的而建議使用的一些來源聯結器可能是：

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## 限制和疑難排解 {#limitations-and-troubleshooting}

探索本頁面上說明的使用案例時，請注意下列限制：

* 如果您選取使用合作夥伴ID，請注意，建置您的合作夥伴ID時不會使用這些ID [身分圖表](/help/identity-service/ui/identity-graph-viewer.md).

## 透過合作夥伴資料支援達成的其他使用案例 {#other-use-cases}

進一步探索透過Real-Time CDP中的合作夥伴資料支援啟用的使用案例：

* (**即將推出**) [!BADGE Beta]{type=Informative}**善用合作夥伴協助的認可** 進行造訪期間個人化的站上體驗，以及造訪後的離站重新目標定位，使用者不需驗證或先前擁有您品牌的造訪記錄。
* (**即將推出**) [!BADGE Beta]{type=Informative}**擴展啟用** 使用合作夥伴ID來發佈不接受PII或雜湊PII的生態系統。