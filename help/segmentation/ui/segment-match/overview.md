---
keywords: Experience Platform；首頁；熱門主題；分段；分段；段匹配；段匹配
solution: Experience Platform
title: 段匹配概述
description: 段匹配是Adobe Experience Platform的段共用服務，允許兩個或兩個以上平台用戶以安全、受管理和隱私友好的方式交換段資料。
exl-id: 4e6ec2e0-035a-46f4-b171-afb777c14850
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1997'
ht-degree: 2%

---

# [!DNL Segment Match] 概覽

Adobe Experience Platform網段匹配是一種網段共用服務，允許兩個或兩個以上平台用戶以安全、受管理和隱私友好的方式交換網段資料。 [!DNL Segment Match] 使用平台隱私標準和個人標識符，如散列電子郵件、散列電話號碼和設備標識符，如IDFA和GAID。

與 [!DNL Segment Match] 您可以：

* 管理身份重疊進程。
* 查看股份前估計。
* 應用資料使用標籤，以控制是否可以與合作夥伴共用資料。
* 在發佈源後維護共用的受眾生命週期管理，並通過添加、刪除和取消共用的功能繼續動態交換資料。

[!DNL Segment Match] 使用身份重疊過程確保以安全且注重隱私的方式進行段共用。 安 **重疊身份** 是在您的網段和所選合作夥伴的網段中具有匹配項的標識。 在發送方和接收方之間共用段之前，標識重疊過程檢查命名空間中的重疊以及發送方和接收方之間的同意檢查。 要共用段，必須通過兩個重疊檢查。

以下各節提供了有關 [!DNL Segment Match]，包括有關設定及其端到端工作流的詳細資訊。

## 設定

以下各節概述了如何設定和配置 [!DNL Segment Match]:

### 設定標識資料和命名空間 {#namespaces}

開始的第一步 [!DNL Segment Match] 是為了確保正在根據支援的標識命名空間接收資料。

標識命名空間是 [Adobe Experience Platform身份服務](../../../identity-service/home.md)。 每個客戶標識都包含指示標識上下文的關聯命名空間。 例如，命名空間可以區分「name」的值<span>@email.com」作為電子郵件地址，或「443522」作為數字CRM ID。

完全限定的標識包括ID值和命名空間。 在配置檔案段之間匹配記錄資料時(例如 [!DNL Real-Time Customer Profile] 合併配置檔案資料)，標識值和命名空間必須匹配。

在 [!DNL Segment Match]，共用資料時在重疊過程中使用命名空間。

支援的命名空間清單如下所示：

