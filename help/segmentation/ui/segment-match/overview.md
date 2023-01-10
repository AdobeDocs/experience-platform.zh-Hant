---
keywords: Experience Platform；首頁；熱門主題；分段；分段符合；區段符合
solution: Experience Platform
title: 區段符合概述
description: 區段比對是Adobe Experience Platform中的區段共用服務，可讓兩位或多位Platform使用者以安全、受控且符合隱私權的方式來交換區段資料。
exl-id: 4e6ec2e0-035a-46f4-b171-afb777c14850
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1998'
ht-degree: 0%

---

# [!DNL Segment Match] 概覽

Adobe Experience Platform區段比對是區段共用服務，可讓兩位或多位Platform使用者以安全、受控且符合隱私權的方式交換區段資料。 [!DNL Segment Match] 使用平台隱私標準和個人識別碼，例如雜湊電子郵件、雜湊電話號碼，以及IDFA和GAID等裝置識別碼。

使用 [!DNL Segment Match] 您可以：

* 管理身分重疊程式。
* 檢視預先共用估計。
* 套用資料使用量標籤，以控制是否可與合作夥伴共用資料。
* 在發佈摘要後維護共用的受眾生命週期管理，並透過新增、刪除和取消共用的功能繼續進行資料的動態交換。

[!DNL Segment Match] 使用身分重疊程式，確保以安全且以隱私權為中心的方式共用區段。 安 **重疊身份** 是您區段和所選合作夥伴區段中均相符的身分。 在傳送者與接收者之間共用區段之前，身分重疊程式會檢查命名空間中的重疊，以及傳送者與接收者之間的同意檢查。 必須傳遞兩個重疊檢查才能共用區段。

以下各節提供關於 [!DNL Segment Match]，包括設定及其端對端工作流程的詳細資訊。

## 設定

以下各節將概述如何設定和配置 [!DNL Segment Match]:

### 設定身分資料和命名空間 {#namespaces}

開始使用的第一步 [!DNL Segment Match] 是為了確保您會根據支援的身分識別命名空間擷取資料。

身分識別命名空間是 [Adobe Experience Platform Identity Service](../../../identity-service/home.md). 每個客戶身分識別都包含指出身分識別內容的相關命名空間。 例如，命名空間可以區分「name」的值<span>@email.com」作為電子郵件地址，或「443522」作為數值CRM ID。

完全限定的身分包括ID值和命名空間。 在設定檔片段間比對記錄資料時(例如 [!DNL Real-Time Customer Profile] 合併設定檔資料)，身分值和命名空間必須相符。

在 [!DNL Segment Match]，共用資料時，會在重疊程式中使用命名空間。

支援的命名空間清單如下：

