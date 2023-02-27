---
title: Adobe Experience Platform 發行說明
description: 2023年2月Adobe Experience Platform發行說明。
source-git-commit: deb8512d3c585512520dae04e555c6497d74ba4c
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 7%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 2 月 22 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Destinations]](#destinations)
- [Experience Data Model(XDM)](#xdm)
- [查詢服務](#query-service)
- [Real-Time Customer Data Platform B2B 版本](#b2b)
- [來源](#sources)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新功能或更新功能** {#destinations-new-updated-features}

| 功能 | 說明 |
| ----------- | ----------- |
| [同意政策增強](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) 與 [檔案型（批次）目的地](/help/destinations/destination-types.md#file-based) | <p> 當設定檔不再符合同意原則的資格時，Experience Platform現在會主動將其退出政策通訊至檔案式目的地。 這遵循 [於2023年2月發行](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) 流目的地功能相同。 </p> <p> <b>附註</b>:此功能僅適用於 **[!UICONTROL 隱私與安全防護]**，以及 **[!UICONTROL 醫療保健盾]**. </p> |

{style=&quot;table-layout:auto&quot;}

**新檔案或更新檔案** {#destinations-new-updated-documentation}

| 文件 | 說明 |
| ----------- | ----------- |
| 目的地如何運作檔案 | <p>我們根據使用者的常見問題，發佈了三篇關於目的地運作方式的新說明文章：</p> <p><ul><li>[目的地中的可設定和通用匯出設定](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[不同目的地類型的設定檔匯出行為](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[目的地啟動工作流程中的身分處理](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

如需目的地的詳細一般資訊，請參閱 [目的地概述](../../destinations/home.md).

## Experience Data Model(XDM) {#xdm}

XDM是開放原始碼規格，可針對匯入Adobe Experience Platform的資料提供通用結構和定義（結構）。 遵循XDM標準，所有客戶體驗資料皆可整合至通用表示法，以更快速、更整合的方式提供深入分析。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 透過UI取代欄位 | 您現在可以 [擷取資料後，會取代結構中的欄位](../../xdm/tutorials/field-deprecation-ui.md). 取代XDM欄位可讓您從UI檢視中移除欄位，同時保留欄位以供使用。 您可以視需要再次顯示已棄用的欄位，而任何參考欄位的區段、查詢或下游解決方案將照常執行。 |

{style=&quot;table-layout:auto&quot;}

**新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL XDM個別潛在客戶設定檔]](https://github.com/adobe/xdm/pull/1669/files) | XDM個別潛在客戶設定檔類別會提供合作夥伴提供的ID。 |

{style=&quot;table-layout:auto&quot;}

**更新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位群組 | [!UICONTROL 頻率限定限制] | 此 [!UICONTROL 頻率限定限制] 欄位組已 [更新以支援重複和自訂事件](https://github.com/adobe/xdm/pull/1641/files). |
| 資料類型 | [!UICONTROL 網頁反向連結] | 網頁反向連結屬性已 [更新以包含 `xdm:linkName` 和 `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). 分別是在上一頁選取的HTML元素的名稱和地區。 |
| 欄位組 | [!UICONTROL AdobeCJM ExperienceEvent — 訊息互動詳細資訊] | [此 [!UICONTROL 追蹤器URL] 欄位已新增](https://github.com/adobe/xdm/pull/1665/files) 到 [!UICONTROL AdobeCJM ExperienceEvent]. 此追蹤器提供使用者選取的URL。 |
| 欄位組 | [!UICONTROL AdobeCJM ExperienceEvent — 訊息互動詳細資料] | [空白 `meta:enum` 屬性已移除](https://github.com/adobe/xdm/pull/1668/files) 從URL [!UICONTROL 追蹤類型] 欄位。 |
| 資料類型 | [!UICONTROL 媒體資訊] | [來自的規則運算式模式 `videoSegment` 屬性 [!UICONTROL 媒體資訊] 資料類型已刪除](https://github.com/adobe/xdm/pull/1667/files). |

{style=&quot;table-layout:auto&quot;}

如需Platform中XDM的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## 查詢服務 {#query-service}

查詢服務可讓您使用標準SQL在Adobe Experience Platform中查詢資料 [!DNL Data Lake]. 您可以加入Data Lake中的任何資料集，並將查詢結果擷取為新資料集，以用於報表、Data Science Workspace或擷取至即時客戶個人檔案。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 為配置檔案啟用SQL資料集 | 在CTAS查詢中使用LABEL來建立資料集「已啟用配置檔案」，或使用ALTER更新要為配置檔案啟用的現有資料集。 |
| 監視計畫查詢 | 使用「計畫查詢」頁簽查找有關查詢運行和訂閱警報的重要資訊。 如果排程詳細資訊、狀態和錯誤訊息/代碼失敗，則監視查詢。 |
| 切換自動完成功能 | 切換查詢編輯器自動完成功能，消除特定中繼資料命令並改善處理時間。 此功能會在您編寫查詢時，自動為查詢建議潛在的SQL關鍵字和表詳細資訊。 |
| 資料集範例 | 在查詢中指定取樣率，並使用資料集範例來建立統一的隨機範例，或根據特定條件建立條件範例。 |

{style=&quot;table-layout:auto&quot;}

有關Query Services的詳細資訊，請參閱 [查詢服務概述](../../query-service/home.md).

<!-- Links for QS feature docs after release day: -->
<!-- Enable datasets for profile with SQL link: https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html#create-table-as-select -->
<!-- Monitor scheduled queries link: https://experienceleague.adobe.com/docs/experience-platform/query/monitor-queries.html  -->
<!-- Toggle auto-complete feature link: https://experienceleague.adobe.com/docs/experience-platform/query/ui/user-guide.html#auto-complete -->
<!-- dataset samples: https://experienceleague.adobe.com/docs/experience-platform/query/essential-concepts/dataset-samples.html -->

## Real-Time Customer Data Platform B2B 版本 {#b2b}

Real-Time CDP B2B Edition以Real-time Customer Data Platform(Real-Time CDP)為基礎，專為以企業對企業服務模式運作的行銷人員所打造。 它匯集了來自多個來源的資料，並將其結合為人員和帳戶設定檔的單一檢視。 此統一的資料可讓行銷人員精確鎖定特定對象，並參與所有可用管道中的這些對象。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 啟用相關帳戶服務 | 新的切換功能可讓您在帳戶上啟用相關帳戶服務。 如需詳細資訊，請參閱 [啟用相關帳戶服務](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

若要進一步了解Real-Time CDP B2B版，請閱讀 [Real-Time CDP B2B版概述](../../rtcdp/overview.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，並可讓您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 指定訂閱層級存取，使用 [!DNL Google PubSub] | 您現在可以使用 [!DNL Google PubSub] 來源，在驗證時提供訂閱ID。 如需詳細資訊，請閱讀 [!DNL Google PubSub] 驗證教學課程 [使用流量服務API](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) 或 [平台UI](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| 從內嵌自訂活動資料 [!DNL Marketo] | 您現在可以從 [!DNL Marketo] 例項Experience Platform。 若要內嵌自訂活動資料，您必須在B2B活動結構中設定自訂活動欄位群組，並使用活動資料集建立資料流。 資料流完成後，所擷取的資料集將同時包含您 [!DNL Marketo] 例項。 然後，您就可以使用 [查詢服務](../../query-service/home.md) 存取Platform上的自訂活動記錄。 如需詳細資訊，請參閱 [為自訂活動資料建立資料流](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| 從 [!DNL Marketo] | 您現在可以設定在為公司資料建立資料流時，是否要排除或納入未申請的帳戶以免擷取。 如需詳細資訊，請參閱 [建立源連接和資料流 [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

若要進一步了解來源，請閱讀 [來源概觀](../../sources/home.md).
