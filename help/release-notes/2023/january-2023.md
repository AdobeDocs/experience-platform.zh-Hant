---
title: Adobe Experience Platform發行說明2023年1月
description: 2023年1月為Adobe Experience Platform發佈的說明。
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 1 月 25 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [保證](#assurance)
- [資料收集](#data-collection)
- [[!DNL Destinations]](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [即時客戶設定檔](#profile)
- [細分服務](#segmentation)
- [來源](#sources)

## 人工智慧/機器學習服務 {#ai-ml}

人工智慧和機器學習服務使營銷分析員和從業人員能夠利用AI/ML在客戶體驗使用案例中的威力。 這使市場營銷分析員能夠設定預測，而無需資料科學專業知識，而只需使用業務級配置來滿足公司的需求。

### Attribution AI

Attribution AI用於將積分屬性為觸點，從而導致轉換事件。 行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

**已更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| HIPAA 整備程度 | Healthcare Shield客戶現在可以在Attribution AI和某些其他基於Experience Platform的應用程式中接收、使用、維護或傳輸受保護的健康資訊。 Healthcare Shield適用於HIPAA中涵蓋的實體或業務夥伴的醫療保健客戶。 有關詳細資訊，請閱讀 [HIPAA和Adobe產品與服務](https://www.adobe.com/tw/trust/compliance/hipaa-ready.html) |
| 編輯其他分數資料集列 | 現在，在編輯現有模型時，可以添加或刪除其他分數資料集列（報告列）。 這擴展了歸因分數的靈活性，使您在建立模型後能夠對其他維進行洞察。 查看 [屬性UI指南](../../intelligent-services/attribution-ai/user-guide.md) 來瞭解更多資訊。 |

{style="table-layout:auto"}

請參閱 [AI/ML服務](../../intelligent-services/attribution-ai/overview.md) 概述。

### 客戶AI

Real-time Customer Data Platform的客戶AI用於生成定制傾向得分，例如按比例為單個配置檔案生成流失和轉換。 不必將企業需求轉換為機器學習問題、挑選演算法、培訓或部署，就能達成上述目的。

**已更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| HIPAA 整備程度 | Healthcare Shield客戶現在可以在客戶AI中接收、使用、維護或傳輸針對Real-time Customer Data Platform和某些其他基於Experience Platform的應用程式的受保護的健康資訊。 Healthcare Shield適用於HIPAA中涵蓋的實體或業務夥伴的醫療保健客戶。 有關詳細資訊，請參閱 [HIPAA和Adobe產品與服務](https://www.adobe.com/tw/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

請參閱 [AI/ML服務](../../intelligent-services/customer-ai/overview.md) 概述。

## 保證 {#assurance}

Adobe保障允許您檢查、驗證、模擬和驗證如何在移動應用中收集資料或提供體驗。

**新增或更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 驗證編輯器 | 對驗證編輯器添加了新的增強功能。 這些增強包括驗證列、新的代碼生成工具和改進的視圖。 |

{style="table-layout:auto"}

有關Assurance的詳細資訊，請閱讀 [保證文檔](https://developer.adobe.com/client-sdks/documentation/platform-assurance/)。

## 資料收集 {#data-collection}

Adobe Experience Platform公司提供了一套技術，使您能夠收集客戶端客戶體驗資料並將其發送到Adobe Experience Platform邊緣網路，在該網路中，資料可以得到豐富、轉換並分發到Adobe或非Adobe目的地。

**新增或更新的功能**

| 功能 | 說明 |
| --- | --- |
| 新建主螢幕 | 資料收集UI的首頁已更新，以包含有助於提高工作效率的入門資訊和連結。 其中包括:<ol><li>要開始的文檔和建議的工作流</li><li>最近的屬性、規則和資料元素</li><li>常用擴展</li><li>具有快速安裝功能的新擴展更新</li></ol> |
| 將資料發送到 [!DNL Google Ads] 使用事件轉發 | 您現在可以使用 [[!DNL Google Ads Enhanced Conversions] API擴展](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 用於事件轉發，與 [GoogleOauth 2機密](../../tags/ui/event-forwarding/secrets.md#google-oauth2)，將伺服器端資料安全地發送到 [!DNL Google Ads] 即時。 |

{style="table-layout:auto"}

## 目的地（2月2日更新） {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| [(Beta)Adobe Experience Cloud觀眾連接](../../destinations/catalog/adobe/experience-cloud-audiences.md) | 使用 [!UICONTROL （貝塔）Adobe Experience Cloud觀眾] 連接，以共用從Experience Platform到各種Experience Platform解決方案的段，如Audience Manager、分析、Advertising Cloud、Adobe Campaign、目標或Marketo。 |
| [Pega配置檔案連接](../../destinations/catalog/personalization/pega-profile.md) | 使用 [!DNL Pega Profile Connector] 在Adobe Experience Platform建立與 [!DNL Amazon] S3儲存，定期將配置檔案資料從Adobe Experience Platform導出到CSV檔案，並將其導出到您自己的S3儲存桶中。 在 [!DNL Pega Customer Decision Hub]，您可以安排資料作業從S3儲存導入此配置檔案資料以更新 [!DNL Pega Customer Decision Hub] 檔案。 |
| [(Beta)貿易台CRM EU連接](../../destinations/catalog/advertising/tradedesk-emails.md) | 隨著EUID（歐洲統一ID）的發佈，您現在看到兩個 [!DNL The Trade Desk - CRM] 目標 [目標目錄](/help/destinations/catalog/overview.md)。 <ul><li> 如果您在歐盟中源資料，請使用 **[!DNL The Trade Desk - CRM (EU)]** 目標。</li><li> 如果您在APAC或NAMER區域中源資料，請使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目標。 </li></ul> |

**新增或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 付費媒體同意策略增強，用於與流目標整合 | 安 [加強政策執行](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) 上 [流目標](/help/destinations/destination-types.md#streaming-destinations) 用於付費媒體激活使用案例。 當配置檔案不再有資格獲得同意策略時，Experience Platform現在會主動將其策略退出通知到流目標。 <br> <b>注釋</b>:此功能僅適用於 **[!UICONTROL 隱私和安全防護]**&#x200B;和 **[!UICONTROL 醫療保健盾]**。 |
| 測試版雲儲存目標連接器的新分隔符選項 | 三個新分隔符選項（冒號） `:`，管道，分號 `;`)現在可用於新的測試版雲儲存目標 —  [(β)AmazonS3](/help/destinations/catalog/cloud-storage/amazon-s3.md)。 [（測試版）Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md)。 [(Beta)Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md)。 [(Beta)資料登錄區](/help/destinations/catalog/cloud-storage/data-landing-zone.md)。 [（測試版）Google雲儲存](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)。 [(Beta)SFTP](/help/destinations/catalog/cloud-storage/sftp.md)。 <br> 閱讀支援的 [檔案格式選項](/help/destinations/ui/batch-destinations-file-formatting-options.md) 用於基於檔案的目標。 |
| 中提供的新可選參數 [客戶資料欄位](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md) 配置 [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`:當您需要建立客戶資料欄位時，使用此參數，該欄位的值必須在用戶組織設定的所有目標資料流中唯一。 <br> 例如， **[!UICONTROL 整合別名]** 的 [[!UICONTROL 自定義個性化]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) 目標必須唯一，這意味著到此目標的兩個單獨的資料流不能為此欄位具有相同的值。 |

**修復和增強** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>修復或增強</b></td>
        <td><b>說明</b></td>
    </tr>
    <tr>
        <td>已更新到基於檔案的目標的導出行為(PLAT-123316)</td>
        <td>我們解決了 <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">必備屬性</a> 將資料檔案導出到批處理目標時。 <br> 以前，輸出檔案中的每個記錄都已驗證為包含以下兩項： <ol><li>的非空值 <code>mandatoryField</code> 列和</li><li>至少一個其它非強制欄位上的非空值。</li></ol> 第二個條件已移除。 因此，您可能會在導出的資料檔案中看到更多輸出行，如下例所示：<br> <b> 2023年1月發佈前的行為示例 </b> <br> 必填欄位： <code>emailAddress</code> <br> <b>要激活的輸入資料</b> <br><table><thead><tr><th>名字</th><th>電子郵件地址</th></tr></thead><tbody><tr><td>約翰</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>傑尼費</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>激活輸出</b> <br><table><thead><tr><th>名字</th><th>電子郵件地址</th></tr></thead><tbody><tr><td>約翰</td><td>john@acme.com</td></tr><tr><td>傑尼費</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> 2023年1月發佈後的行為示例 </b> <br> <b>激活輸出</b> <br> <table><thead><tr><th>名字</th><th>電子郵件地址</th></tr></thead><tbody><tr><td>約翰</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>傑尼費</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>UI和API驗證所需映射和重複映射(PLAT-123316)</td>
        <td>現在，在UI和API中，如下強制執行驗證 <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mapping">映射欄位</a> 在激活目標工作流中：<ul><li><b>必需的映射</b>:如果目標開發人員已設定了所需的映射(例如， <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=en">Google廣告經理360</a> 目標)，則用戶在將資料激活到目標時需要添加這些所需的映射。 </li><li><b>重複映射</b>:在激活工作流的映射步驟中，可以在源欄位中添加重複的值，但不能在目標欄位中添加重複的值。 有關允許和禁止的映射組合的示例，請參閱下表。 <br><table><thead><tr><th>允許/禁止</th><th>來源欄位</th><th>目標欄位</th></tr></thead><tbody><tr><td>允許</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>電子郵件別名2</li></ul></td></tr><tr><td>禁止</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新增或更新的功能**

| 功能 | 說明 |
| --- | --- |
| 架構樹顯示名稱改進 | 以前，欄位名在UI中顯示，但現在，模式畫布上模式欄位的顯示名稱更易於人工讀取。 |

**新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL 轉換]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | 用於跟蹤兌換資料的類，如貨幣兌換。 |
| 欄位群組 | [[!UICONTROL 幣種折換率詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | 的欄位組 [!UICONTROL 轉換] 類，捕獲與貨幣兌換相關的其他詳細資訊。 |
| 欄位群組 | [[!UICONTROL 同意策略評估結果與元資料的映射]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | 捕獲多個同意策略的評估結果的詳細資訊，包括關於同意策略入口和存在的元資料資訊。 |

**更新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 資料類型 | [[!UICONTROL 廣告詳細資訊資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | 的 `ID` 欄位已更名為 `name`，以及 `name` 欄位 `friendlyName`。 |
| 資料類型 | [[!UICONTROL 決策建議詳細資訊]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | 已添加 `selectionStrategy` 欄位，用於捕獲選擇策略的詳細資訊。 |
| 欄位群組 | [[!UICONTROL 體驗事件 — 建議交互]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | 欄位組現在與 [!UICONTROL 行程步驟事件] 類。 |
| 資料類型 | [[!UICONTROL 錯誤詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | 的 `ID` 欄位已更名為 `name`。 |
| 資料類型 | [[!UICONTROL 媒體資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | 已將模式更改還原為視頻段屬性。 |
| 資料類型 | [[!UICONTROL Qoe資料詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 已刪除 `droppedFrameCount` 的子菜單。 |
| 資料類型 | [[!UICONTROL 會話詳細資訊資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 已更名 `isAuthorized` 欄位 `authorized`，更新 `type` 到字串。 |
| 資料類型 | [[!UICONTROL 裝運]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 添加了幾個新欄位： `shipDate`。 `trackingNumber`, `trackingURL`。 |
| 欄位群組 | [[!UICONTROL AJO實體欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | 添加了幾個新欄位： `journeyNodeID`。 `journeyNodeName`, `journeyModeType`。 |
| 欄位群組 | [[!UICONTROL 消費者體驗事件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | 欄位組現在也與 [!UICONTROL 摘要度量] 類。 |
| 欄位群組 | [[!UICONTROL 產品觸發器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | 的 `productTriggers` 欄位現在嵌套在 `weather` 的雙曲餘切值。 |
| 欄位群組 | [[!UICONTROL 相對觸發器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | 的 `relativeTriggers` 欄位現在嵌套在 `weather` 的雙曲餘切值。 |
| 欄位群組 | [[!UICONTROL 嚴重觸發器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 的 `severeTriggers` 欄位現在嵌套在 `weather` 的雙曲餘切值。 |
| 欄位群組 | [[!UICONTROL 天氣觸發器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 的 `weatherTriggers` 欄位現在嵌套在 `weather` 的雙曲餘切值。 |
| 欄位群組 | [[!UICONTROL XDM相關業務客戶]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | 現場組現在穩定。 |

{style="table-layout:auto"}

有關平台中XDM的詳細資訊，請參見 [XDM系統概述](../../xdm/home.md)。

## 即時客戶設定檔 {#profile}

Adobe Experience Platform使您能夠為您的客戶提供協調、一致和相關的體驗，無論客戶在何處或何時與您的品牌進行交互。 使用即時客戶配置檔案，您可以看到每個客戶的整體視圖，該視圖將來自多個渠道的資料組合在一起，包括線上、離線、CRM和第三方資料。 配置檔案允許您將客戶資料整合到一個統一視圖中，為每次客戶交互提供一個可操作且時間戳記的帳戶。

**即將淘汰** {#deprecation}

為消除段成員資格生命週期中的冗餘， `Existing` 狀態將從 [段成員資格映射](../../xdm/field-groups/profile/segmentation.md) 2023年3月底。 後續公告將包括確切的棄用日期。

折舊後，段中限定的配置檔案將表示為 `Realized` 取消資格的配置檔案將繼續作為 `Exited`。 這將帶來與基於檔案的目標的奇偶校驗 `Active` 和 `Expired` 段狀態。

如果您使用 [企業目標](../../destinations/destination-types.md#streaming-profile-export) (AmazonKinesis、Azure事件中心、 HTTP API)，並已根據 `Existing` 狀態。 如果情況是這樣，請檢查下游整合。 如果您希望確定超過一定時間的新合格配置檔案，請考慮使用 `Realized` 狀態和 `lastQualificationTime` 在段成員關係圖中。 詳情請洽Adobe代表。

要瞭解有關即時客戶概要資訊的更多資訊，包括有關使用概要資訊資料的教程和最佳做法，請首先閱讀 [即時客戶概要資訊概述](../../profile/home.md)。

## 分段服務 {#segmentation}

[!DNL Segmentation Service] 通過描述區分客戶群中可銷售人員組的標準來定義特定配置檔案子集。 段可以基於記錄資料（如人口統計資訊）或表示客戶與您品牌的交互的時間序列事件。

**新增或更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 段生成器中的批量值導入 | 段生成器現在支援通過上載CSV或TSV檔案或手動插入逗號分隔值來導入多個值。 在 [段生成器指南](../../segmentation/ui/segment-builder.md#rule-builder-canvas)。 |
| 外部受眾成員資格過期 | 預設情況下，外部訪問者成員身份將保留30天。 要將其保留更久，請使用 `validUntil` 的子菜單。 |
| 平台生成的段成員資格過期 | 位於 `Exited` 超過30天，根據 `lastQualificationTime` 欄位將被刪除。 |

{style="table-layout:auto"}

有關 [!DNL Segmentation Service]，請參閱 [分段概述](../../segmentation/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，並允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

| 功能 | 說明 |
| --- | --- |
| 允許用戶訪問雲儲存源的子資料夾 | 現在，您可以在建立新帳戶時定義對雲儲存源特定子資料夾的訪問權限。 建立後，用戶將只能訪問允許的子資料夾中的資料。 此功能可用於以下雲儲存源： [Azure Blob儲存](../../sources/connectors/cloud-storage/blob.md)。 [Google雲儲存](../../sources/connectors/cloud-storage/google-cloud-storage.md)。 [Google酒吧](../../sources/connectors/cloud-storage/google-pubsub.md), [SFTP](../../sources/connectors/cloud-storage/sftp.md)。 |
| Beta可用性 [!DNL SugarCRM] | [!DNL SugarCRM] 目前在beta中提供源。 使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 源從 [!DNL SugarCRM] 帳戶到Experience Platform。 有關詳細資訊，請閱讀 [[!DNL SugarCRM] 概述](../../sources/connectors/crm/sugarcrm.md)。 |