| 命名空間 | 說明 |
| --------- | ----------- |
| 電子郵件（SHA256，小寫） | 預先雜湊電子郵件地址的命名空間。 此命名空間中提供的值在以SHA256進行雜湊處理前會轉換為小寫。 在標準化電子郵件地址之前，需要先裁剪開頭和結尾空格。 無法回溯變更此設定。 Platform提供兩種方法，可支援透過 [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) 和 [資料準備](../../../data-prep/functions.md#hashing). |
| 電話(SHA256_E.164) | 表示需要同時使用SHA256和E.164格式雜湊的原始電話號碼的命名空間。 |
| ECID | 代表Experience CloudID(ECID)值的命名空間。 此命名空間也可由下列別名引用：&quot;Adobe Marketing Cloud ID&quot;、&quot;Adobe Experience Cloud ID&quot;、&quot;Adobe Experience Platform ID&quot;。 請參閱 [ECID概觀](../../../identity-service/ecid.md) 以取得更多資訊。 |
| Apple IDFA（廣告商的ID） | 代表廣告商Apple ID的命名空間。 請參閱下列檔案，內容如下 [興趣型廣告](https://support.apple.com/en-us/HT202074) 以取得更多資訊。 |
| Google廣告ID | 代表Google Advertising ID的命名空間。 請參閱下列檔案，內容如下 [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) 以取得更多資訊。 |

### 設定同意設定

您必須提供同意設定，並將其預設值設為 `opt-in` 或 `opt-out` 進行同意檢查。

選擇加入和選擇退出同意檢查會決定您是否可以以同意的方式操作，以依預設共用使用者資料。 如果同意設定預設設為 `opt-out`，則可共用使用者資料，除非使用者明確選擇退出。 如果預設值設為 `opt-in`，則無法共用使用者資料，除非使用者明確選擇加入。

的預設同意設定 [!DNL Segment Match] 設為 `opt-out`. 若要對您的資料強制執行選擇加入模型，請傳送電子郵件要求給您的Adobe客戶經理。

如需 `share` 用於設定資料共用同意值的屬性，請參閱下列檔案，位於 [隱私權與同意欄位群組](../../../xdm/field-groups/profile/consents.md). 如需用於擷取消費者同意以收集和使用與隱私權、個人化和行銷偏好設定相關資料之特定欄位群組的資訊，請參閱下列內容 [隱私權、個人化和行銷偏好設定的同意GitHub範例](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### 設定資料使用量標籤

您必須建立的最後一個先決條件是設定新的資料使用量標籤，以防止資料共用。 透過資料使用量標籤，您可以管理哪些資料可透過 [!DNL Segment Match].

資料使用量標籤可讓您根據套用至該資料的使用量原則，對資料集和欄位進行分類。 標籤可隨時套用，提供您選擇控管資料的彈性。 最佳實務鼓勵在資料內嵌至Experience Platform時，或資料可供Platform使用時，立即加上標籤。

[!DNL Segment Match] 使用C11標籤，此標籤是 [!DNL Segment Match] 可手動新增至任何資料集或屬性，以確保系統不會將其排除在 [!DNL Segment Match] 合作夥伴分享程式。 C11標籤表示不應在 [!DNL Segment Match] 程式。 決定要排除的資料集和/或欄位後 [!DNL Segment Match] 並據此新增C11標籤，標籤便會由 [!DNL Segment Match] 工作流程。 [!DNL Segment Match] 自動啟用 [!UICONTROL 限制資料共用] 核心政策。 如需如何將資料使用量標籤套用至資料集的特定指示，請參閱以下主題的教學課程： [在UI中管理資料使用量標籤](../../../data-governance/labels/user-guide.md).

如需資料使用量標籤及其定義的清單，請參閱 [資料使用標籤字彙表](../../../data-governance/labels/reference.md). 如需資料使用原則的資訊，請參閱 [資料使用原則概觀](../../../data-governance/policies/overview.md).

### 了解 [!DNL Segment Match] 權限

有兩個權限與 [!DNL Segment Match]:

| 權限 | 說明 |
| --- | --- |
| 管理對象共用連線 | 此權限可讓您完成合作夥伴交握程式，此程式會連接兩個IMS組織以啟用 [!DNL Segment Match] 流量。 |
| 管理受眾分享 | 此權限可讓您建立、編輯和發佈摘要（用於的資料套件） [!DNL Segment Match])與活躍合作夥伴(管理員使用者已與 **[!UICONTROL 對象共用連線]** 存取)。 |

請參閱 [存取控制概觀](../../../access-control/home.md) 以取得存取控制和權限的詳細資訊。

## [!DNL Segment Match] 端對端工作流程

設定身分資料和命名空間、同意設定和資料使用標籤後，您就可以開始使用 [!DNL Segment Match] 以及它的特點。

### 管理合作夥伴

在平台UI中，選取 **[!UICONTROL 區段]** 從左側導覽中，然後選取 **[!UICONTROL 動態消息]** 從頂端標題。

![segments-feed.png](./images/segments-feed.png)

此 [!UICONTROL 動態消息] 頁面包含從合作夥伴收到的摘要清單，以及您已共用的摘要。 要查看現有合作夥伴的清單或與新合作夥伴建立連接，請選擇 **[!UICONTROL 管理合作夥伴]**.

![manage-partners.png](./images/manage-partners.png)

兩個合作夥伴之間的連線是「雙向交握」，可做為使用者在沙箱層級將其Platform組織連結在一起的自助方法。 需要連線，才能通知Platform已建立合約，且Platform可協助您與合作夥伴共用服務。

>[!NOTE]
>
>你和你的伴侶之間的「雙向握手」嚴格說來就是一種聯繫。 此過程中不會交換任何資料。

您可以在的主介面中檢視與現有合作夥伴的連線清單 [!UICONTROL 管理合作夥伴] 螢幕。 在右側邊欄上， [!UICONTROL 共用設定] 面板，此面板提供產生新 [!UICONTROL connect ID] 以及輸入方塊，您可在其中輸入合作夥伴 [!UICONTROL connect ID].

![suteling-connection.png](./images/establish-connection.png)

建立新 [!UICONTROL connect ID]，選取 **[!UICONTROL 重新產生]** 在 [!UICONTROL 共用設定] 然後選取新產生ID旁的復製圖示。

![share-setting.png](./images/share-setting.png)

使用 [!UICONTROL connect ID]，請在下方的輸入方塊中輸入其唯一ID值 [!UICONTROL 連接合作夥伴] 然後選取 **[!UICONTROL 要求]**.

![connect-partner.png](./images/connect-partner.png)

### 建立摘要 {#create-feed}

>[!CONTEXTUALHELP]
>id="platform_segment_match_marketing"
>title="限制的行銷使用案例"
>abstract="受限的行銷使用案例可協助您的合作夥伴提供指引，確保依照您的資料控管限制正確使用共用區段。"
>text="Learn more in documentation"

A **摘要** 是資料（區段）的分組、資料公開或使用方式的規則，以及決定資料與合作夥伴資料相符之方式的設定。 摘要可以獨立管理，並透過與其他Platform使用者交換 [!DNL Segment Match].

若要建立新摘要，請選取 **[!UICONTROL 建立摘要]** 從 [!UICONTROL 動態消息] 控制面板。

![create-feed.png](./images/create-feed.png)

摘要的基本設定包含有關行銷使用案例和身分設定的名稱、說明和設定。 提供摘要的名稱和說明，然後套用您希望排除資料的行銷使用案例。 您可以從清單中選取多個使用案例，其中包括：

* [!UICONTROL Analytics]
* [!UICONTROL 與PII結合]
* [!UICONTROL 跨網站定位]
* [!UICONTROL 資料科學]
* [!UICONTROL 電子郵件目標定位]
* [!UICONTROL 匯出至第三方]
* [!UICONTROL 站上廣告]
* [!UICONTROL 站上個人化]
* [!UICONTROL 區段符合]
* [!UICONTROL 單一身分個人化]

最後，為您的摘要選取適當的身分識別命名空間。 如需支援的特定命名空間相關資訊 [!DNL Segment Match]，請參閱 [身分資料和命名空間表格](#namespaces). 完成後，請選取 **[!UICONTROL 下一個]**.

![audience-sharing.png](./images/audience-sharing.png)

建立摘要的設定後，從第一方區段清單中選取您要共用的區段。 您可以從清單中選取多個區段，並可使用右側邊欄來管理所選區段的清單。 完成後，請選取 **[!UICONTROL 下一個]**.

![select-segments.png](./images/select-segments.png)

此 [!UICONTROL 共用] 頁面，提供您選取要與其共用摘要的合作夥伴的介面。 在此步驟中，您也可以檢視預先共用重疊估計報表，並依您與合作夥伴之間的命名空間查看重疊身分的數量，以及同意共用資料的重疊身分數。

選擇 **[!UICONTROL 依區段分析]** 來查看估計報告。

![analyze.png](./images/analyze.png)

重疊估計報表可讓您在共用摘要前，管理每個合作夥伴和每個區段的重疊和同意檢查。

| 量度 | 說明 |
| ------- | ----------- |
| 經同意的預估身分 | 符合貴組織所設定同意要求的重疊身分總數。 |
| 估計的重疊身份 | 符合所選區段資格且與所選合作夥伴相符的身分數。 這些身分識別會依命名空間顯示，不代表個別設定檔身分識別。 重疊估計基於配置檔案草圖。 |

完成後，請選取 **[!UICONTROL 關閉]**.

![overlap-report.png](./images/overlap-report.png)

在您選取合作夥伴並檢視重疊估計報表後，請選取 **[!UICONTROL 下一個]** 繼續。

![share.png](./images/share.png)

此 [!UICONTROL 檢閱] 步驟，可讓您在共用和發佈新摘要之前先加以檢閱。 此步驟包含您所套用之身分設定的詳細資訊，以及您所選行銷使用案例、區段和合作夥伴的相關資訊。

選擇 **[!UICONTROL 完成]** 繼續。

![review.png](./images/review.png)

### 更新摘要

若要新增或移除區段，請選取 **[!UICONTROL 建立摘要]** 從 [!UICONTROL 動態消息] 頁面，然後選取 **[!UICONTROL 現有摘要]**. 在顯示的現有摘要清單中，選取您要更新的摘要，然後選取 **[!UICONTROL 下一個]**.

![摘要清單](./images/feed-list.png)

區段清單隨即顯示。 從這裡，您可以新增區段至動態消息，也可以使用右側邊欄來移除您不再需要的任何區段。 在您完成摘要中的區段管理後，請選取 **[!UICONTROL 下一個]** 然後依照上述步驟完成更新的摘要。

![更新](./images/update.png)

>[!NOTE]
>
>當您從共用摘要新增或移除區段時，接收合作夥伴必須重新啟用 [!DNL Profile] 切換其收到摘要的清單。

### 接受傳入的摘要

若要檢視傳入的摘要，請選取 **[!UICONTROL 已接收]** 從 [!UICONTROL 動態消息] 頁面，然後從清單中選取您要檢視的摘要。 若要接受摘要，請選取 **[!UICONTROL 啟用設定檔]** 並讓狀態在數分鐘內更新 [!UICONTROL 待定] to [!UICONTROL 已啟用].

![received.png](./images/received.png)

接受共用摘要後，您就可以開始使用共用資料來建立新區段。

## 後續步驟

通過閱讀本檔案，您對 [!DNL Segment Match]、功能及端對端工作流程。 請參閱下列檔案，深入了解其他Platform服務：

* [[!DNL Segmentation Service]](../../home.md)
* [[!DNL Identity Service]](../../../identity-service/home.md)
* [[!DNL Real-Time Customer Profile] 概覽](../../../profile/home.md)
