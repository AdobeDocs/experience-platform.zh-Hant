---
title: （測試版）透過潛在客戶使用案例吸引和贏取新客戶
description: 瞭解如何透過Real-Time CDP中的合作夥伴資料支援提供的潛在使用案例來吸引和贏取新客戶。
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 486e1390dfa0602bef15d196d4a1a5befdc9ff23
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 15%

---

# 透過潛在客戶使用案例吸引和贏取新客戶

>[!AVAILABILITY]
>
>* 此 Beta 功能可供已獲得 Real-Time CDP (應用程式服務)、Adobe Experience Platform Activation、Real-time CDP、Real-Time CDP Prime、Real-Time CDP Ultimate 授權的客戶使用。如需詳細資訊，請閱讀[產品說明](https://helpx.adobe.com/legal/product-descriptions.html)中有關這些套件的詳細資料，並和您的 Adob&#x200B;&#x200B;e 代表聯絡。

使用Real-Time CDP中的第三方資料支援，透過資料合作夥伴的潛在客戶設定檔來擴展您的設定檔庫，並與他們互動以贏取或吸引新客戶。

![客戶潛在客戶使用案例高階視覺化概觀。](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## 必要條件和規劃 {#prerequisites-and-planning}

當您考慮使用Real-Time CDP中的合作夥伴資料支援來聯絡及爭取新客戶時，請在規劃程式中考慮下列必要條件：

* 您預期合作夥伴提供的設定檔會以何種步調擷取到Real-Time CDP並更新？
* 您的下游目的地需要哪些身分？
* 確保擷取的識別碼可在下游操作
* 您擷取的合作夥伴資料是否與廣泛接受的永續性識別碼連結，例如個人識別資訊(PII)、雜湊PII或合作夥伴識別碼？
* 從合作夥伴的角度以及您自己的法律、隱私權或合規團隊來看，您需要瞭解哪些資料使用原則？

## 如何實現使用案例：高層級概觀 {#achieve-the-use-case-high-level}

在您擴展Real-Time CDP以吸引和贏取新客戶之前，請務必使用Real-Time CDP為您的第一部分資料奠定堅實的基礎。 達成此使用案例的工作流程類似於與已知客戶互動的工作流程。

![客戶潛在客戶使用案例高階視覺化概觀。](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. As a **客戶**，您可從一或多個潛在客戶設定檔授予授權 **資料合作夥伴** 協助推動漏斗客戶贏取。
2. As a **客戶**，您可以擴充設定檔資料和治理模型，以擷取 **合作夥伴** — 提供的潛在客戶設定檔清單。
3. As a **客戶**，即可將潛在客戶設定檔載入到Real-Time CDP中，並建立控管政策以確保負責任地使用。
4. As a **客戶**，即可從潛在客戶設定檔清單中建立重點受眾。
5. As a **客戶**，您可將潛在客戶對象啟用至接受潛在客戶清單中可用身分的目的地。
6. 如有需要，請使用 **資料合作夥伴** 用於向所需的付費媒體目的地進行受眾的最後一哩啟動。

## 如何實現使用案例：逐步說明 {#step-by-step-instructions}

詳閱以下章節，其中包含指向更多文件的連結，以完成上述高層級概觀中的每個步驟。

### 您將使用的UI功能和元素 {#ui-functionality-and-elements}

完成實施使用案例的步驟後，您將使用以下Real-Time CDP功能和UI元素（按使用順序列出）。 請確定您擁有所有這些區域必要的屬性型存取控制許可權，或要求系統管理員授與您必要的許可權。

* [身分](/help/identity-service/namespaces.md)
* [綱要](/help/xdm/home.md)
* [資料使用標籤](/help/data-governance/labels/overview.md)
* [資料集](/help/catalog/datasets/overview.md)
* [來源](/help/sources/home.md)
* 設定檔（潛在客戶設定檔的連結）
* 對象（指向潛在客戶對象的連結）
* [目的地](/help/destinations/home.md)

### 從合作夥伴取得授權協力廠商設定檔詳細資料 {#license-profiles-from-partner}

此步驟的說明請參閱 [必備條件](#prerequisites-and-planning) 和Adobe會假設您與受信任的資料供應商有適當的合約協定，以便擷取資料合作夥伴提供的潛在客戶設定檔。

### 擴充您的設定檔資料和治理模型，以配合合作夥伴提供的潛在客戶設定檔 {#extend-governance-model}

為了準備從您的資料合作夥伴接收潛在客戶設定檔，您必須在Real-Time CDP中擴充資料管理架構，以符合這個新的設定檔型別。

您將使用的身分、資料管理和治理元件包括：

* 新 **[!UICONTROL 合作夥伴ID]** 合作夥伴提供的設定檔的身分型別
* 新 **[!UICONTROL XDM個別潛在客戶設定檔]** XDM類別
* **（檔案即將推出）** 專為合作夥伴資料支援量身打造的欄位群組
* **（檔案即將推出）** 您要在來自合作夥伴的屬性上新增的第三方標籤

#### 建立合作夥伴ID身分名稱空間

首先，請針對您將從合作夥伴收到的設定檔建立新的身分型別。 若要這麼做，您必須在「身分」段落中建立型別的新身分名稱空間 **[!UICONTROL 合作夥伴ID]**.

![建立新的合作夥伴ID身分名稱空間。](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* 若要深入瞭解合作夥伴ID名稱空間，請參閱 [身分型別段落](/help/identity-service/namespaces.md).
* 閱讀有關在 Experience Platform 使用者介面中[如何定義身分欄位](/help/xdm/ui/fields/identity.md)的資訊。

#### 使用建立新結構描述 **[!UICONTROL XDM個別潛在客戶設定檔]** 類別

下一個，在 **[!UICONTROL 資料管理]** > **[!UICONTROL 結構描述]**，建立新結構描述並為其指派 **[!UICONTROL XDM個別潛在客戶設定檔]** 類別。

![在XDM結構描述產生器中搜尋XDM個別潛在客戶設定檔類別。](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

閱讀如何 [在UI中建立和編輯結構描述](/help/xdm/ui/resources/schemas.md) 並取得有關XDM個人潛在客戶設定檔類別的完整資訊（即將推出的連結）。

此 **[!UICONTROL XDM個別潛在客戶設定檔]** 類別已預先設定下列欄位。 若要使用合作夥伴為潛在客戶設定檔提供的屬性來豐富您的結構描述，您可以使用預期的屬性來建立新的欄位群組，並將其新增到結構描述中，或者您可以使用Adobe提供的其中一個預先設定的欄位群組。

![XDM個別潛在客戶設定檔類別的預先設定欄位。](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

接下來，您必須選取您先前建立的partnerID身分識別，作為結構描述的主要身分識別。 設定檔記錄必須攜帶主要識別碼。 此步驟是必要的，以確保可將潛在客戶資料載入設定檔存放區，並可用於細分和啟動。

>[!AVAILABILITY]
>
>潛在客戶設定檔會自動限製為僅使用合作夥伴ID型別的ID名稱空間。 這是刻意設計，並確保第一方與潛在客戶設定檔之間可完全分開。

![選取先前設定的合作夥伴ID作為結構描述中的主要身分。](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

請注意，尚未為設定檔啟用此結構描述。 切換設定檔按鈕以啟用此結構描述以包含在設定檔服務中。 如需啟用結構以用於Real-Time Customer Profile的詳細資訊，請參閱 [建立結構描述教學課程。](/help/xdm/tutorials/create-schema-ui.md#profile)

![啟用設定檔結構.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### 將第三方資料控管標籤新增至結構描述中的所有欄位

請考慮將第三方資料控管標籤新增至組成結構描述的所有欄位。 這對於確保負責任地使用協力廠商資料並將資料洩漏的風險降至最低非常重要。 尋找有關第三方資料控管標籤的更多資訊（新增Jordan檔案的連結）

請依照下列步驟執行此操作：

1. 導覽至您建立的結構描述，然後選取 **[!UICONTROL 標籤]** 標籤。
2. 使用最上方的核取方塊按鈕選取此結構描述中的所有欄位，然後按一下右側的鉛筆圖示以將資料控管標籤套用至此結構描述。
3. 選取 **[!UICONTROL 合作夥伴生態系統]** 從左側的類別加上標籤。
4. 選擇名為的標籤 **[!UICONTROL 協力廠商]** 並選取 **[!UICONTROL 儲存]**.
5. 請注意，結構描述中的所有欄位現在都帶有您在上一步驟中選擇的標籤。

>[!SUCCESS]
>
>您的結構描述現在已可供使用，您可以繼續進行下一個步驟，從您的資料合作夥伴擷取潛在客戶資料。

此外，在此步驟中，請考慮隨著您擴大資料管理策略以包含合作夥伴提供的協力廠商資料時，您的資料治理模式會如何變更。探索以下文件連結中的考量事項：

* (**即將推出**) 將協力廠商資料保存在單獨的資料集中，以便可輕鬆進行刪除及還原整合。
* (**即將推出**) 對於購買了資料清理附加元件的用戶端，在資料集上使用[資料集到期](/help/hygiene/ui/dataset-expiration.md)功能。
* (**即將出**) 建立引入協力廠商資料的衍生資料集時需謹慎小心，因為一旦混合在一起，若要移除協力廠商資料，唯一的解決方案是刪除整個衍生資料集。

### 載入潛在客戶設定檔清單並檢查潛在客戶設定檔檢視

在您準備好資料模型以管理潛在客戶設定檔後，就可以開始擷取資料了。

#### 建立資料集並載入範例潛在客戶資料

若要載入一些範例資料並填入潛在客戶設定檔，請建立資料集並上傳您從資料合作夥伴收到的檔案。 完成下列步驟：

1. 導覽至 **[!UICONTROL 資料管理]** > **[!UICONTROL 資料集]** 並選取 **[!UICONTROL 建立資料集]**.
2. 選取從結構描述建立資料集
3. 選取您在上一步建立的綱要
4. 為資料集命名並選擇性地提供說明。
5. 選取&#x200B;**[!UICONTROL 「完成」]**。

![為潛在客戶設定檔建立資料集的步驟記錄。](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

請注意，與建立結構的步驟類似，您需要啟用資料集以包含在即時客戶個人檔案中。 如需啟用資料集以用於即時客戶個人檔案的詳細資訊，請參閱 [建立結構描述教學課程。](/help/xdm/tutorials/create-schema-ui.md#profile)

![為設定檔啟用資料集。](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

若要將您從合作夥伴收到的檔案載入資料集，請選取資料集，向下捲動右側邊欄，然後選取 **[!UICONTROL 新增資料]**. 您可以拖放檔案或選取 **[!UICONTROL 選擇檔案]** 以瀏覽至檔案位置並加以選取。

![將檔案新增至資料集。](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

將資料合作夥伴的設定檔清單載入Real-Time CDP後，請繼續前往 [Inspect已載入的潛在客戶設定檔區段](#inspect-profiles) 檢查潛在客戶設定檔是否填入UI中。

#### 透過來源聯結器內嵌潛在客戶資料

您可以設定週期性檔案匯入，以透過來源聯結器從合作夥伴擷取資料，並將潛在客戶設定檔清單帶入Real-Time CDP。

以下是一些為此目的而建議的來源聯結器，但請注意，任何將檔案型擷取方法引入Real-Time CDP均符合您的用途。

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

從資料合作夥伴將設定檔清單載入Real-Time CDP後，請繼續下一節以檢查潛在客戶設定檔是否正在UI中填入。

#### Inspect載入的潛在客戶設定檔 {#inspect-profiles}

若要檢視潛在客戶設定檔清單，請導覽至 **[!UICONTROL 潛在客戶]** > **[!UICONTROL 設定檔]** 在左側邊欄中。

請注意，您剛才載入Real-Time CDP的潛在客戶設定檔可能需要長達兩個小時才能顯示在中 **[!UICONTROL 瀏覽]** 潛在客戶設定檔畫面檢視。 如果頁面顯示「目前沒有可瀏覽的潛在客戶設定檔」訊息，請稍後再試。 等待一段時間後，潛在客戶設定檔應開始顯示在 **[!UICONTROL 瀏覽]** 檢視。

>[!TIP]
>
>記下是否存在 **[!UICONTROL 身分名稱空間]** 欄。 如果您與多個資料廠商合作，請使用此欄來推斷潛在客戶設定檔的來源。

![載入Real-Time CDP中的潛在客戶設定檔檢視。](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

您也可以選取任何潛在客戶設定檔以進行進一步檢查，如下所示。

![如何檢查潛在客戶設定檔的檢視。](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

(**即將推出**)進一步瞭解潛在客戶設定檔。

### 建立潛在客戶對象 {#create-prospect-audiences}

使用Real-Time CDP中的細分功能，從您的潛在客戶設定檔建立對象。 使用所需的細分規則來建立量身打造的對象。

若要開始使用並建立由潛在客戶設定檔組成的對象，請導覽至 **[!UICONTROL 潛在客戶]** > **[!UICONTROL 受眾]**.

![潛在客戶受眾的檢視。](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

請注意，潛在客戶設定檔的對象建立體驗與從您已知的第一方客戶建立對象的體驗不同。 此檢視僅限於：

* 您先前建立之潛在客戶類別的屬性。
* 僅批次設定檔評估。
* 不支援根據時間序列事件建立對象。

(**即將推出**)進一步瞭解潛在客戶對象。

### 對目的地啟用潛在客戶設定檔 {#activate-to-destinations}

將潛在客戶對象匯出至目的地，以利用這些受眾。 目前，只有特定目的地(例如 [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) 或 [!BADGE Alpha]{type=Informative}[LiveRamp](/help/destinations/catalog/advertising/liveramp.md) 目的地支援啟動潛在客戶設定檔。

## 其他透過合作夥伴資料支援封存的使用案例 {#other-use-cases}

探索透過 Real-Time CDP 中的合作夥伴資料支援啟用的更多使用案例：

* [!BADGE Beta]{type=Informative}[使用受信任資料合作夥伴的屬性來補充第一方設定檔，以改善您的資料基礎並對客戶群取得新的分析，而且獲致更佳的對象最佳化。](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* (**即將推出**) [!BADGE Beta]{type=Informative}**利用合作夥伴輔助識別**，不需要使用者驗證或之前使用您的品牌的紀錄，即可在造訪期間提供個人化的現場體驗並在造訪後進行場外重定位。