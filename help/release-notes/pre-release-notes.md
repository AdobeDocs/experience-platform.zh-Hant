---
title: Experience Platform發行前說明
description: Adobe Experience Platform最新版本注意事項預覽。
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 8f898e618fbc2b414a3c899511ac410465f280d8
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 17%

---

# Adobe Experience Platform搶鮮版發行說明

>[!IMPORTANT]
>
>本檔案旨在當月發行說明的&#x200B;**預覽**。 發行專案可能會有所變更，且可能會在最終發行中新增或移除。

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/latest)
>- [聯合客群構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期：2026 年 4 月**

Adobe Experience Platform 的新功能及現有功能更新：

- [目的地](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [查詢服務](#query-service)
- [Real-Time CDP](#rtcdp)
- [沙箱](#sandboxes)
- [細分服務](#segmentation-service)
- [來源](#sources)

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Experience Platform 的資料。您可以使用目標來啟用已知和未知的資料，以供跨通道行銷活動、電子郵件行銷活動、定向廣告及其他許多使用案例使用。

**全新或已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [Microsoft Ads客戶符合](../destinations/catalog/advertising/microsoft-ads-customer-match.md) | 依電子郵件地址比對客戶，並在[!DNL Microsoft Advertising Network]中與客戶重新互動，包括搜尋和對象廣告。 將您的[!DNL Microsoft Advertising]帳戶連結至Real-Time CDP，以直接從Experience Platform自動建立和管理客戶比對清單。 若要取得存取權，請聯絡您的Adobe客戶經理。 |
| [!BADGE Beta]{type=Informative} [Reddit自訂對象](../destinations/catalog/advertising/reddit-custom-audience.md) | 將對象從Experience Platform傳送至[!DNL Reddit Ads]。 連線您的[!DNL Reddit]帳戶、對應身分並啟用對象，以聯絡在[!DNL Reddit]上積極探索其興趣的人。 |
| [Amazon Ads v2](../destinations/catalog/advertising/amazon-ads-v2.md) | [!DNL Amazon Ads v2]是所有新[!DNL Amazon Ads]連線的目前目的地。 如果您有現有的[（舊版） [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md)連線，它將繼續運作，而不會進行任何必要的變更。 [!DNL Amazon Ads v2]連線到[!DNL Ads Data Manager]，後者支援擴充的身分型別、位址相關欄位，以及跨[!DNL Amazon Ads]個產品的資料共用，相較於[ （舊版） [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md)改善鎖定目標和對象符合率。 |
| [!DNL Rokt] | 使用[!DNL Rokt]將Experience Platform對象連結到AI驅動的即時決策，透過更精確的目標定位、隱藏和個人化來改善行銷活動績效。 |
| [Criteo](../destinations/catalog/advertising/criteo.md)的外部對象支援 | 從Segmentation Service以外的來源啟用對象至[!DNL Criteo]，包括自訂上傳對象（從CSV匯入）、相似對象、同盟對象，以及在其他Experience Platform應用程式（例如[!DNL Adobe Journey Optimizer]）中建立的對象。 如需詳細資訊，請參閱[支援的對象](../destinations/catalog/advertising/criteo.md#supported-audiences)區段。 |
| [Acxiom對象連線](../destinations/catalog/advertising/acxiom-audience-connection.md) | [!DNL Acxiom Audience Connection]目的地現在已可供一般使用。 使用它來增強具有[!DNL Acxiom's Real ID]技術的對象，並將他們啟用至其他平台，包括[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]、[!DNL Cox]、[!DNL LG Ads]、[!DNL Spectrum]和[!DNL Viant]。 |
| [Acxiom真實ID對象連線](../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | [!DNL Acxiom Real ID Audience Connection]目的地現在已可供一般使用。 使用它來啟用受眾，將[!DNL Acxiom's Real ID]當做相同受支援平台集的相符索引鍵，包括[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]、[!DNL Cox]、[!DNL LG Ads]、[!DNL Spectrum]和[!DNL Viant]。 |

{style="table-layout:auto"}

**修正和改良**

| 修正 | 說明 |
| --- | --- |
| 自訂Personalization監控支援 | 目的地的監視儀表板現在支援[!DNL Custom Personalization]個目的地。 已移除從監視中排除[!DNL Custom Personalization]的限制備註。 |
| 啟動檢閱中的設定檔計數 | 啟用檢閱步驟現在會顯示已啟用的對象的設定檔計數。 也會顯示串流目的地的設定檔計數，而不僅僅是批次目的地。 |
| [!DNL Pinterest]權杖到期可見性 | [!DNL Pinterest]目的地現在顯示直接從[!DNL Pinterest]傳回的權杖到期時間，因此您可以看到何時需要重新驗證。 |
| 匯出檔案現在已針對無效排程停用 | 當對象排程無效或過期時，**[!UICONTROL Export file now]**&#x200B;動作現在會停用。 工具提示會說明動作無法使用的原因。 |
| 啟動工作流程中的欄可見性修正 | 修正變更一個表格中的可見欄位，錯誤地影響啟動工作流程中其他表格的問題。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../destinations/home.md)。

## 體驗資料模型 (XDM) {#xdm}

XDM是開放原始碼規格，為引入Experience Platform的資料提供通用結構和定義（結構描述）。 只要遵循XDM標準，所有客戶體驗資料都可整合到共同表現中，以更快、更整合的方式提供深入分析。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 欄位群組結構描述使用方式可見性 | 從詳細資料頁面檢視使用欄位群組的結構描述，並在包含結構描述中繼資料的可排序對話方塊中探索它們。 這可幫助您快速評估相依性和影響，而無需離開該頁面。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[XDM系統總覽](../xdm/home.md)。

## 查詢服務 {#query-service}

使用查詢服務以查詢具有標準SQL的Adobe Experience Platform [!DNL Data Lake]中的資料。 從[!DNL Data Lake]加入任何資料集，並將查詢結果擷取為新資料集，以用於報表、Data Science Workspace，或內嵌至Real-Time Customer Profile。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 資料Distiller加速器 | 在查詢服務UI中執行並排程Adobe管理的引數化SQL範本，以執行一般分析而不撰寫SQL。 這可協助您標準化分析工作流程，並在整個組織中重複使用信任的查詢邏輯。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[查詢服務總覽](../query-service/home.md)。

## Real-Time CDP {#rtcdp}

[!DNL Real-Time CDP]透過跨多個管道即時擷取、處理和啟用資料，提供統一且可操作的客戶設定檔。 透過Real-Time CDP，組織可以連線現有的資料來源、建置和啟用豐富受眾，並確保從Experience Platform跨目的地啟用符合隱私權的啟用作業。 透過順暢的跨管道行銷活動，行銷人員、分析師和IT團隊得以為其客戶提供高度個人化、即時的體驗。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| Real-Time CDP MCP (Beta) | 使用Real-Time CDP MCP將Real-Time CDP帶入AI代理程式和MCP相容的使用者端，讓您直接透過原生LLM體驗與Real-Time CDP工具互動。 藉由將與MCP相容的使用者端（例如Claude、ChatGPT、Claude Code、Codex、Cursor或VS Code）連線至`https://rtcdp-mcp.adobe.io/mcp`，您可以使用自然語言來檢查對象、目的地設定和啟動執行歷史記錄，而不需要撰寫Experience Platform REST API呼叫或導覽多個UI工作流程。 完成瀏覽器式Adobe登入後，您將擁有工具的唯讀存取權，包括： <ul><li>搜尋現有對象</li><li>預覽對象會籍</li><li>列出目的地型別</li><li>列出已設定的帳戶</li><li>列出已設定的目的地</li><li>列出Source連線</li><li>列出目標連線</li><li>檢查啟動執行</li></ul>. 每個請求都需要`imsOrgId`和`sandboxName`引數，以確保動作範圍限定在您的組織和沙箱中。 請注意，此Beta版本不支援寫入作業。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[Real-Time CDP概觀](../rtcdp/home.md)。

## 沙箱 {#sandboxes}

Adobe Experience Platform 旨在協助您在全球各地打造更豐富的數位體驗應用程式。公司通常會同時執行多個數位體驗應用程式，而且需要滿足這些應用程式的開發、測試和部署需求，同時確保營運合規性。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 快速複製 | 使用Express Copy從[沙箱工具UI](/help/sandboxes/ui/sandbox-tooling.md#express-copy)以單一動作將物件複製到目標沙箱。 系統會自動偵測相依物件，並在目標沙箱中建立，或當相依物件已存在時重複使用。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[沙箱總覽](../sandboxes/home.md)。

## 細分服務 {#segmentation-service}

使用細分服務從您的客戶資料建立對象，並在Experience Platform中管理其完整的生命週期。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 串流細分監視 | 在沙箱、資料集和區段層級即時顯示評估率、擷取延遲和資料品品質度，以監控串流區段。 檢視量度，包括評估率、P95擷取延遲、收到的記錄、評估的記錄、失敗的記錄和略過的記錄。 也檢視每個區段符合資格和取消資格的淨新設定檔。 使用這些見解來識別容量違規和擷取問題，以免影響您的資料。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[對象總覽](../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**新的或更新來源**

| 來源 | 說明 |
| --- | --- |
| 自動停用資料流 | 持續失敗30天的來源擷取資料流會自動停用，有助於呈現不健康的資料流並減少重複的失敗執行。 |
| [!DNL Delta Sharing] | 您可以使用[!DNL Delta Sharing]來源，透過安全、開放的資料共用通訊協定，將Delta資料錶帶入Experience Platform。 在您設定[!DNL Delta Sharing]連線並選取要擷取的共用和表格後，Platform會自動將該資料帶入您的資料集，以便您將其用於分析、細分和啟用。 |
| [!DNL Meta Ads] (Beta) | 您可以在來源工作區中使用[!DNL Meta Ads]來源聯結器(Beta)來驗證[!DNL Meta]、選取您的廣告帳戶，以及排程將[!DNL Meta Ads]行銷活動和效能資料擷取到Experience Platform資料集。 |
| [!DNL Talon.One] | 您現在可以使用新的[!DNL Talon.One]批次和串流來源將Experience Platform連線至[!DNL Talon.One]。 使用新來源將熟客資料以及交易和熟客活動事件擷取到Experience Platform。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../sources/home.md)。