| 命名空間 | 說明 |
| --------- | ----------- |
| 電子郵件（SHA256，小寫） | 預散列電子郵件地址的命名空間。 在使用SHA256散列之前，此命名空間中提供的值將轉換為小寫。 在對電子郵件地址進行規範化之前，需要裁剪前導空格和尾隨空格。 無法追溯更改此設定。 平台提供了兩種方法，通過 [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) 通過 [資料準備](../../../data-prep/functions.md#hashing)。 |
| 電話(SHA256_E.164) | 表示需要使用SHA256和E.164格式散列的原始電話號碼的命名空間。 |
| ECID | 表示Experience CloudID(ECID)值的命名空間。 以下別名也可以引用此命名空間：&quot;Adobe Marketing CloudID&quot;,&quot;Adobe Experience CloudID&quot;,&quot;Adobe Experience PlatformID&quot; 查看 [ECID概述](../../../identity-service/ecid.md) 的子菜單。 |
| AppleIDFA（廣告商ID） | 表示廣告商的AppleID的命名空間。 請參閱以下文檔 [基於興趣的廣告](https://support.apple.com/en-us/HT202074) 的子菜單。 |
| Google廣告ID | 表示Google廣告ID的命名空間。 請參閱以下文檔 [Google廣告ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) 的子菜單。 |

### 設定同意配置

必須提供同意配置並將其預設值設定為 `opt-in` 或 `opt-out` 以便進行同意檢查。

「選擇加入」和「選擇退出」許可檢查決定您是否可以在預設情況下在同意共用用戶資料的情況下進行操作。 如果同意配置預設值設定為 `opt-out`，則可以共用用戶資料，除非用戶明確選擇。 如果預設值設定為 `opt-in`，則無法共用用戶資料，除非用戶明確選擇。

的預設同意配置 [!DNL Segment Match] 設定為 `opt-out`。 要強制您的資料選擇加入模型，請向您的Adobe帳戶團隊發送電子郵件請求。

有關 `share` 用於設定資料共用同意值的屬性，請參閱以下文檔 [隱私和同意欄位組](../../../xdm/field-groups/profile/consents.md)。 有關特定欄位組的資訊，請參閱以下內容：收集和使用與隱私、個性化和市場營銷首選項相關的資料時，用於獲取消費者同意 [隱私、個性化和市場營銷首選項的同意示例GitHub](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md)。

### 配置資料使用標籤

您必須建立的最後一個先決條件是配置新的資料使用標籤以防止資料共用。 通過資料使用標籤，您可以管理允許通過以下方式共用的資料 [!DNL Segment Match]。

資料使用情況標籤允許您根據應用於該資料的使用情況策略對資料集和欄位進行分類。 標籤可以隨時應用，在選擇管理資料的方式上提供了靈活性。 最佳做法鼓勵在資料被引入Experience Platform或資料在平台中可用時立即標籤資料。

[!DNL Segment Match] 使用C11標籤，該標籤是特定於 [!DNL Segment Match] 可以手動添加到任何資料集或屬性，以確保它們被排除在 [!DNL Segment Match] 合作夥伴共用過程。 C11標籤表示不應用於 [!DNL Segment Match] 進程。 確定要從中排除的資料集和/或欄位後 [!DNL Segment Match] 並相應地添加C11標籤，標籤由 [!DNL Segment Match] 工作流。 [!DNL Segment Match] 自動啟用 [!UICONTROL 限制資料共用] 核心政策。 有關如何將資料使用標籤應用到資料集的特定說明，請參見上的教程 [管理UI中的資料使用標籤](../../../data-governance/labels/user-guide.md)。

有關資料使用標籤及其定義的清單，請參見 [資料使用標籤](../../../data-governance/labels/reference.md)。 有關資料使用策略的資訊，請參見 [資料使用策略概述](../../../data-governance/policies/overview.md)。

### 理解 [!DNL Segment Match] 權限

有兩個權限與 [!DNL Segment Match]:

| 權限 | 說明 |
| --- | --- |
| 管理受眾共用連接 | 此權限允許您完成合作夥伴握手過程，該過程將連接兩個組織以啟用 [!DNL Segment Match] 流。 |
| 管理受眾共用 | 此權限允許您建立、編輯和發佈源(用於 [!DNL Segment Match])與活動合作夥伴(管理員用戶已與 **[!UICONTROL 受眾共用連接]** 訪問)。 |

查看 [訪問控制概述](../../../access-control/home.md) 的子菜單。

## [!DNL Segment Match] 端到端工作流

設定身份資料和命名空間、同意配置和資料使用標籤後，可以開始使用 [!DNL Segment Match] 以及它的特點。

### 管理合作夥伴

在平台UI中，選擇 **[!UICONTROL 段]** 從左導航，然後選擇 **[!UICONTROL 源]** 的下界。

![段饋送.png](./images/segments-feed.png)

的 [!UICONTROL 源] 頁面包含從合作夥伴接收的源以及您共用的源的清單。 要查看現有合作夥伴的清單或與新合作夥伴建立連接，請選擇 **[!UICONTROL 管理合作夥伴]**。

![manage-partners.png](./images/manage-partners.png)

兩個合作夥伴之間的連接是一種「雙向握手」，它充當用戶在沙盒級別將其平台組織連接在一起的自助服務方法。 需要建立連接，才能通知平台已經簽訂了協定，平台可以方便您與合作夥伴共用服務。

>[!NOTE]
>
>你和你的伴侶之間的「雙向握手」，嚴格來說就是一種聯繫。 在此過程中未交換任何資料。

您可以在的主介面中查看與現有合作夥伴的連接清單 [!UICONTROL 管理合作夥伴] 的上界。 在右欄上 [!UICONTROL 共用設定] 面板，它提供了生成新的 [!UICONTROL 連接ID] 以及輸入框 [!UICONTROL 連接ID]。

![建立連接.png](./images/establish-connection.png)

建立新 [!UICONTROL 連接ID]選中 **[!UICONTROL 再生]** 在 [!UICONTROL 共用設定] ，然後選擇新生成的ID旁邊的複製表徵圖。

![共用設定.png](./images/share-setting.png)

使用其 [!UICONTROL 連接ID]，在輸入框中輸入其唯一ID值 [!UICONTROL 連接合作夥伴] ，然後選擇 **[!UICONTROL 請求]**。

![connect partner.png](./images/connect-partner.png)

### 建立源 {#create-feed}

>[!CONTEXTUALHELP]
>id="platform_segment_match_marketing"
>title="受限制的行銷使用案例"
>abstract="受限制的行銷使用案例有助於為您的合作夥伴提供指引，以確保根據您的資料控管限制正確使用共用的區段。"
>text="Learn more in documentation"

A **飼料** 是一組資料（段）、資料如何公開或使用的規則，以及確定資料與合作夥伴資料匹配方式的配置。 源可以獨立管理，並可通過以下方式與其他平台用戶交換 [!DNL Segment Match]。

要建立新源，請選擇 **[!UICONTROL 建立源]** 從 [!UICONTROL 源] 控制項欄。

![create.feed.png](./images/create-feed.png)

源的基本設定包括有關市場營銷使用案例和身份設定的名稱、描述和配置。 提供訂閱源的名稱和說明，然後應用希望將資料排除在市場營銷使用案例之外。 您可以從包括以下內容的清單中選擇多個使用案例：

* [!UICONTROL Analytics]
* [!UICONTROL 與PII結合]
* [!UICONTROL 跨站點目標]
* [!UICONTROL 資料科學]
* [!UICONTROL 電子郵件目標]
* [!UICONTROL 出口給第三方]
* [!UICONTROL 現場廣告]
* [!UICONTROL 現場個性化]
* [!UICONTROL 段匹配]
* [!UICONTROL 單一身份個性化]

最後，為源選擇適當的標識命名空間。 有關支援的特定命名空間的資訊 [!DNL Segment Match]，請參見 [標識資料和命名空間表](#namespaces)。 完成後，選擇 **[!UICONTROL 下一個]**。

![觀眾共用.png](./images/audience-sharing.png)

建立源設定後，從第一方段清單中選擇要共用的段。 您可以從清單中選擇多個段，並可以使用右滑軌管理選定段的清單。 完成後，選擇 **[!UICONTROL 下一個]**。

![select-segments.png](./images/select-segments.png)

的 [!UICONTROL 共用] 的子菜單。 在此步驟中，您還可以查看共用前重疊估計報告，並查看您與合作夥伴之間按命名空間劃分的重疊標識數，以及同意共用資料的重疊標識數。

選擇 **[!UICONTROL 按段分析]** 查看估計報告。

![analyze.png](./images/analyze.png)

重疊估計報告允許您在共用源之前管理每個合作夥伴和每個段的重疊和同意檢查。

| 量度 | 說明 |
| ------- | ----------- |
| 經同意的估計身份 | 符合為您的組織配置的同意要求的重疊身份總數。 |
| 估計的重疊恆等式 | 符合選定段資格且與選定夥伴匹配的標識數。 這些標識按命名空間顯示，不表示單個配置檔案標識。 重疊估計基於輪廓草繪。 |

完成後，選擇 **[!UICONTROL 關閉]**。

![重疊報表.png](./images/overlap-report.png)

選擇合作夥伴並查看重疊估計報告後，選擇 **[!UICONTROL 下一個]** 繼續。

![共用.png](./images/share.png)

的 [!UICONTROL 審閱] 步驟，允許您在共用和發佈新源之前查看新源。 此步驟包括您所應用的身份設定的詳細資訊，以及您選擇的市場營銷使用案例、細分市場和合作夥伴的資訊。

選擇 **[!UICONTROL 完成]** 繼續。

![review.png](./images/review.png)

### 更新源

要添加或刪除段，請選擇 **[!UICONTROL 建立源]** 從 [!UICONTROL 源] ，然後選擇 **[!UICONTROL 現有源]**。 在顯示的現有源清單中，選擇要更新的源，然後選擇 **[!UICONTROL 下一個]**。

![源清單](./images/feed-list.png)

此時將顯示段清單。 在此處，您可以向源中添加新段，並可以使用右滑軌移除不再需要的任何段。 完成源中段的管理後，選擇 **[!UICONTROL 下一個]** 然後按照上述步驟完成更新的源。

![update](./images/update.png)

>[!NOTE]
>
>當您從共用源添加或刪除段時，接收夥伴必須通過重新啟用 [!DNL Profile] 切換其已接收源清單。

### 接受傳入的源

要查看傳入的源，請選擇 **[!UICONTROL 已接收]** 的 [!UICONTROL 源] 頁面，然後從清單中選擇要查看的源。 要接受進紙，請選擇 **[!UICONTROL 啟用配置檔案]** 並允許稍後更新狀態 [!UICONTROL 待定] 至 [!UICONTROL 已啟用]。

![received.png](./images/received.png)

接受共用源後，可以開始使用共用資料構建新段。

## 後續步驟

通過閱讀此文檔，您瞭解 [!DNL Segment Match]功能，端對端工作流。 請參閱以下文檔，以瞭解有關其他平台服務的詳細資訊：

* [[!DNL Segmentation Service]](../../home.md)
* [[!DNL Identity Service]](../../../identity-service/home.md)
* [[!DNL Real-Time Customer Profile] 概覽](../../../profile/home.md)
