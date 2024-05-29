---
title: 不依賴第三方Cookie即可吸引和贏取新客戶
description: 瞭解如何透過潛在使用案例吸引和贏取新客戶，而不需依賴第三方Cookie。
feature: Use Cases, Customer Acquisition
exl-id: b9e7b3af-2a13-4904-bd12-e3ed05a1988e
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2074'
ht-degree: 85%

---

# 不依賴第三方Cookie即可吸引和贏取新客戶

>[!AVAILABILITY]
>
>* 已授權Real-Time CDP （應用程式服務）、Adobe Experience Platform Activation、Real-Time CDP、Real-Time CDP Prime、Real-Time CDP Ultimate的客戶可使用此功能。 如需詳細資訊，請閱讀[產品說明](https://helpx.adobe.com/legal/product-descriptions.html)中有關這些套件的詳細資料，並和您的 Adob&#x200B;&#x200B;e 代表聯絡。

使用 Real-Time CDP 的協力廠商資料支援，透過資料合作夥伴的潛在客戶設定檔來擴大您的設定檔庫，並與其互動以獲取或接觸新客戶。

![挖掘潛在客戶使用案例高層級視覺化概觀。](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## 為何考慮此使用案例 {#why-this-use-case}

品牌同時面臨艱鉅的挑戰，需要負責地執行最上層漏斗式客戶贏取使用案例，而不需要依賴第三方Cookie、有限的預算，以及更高的透明度和廣告支出報酬要求。

Adobe Real-time Customer Data Platform可協助品牌安全地將其支援的資料管理平台(DMP)使用案例轉換為免Cookie的替代方案，其方式可將自助式細分、對象管理和啟用的完整複雜度和功能整合到單一系統中。 Adobe透過專利的資料控管和同意架構，專注負責任地使用資料，絲毫不受影響。

例如，當您需要執行行銷活動以吸引潛在客戶成為使用者或已知客戶時，請遵循此使用案例中所述的步驟。

## 必要條件和規劃 {#prerequisites-and-planning}

當您考慮聯絡及爭取新客戶時，請在計畫處理中考慮下列必要條件：

* 您期望多久一次在 Real-Time CDP 擷取和重新整理合作夥伴提供的設定檔？
* 您的下游目的地需要什麼身分？
* 確保擷取的身分可在下游供操作
* 您擷取的合作夥伴資料是否與廣泛接受的持久身分相關聯，例如個人可識別資訊 (PII)、雜湊 PII 或合作夥伴身分？
* 從合作夥伴的角度以及您自己的法律、隱私權或合規團隊的角度，您需要了解哪些資料使用政策？

## 如何實現使用案例：高層級概觀 {#achieve-the-use-case-high-level}

在擴展 Real-Time CDP 以吸引和獲取新客戶之前，請確保使用 Real-Time CDP 為您的第一方資料建立堅實的基礎。實現此使用案例的工作流程與已知客戶互動的工作流程類似。

![挖掘潛在客戶使用案例高層級視覺化概觀。](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. 作為&#x200B;**客戶**，您可以從一個或多個&#x200B;**資料合作夥伴**&#x200B;取得潛在客戶設定檔，以幫助獲取漏斗頂部的客戶。
2. 作為&#x200B;**客戶**，您擴充您的設定檔資料和治理模型以擷取&#x200B;**合作夥伴**&#x200B;提供的潛在客戶設定檔清單。
3. 作為&#x200B;**客戶**，您將潛在客戶設定檔載入到 Real-Time CDP 並建立治理原則以確保負責任地使用資料。
4. 作為&#x200B;**客戶**，您從潛在客戶設定檔清單建立重點對象。
5. 作為&#x200B;**客戶**，您將潛在客戶對象啟動到接受您潛在客戶清單之身分的目的地。
6. 如有需要，與&#x200B;**資料合作夥伴**&#x200B;協作，將對象啟動到所需付費媒體目的地的最後一里路完成。

## 影片逐步解說 {#video-walkthrough}

觀看以下影片教學課程，逐步瞭解如何觸及及吸引潛在客戶受眾：

>[!VIDEO](https://video.tv.adobe.com/v/3423071/?learn=on)

## 如何實現使用案例：逐步說明 {#step-by-step-instructions}

詳閱以下章節，其中包含指向更多文件的連結，以完成上述高層級概觀中的每個步驟。

### 您將使用的 UI 功能和元素 {#ui-functionality-and-elements}

當您完成實作使用案例的步驟時，您將使用以下 Real-Time CDP 功能和 UI 元素 (按使用順序列出)。確保您擁有所有這些區域所需的屬性型存取控制權限，或要求系統管理員授予您必要的權限。

* [身分](/help/identity-service/features/namespaces.md)
* [結構描述](/help/xdm/home.md)
* [資料使用情況標籤](/help/data-governance/labels/overview.md)
* [資料集](/help/catalog/datasets/overview.md)
* [來源](/help/sources/home.md)
* [潛在客戶設定檔](/help/profile/ui/prospect-profile.md)
* [潛在客戶對象](/help/segmentation/ui/prospect-audience.md)
* [目的地](/help/destinations/home.md)

### 取得來自合作夥伴的協力廠商設定檔詳細資料 {#license-profiles-from-partner}

此步驟包含在[必要條件](#prerequisites-and-planning)中，而且 Adobe 假定您已和受信任的資料廠商簽訂適合的合約協議，可擷取資料合作夥伴提供的潛在客戶設定檔。

### 擴充您的設定檔資料和治理模型以容納合作夥伴提供的潛在客戶設定檔。 {#extend-governance-model}

為了準備從資料合作夥伴接收潛在客戶設定檔，您必須擴充 Real-Time CDP 的資料管理架構以容納此新設定檔類型。

您將使用的身分、資料管理和治理元件包括：

* 新的&#x200B;**[!UICONTROL 合作夥半 ID]** 身分類型，用於合作夥伴提供的設定檔
* 新的 **[!UICONTROL XDM 個別潛在客戶設定檔]** XDM 類別
* **(文件即將推出)** 為合作夥伴資料支援量身打造的欄位群組
* **(文件即將推出)** 您將新增到來自合作夥伴之屬性的協力廠商標籤

#### 建立合作夥伴 ID 身分命名空間 {#create-partner-id-namespace}

首先建立新的身分類型，用於將從合作夥伴收到的設定檔。為此，在「身分」區段中，您必須建立類型&#x200B;**[!UICONTROL 合作夥伴 ID]**&#x200B;的新身分命名空間。

![建立新的合作夥伴 ID 身分命名空間。](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* 如需有關合作夥伴 ID 命名空間的詳細資訊，請閱讀[身分類型章節](/help/identity-service/features/namespaces.md)。
* 閱讀有關在 Experience Platform 使用者介面中[如何定義身分欄位](/help/xdm/ui/fields/identity.md)的資訊。

#### 建立含有 **[!UICONTROL XDM 個別潛在客戶設定檔]**&#x200B;類別的新結構描述

接下來，在「**[!UICONTROL 資料管理]** > **[!UICONTROL 結構描述]**」，建立新結構描述並將 **[!UICONTROL XDM 個別潛在客戶設定檔]**&#x200B;類別指派給它。

![在 XDM 結構描述產生器中搜尋 XDM 個別潛在客戶設定檔類別](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)。

閱讀如何[在 UI 中建立和編輯結構描述](/help/xdm/ui/resources/schemas.md)並取得有關 XDM 個別潛在客戶設定檔的完整資訊 (連結即將推出)。

**[!UICONTROL XDM 個別潛在客戶設定檔]**&#x200B;類別預先設定在下方所示欄位。若要使用合作夥伴為潛在客戶設定檔提供的屬性來豐富您的結構描述，您可以建立含有所要屬性的新欄位群組再加入到結構描述，也可以使用其中一個 Adobe 提供的預先設定欄位群組。

![XDM 個別潛在客戶設定檔類別的預先設定欄位](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)。

接下來，您必須選取之前建立的合作夥伴 ID 身分作為結構描述的主要身分。設定檔記錄必須帶有主要身分。此步驟是必要的，才能確保潛在客戶資料可載入設定檔存放區，並可供細分和啟用。

>[!AVAILABILITY]
>
>潛在客戶設定檔會自動限制為僅使用合作夥伴 ID 類型的 ID 命名空間。這是出於設計，可確保將您的第一方和潛在客戶設定檔清楚分開。

![選取先前設定的合作夥伴 ID 作為結構描述中的主要身分。](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

請注意，尚未為設定檔啟用結構描述。切換設定檔按鈕以啟用此結構描述以包含在設定檔服務中。如需深入了解如何啟用結構描述用於即時客戶設定檔，請閱讀[建立結構描述教學課程](/help/xdm/tutorials/create-schema-ui.md#profile)。

![啟用設定檔結構描述。](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### 將協力廠商資料治理標籤新增到結構描述的所有欄位

考慮將協力廠商資料標籤新增到組成結構描述的所有欄位。這對於確保負責任地使用協力廠商資料並將資料洩漏風險降至最低而言非常重要。尋找更多關於以下內容的資訊： [第三方資料控管標籤](../../data-governance/labels/reference.md#partner-ecosystem-labels).

請依照下列步驟執行此操作：

1. 瀏覽至您建立的結構描述並選取「**[!UICONTROL 標籤]**」索引標籤。
2. 使用最頂部的核取方塊按鈕選取此結構描述中的所有欄位，然後按一下右側的鉛筆圖示，將資料治理標籤套用到此結構描述。
3. 選取左側類別中的「**[!UICONTROL 合作夥伴生態系統]**」標籤。
4. 選擇名為&#x200B;**[!UICONTROL 協力廠商]**&#x200B;的標籤，並選取「**[!UICONTROL 儲存]**」。
5. 請注意，結構描述中的所有欄位現在都含有您在上一步驟選取的標籤。

>[!SUCCESS]
>
>您的結構描述現已可供使用，您可以繼續執行下一步驟，從資料合作夥伴擷取潛在客戶資料。

此外，在此步驟中，請考慮隨著您擴大資料管理策略以包含合作夥伴提供的協力廠商資料時，您的資料治理模式會如何變更。探索以下文件連結中的考量事項：

* (**即將推出**) 將協力廠商資料保存在單獨的資料集中，以便可輕鬆進行刪除及還原整合。
* (**即將推出**) 對於購買了資料清理附加元件的用戶端，在資料集上使用[資料集到期](/help/hygiene/ui/dataset-expiration.md)功能。
* (**即將出**) 建立引入協力廠商資料的衍生資料集時需謹慎小心，因為一旦混合在一起，若要移除協力廠商資料，唯一的解決方案是刪除整個衍生資料集。

### 載入潛在客戶設定檔清單並檢查潛在客戶設定檔檢視

準備好用於管理潛在客戶設定檔的資料模型後，就可以擷取資料了。

#### 建立資料集並載入潛在客戶資料範例

若要載入一些範例資料並填入潛在客戶設定檔，請建立資料集並上傳您從資料合作夥伴收到的檔案。完成以下步驟：

1. 瀏覽至「**[!UICONTROL 資料管理]** > **[!UICONTROL 資料集]**」並選取「**[!UICONTROL 建立資料集]**」。
2. 選取「從結構描述建立資料集」
3. 選取您在上一步驟中建立的結構描述
4. 為資料集命名，並提供說明 (非必填)。
5. 選取「**[!UICONTROL 完成]**」。

![為潛在客戶設定檔建立資料集的步驟記錄](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)。

請注意，與結構描述建立步驟類似，您需要啟用資料集以包含在即時客戶設定檔中。如需進一步了解如何啟用資料集以用於即時客戶設定檔，請閱讀[建立結構描述教學課程](/help/xdm/tutorials/create-schema-ui.md#profile)。

![啟用設定檔資料集](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)。

若要將從合作夥伴收到的檔案載入到資料集中，請選取資料集，在右邊欄向下捲動，然後選取「**[!UICONTROL 新增資料]**」。您可以拖放檔案或選取「**[!UICONTROL 選擇檔案]**」以瀏覽至檔案位置並選取檔案。

![將檔案新增到資料集](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)。

將來自資料合作夥伴的設定檔清單載入到 Real-Time CDP 後，繼續[檢查載入的潛在客戶設定檔區段](#inspect-profiles)，檢查潛在客戶設定檔是否已填入到 UI 中。

#### 透過來源連接器擷取潛在客戶資料

您可以設定並行檔案匯入，以透過來源連接器從合作夥伴擷取資料，並將潛在客戶設定檔帶入 Real-Time CDP。

下面列出了一些用於此目的之建議來源連接器，但請注意，任何用於 Real-Time CDP 的檔案型擷取方法都適合您的目的。

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

將來自資料合作夥伴的設定檔清單載入至 Real-Time CDP 後，繼續下一個區段，檢查潛在客戶設定檔是否已填入 UI 中。

#### 檢查載入的潛在客戶設定檔 {#inspect-profiles}

若要查看潛在客戶設定檔清單，請在左邊欄瀏覽至「**[!UICONTROL 潛在客戶]** > **[!UICONTROL 設定檔]**」。

請注意，剛才載入至 Real-Time CDP 的潛在客戶設定檔可能最多需要兩個小時才能顯示在「潛在客戶設定檔」畫面的「**[!UICONTROL 瀏覽]**」檢視。如果頁面顯示「目前沒有可供瀏覽的潛在客戶設定檔」訊息，請稍後再試一次。等待一段時間後，潛在客戶設定檔應該開始顯示在「**[!UICONTROL 瀏覽]**」檢視中。

>[!TIP]
>
>請注意，會出現&#x200B;**[!UICONTROL 身分命名空間]**&#x200B;欄。如果您與多個資料廠商合作，請使用此欄來推斷潛在客戶設定檔的來源。

![載入至 Real-Time CDP 之潛在客戶設定檔的檢視](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)。

您也可以選取任何潛在客戶設定檔以進一步檢查，如下所示。

![如何檢查潛在客戶設定檔的檢視](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)。

閱讀更多有關[潛在客戶設定檔](/help/profile/ui/prospect-profile.md)。

### 建立潛在客戶對象 {#create-prospect-audiences}

使用 Real-Time CDP 細分功能，從您的潛在客戶設定檔建立對象。使用所需的細分規則來建立量身打造的對象。

若要開始使用並建立由潛在客戶設定檔組成的對象，請瀏覽至「**[!UICONTROL 潛在客戶]** > **[!UICONTROL 對象]**」。

![潛在客戶對象的檢視](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)。

請注意，從潛在客戶設定檔建立對象的體驗，不同於從已知的第一方客戶建立對象的體驗。此檢視僅限於：

* 您先前建立之潛在客戶類別的屬性。
* 僅限批次設定檔評估。
* 不支援根據時間序列事件建立對象。

閱讀更多有關[潛在客戶對象](/help/segmentation/ui/prospect-audience.md)。

### 將潛在客戶設定檔啟動到目的地 {#activate-to-destinations}

透過將潛在客戶對象匯出到目的地來使用它們。目前，只有某些雲端儲存空間目的地支援啟用潛在客戶設定檔。

![支援潛在客戶對象的目的地。](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

[閱讀全文](/help/destinations/ui/activate-prospect-audiences.md) 關於啟用潛在客戶至雲端儲存空間目的地。

## 其他透過合作夥伴資料支援封存的使用案例 {#other-use-cases}

探索透過 Real-Time CDP 中的合作夥伴資料支援啟用的更多使用案例：

* [使用受信任資料合作夥伴的屬性來補充第一方設定檔，以改善您的資料基礎並對客戶群取得新的分析，而且獲致更佳的對象最佳化。](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* [使用合作夥伴協助的訪客辨識功能，為未知訪客提供個人化的現場體驗](/help/rtcdp/partner-data/onsite-personalization.md) 造訪期間，使用者未經驗證，或先前沒有您品牌的記錄。
* [擴大啟用潛在客戶個人資料和潛在客戶對象](/help/destinations/ui/activate-prospect-audiences.md)以選取目的地。
