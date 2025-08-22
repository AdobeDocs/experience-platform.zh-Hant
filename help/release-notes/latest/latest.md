---
title: Adobe Experience Platform 發行說明 (2025 年 8 月)
description: Adobe Experience Platform 2025 年 8 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: d2b605925a8fd7ea06f198ba8a9f85747a2e585b
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 33%

---

# Adobe Experience Platform 發行說明

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/pre-release-notes)
>- [聯合客群構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期： 2025年8月19日**

Adobe Experience Platform 的新功能及現有功能更新：

- [警報](#alerts)
- [目錄服務](#catalog-service)
- [目標](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [即時客戶輪廓](#profile)
- [沙箱](#sandboxes)
- [細分服務](#segmentation-service)
- [來源](#sources)

## 警報 {#alerts}

Experience Platform 可讓您訂閱各種 Experience Platform 活動的事件型警報。您可以透過 Experience Platform 使用者介面中的「[!UICONTROL 警報]」標籤訂閱不同的警報規則，而且可以選擇在使用者介面本身內或透過電子郵件通知接收警報訊息。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 串流輸送量容量警報 | 三個新警報可讓使用者訂閱及設定警報，主動管理及監控串流輸送量容量的效能。 新警報包括串流吞吐量達到80%、90%或超出容量限制時。 如需詳細資訊，請閱讀[容量警示規則](../../observability/alerts/rules.md#capacity)指南。 |

如需有關警示的詳細資訊，請參閱[[!DNL Observability Insights] 概觀](../../observability/home.md)。

## 目錄服務 {#catalog-service}

目錄服務是 Adobe Experience Platform 內部的資料位置和譜系記錄系統。雖然攝取至 Experience Platform 中的所有資料都會以檔案及目錄形式儲存在資料湖中，但是為了查詢和監控目的，目錄也會保留這些檔案及目錄的中繼資料與說明。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 即時客戶個人檔案的資料保留 | 您只能&#x200B;**每30天**&#x200B;更新一次即時客戶設定檔的資料保留期。 |

如需目錄服務的詳細資訊，請閱讀[目錄服務概觀](../../catalog/home.md)。

## 目標 {#destinations}

[!DNL Destinations]是預先建立的與目的地平台的整合，可讓您從Experience Platform順暢地啟用資料。 您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

>[!IMPORTANT]
>
>**資料集匯出排程延伸**
>
>如果您的組織在2024年11月之前建立了資料集匯出資料流，這些資料流將在&#x200B;**2025年9月1日**&#x200B;停止運作。 如果您需要資料流在2025年9月1日之後繼續匯出資料，您必須依照[本指南](../../destinations/ui/dataset-expiration-update.md)中的步驟，為您要匯出資料集的每個目的地擴充其排程。

>[!IMPORTANT]
>
>**API型目的地需要IP允許清單更新**
>
>由於已升級為串流目的地匯出引擎，使用API型目的地[IP允許清單](../../destinations/catalog/streaming/ip-address-allow-list.md)的組織必須在2025年9月15日之前，將下列IP位址新增至其允許清單&#x200B;**&#x200B;**：
>
>**必要的IP位址：**
>
>```
>3.209.222.108
>3.211.230.204
>35.169.227.49
>66.117.18.133
>66.117.18.134
>66.117.18.135
>```
>
>**此變更適用於下列目的地型別：**
>
>- [串流對象匯出目的地](../../destinations/destination-types.md#streaming-destinations) ([Pega CDH即時對象](/help/destinations/catalog/personalization/pega-v2.md)，與[Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md)和[Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)的API型整合)
>- 透過[Destination SDK](../../destinations/destination-sdk/getting-started.md)建置的公用或私人目的地
>
>**需要動作：**&#x200B;如果您已與Adobe合作將任何IP位址加入允許清單至API型串流目的地，您必須將上述IP位址新增至允許清單，以確保資料流不會中斷至以API型為基礎的目的地。

**新目的地**

| 目標 | 說明 |
| --- | --- |
| [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md)目的地 | 使用[!DNL Acxiom Real ID Audience Connection]目的地來增強具有[!DNL Acxiom's] [真實識別碼](https://www.acxiom.com/real-id/real-id/)技術的對象，並啟用多個平台的對象，例如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。 |
| 增強的[[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)目的地 | 增強的[[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)目的地是現有[[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)聯結器的升級版本。 除了舊版聯結器的現有對象同步功能之外，這個新的聯結器還引進了設定檔同步功能，提供與[!DNL Marketo Engage]更緊密的整合。 <br> [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)聯結器將於&#x200B;**2026年3月**&#x200B;日淘汰。 若要確保順利轉換至新的&#x200B;**[[!UICONTROL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)**&#x200B;目的地，請檢閱下列要點和必要的動作： <ul><li>現有&#x200B;**[!UICONTROL （舊版） (V2) Marketo Engage]**&#x200B;的所有使用者必須在2026年3月前移轉至新的&#x200B;**[!UICONTROL Marketo Engage]**&#x200B;目的地。</li><li> **現有的資料流將不會自動移轉。**&#x200B;您必須[設定與新](../../destinations/ui/connect-destination.md)Marketo Engage **[!UICONTROL 目的地的新連線]**，並在那裡啟用您的對象。</li></ul> |

**已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) 內部升級 | 從2025年8月11日開始，您可能會在目的地目錄中看到兩張&#x200B;**[!DNL Microsoft Bing]**&#x200B;卡片並排。 這是因為目標服務進行內部升級所致。現有的&#x200B;**[!DNL Microsoft Bing]**&#x200B;目的地聯結器已重新命名為&#x200B;**[!UICONTROL （已棄用） Microsoft Bing]**，現在您可以使用名稱為&#x200B;**[!UICONTROL Microsoft Bing]**&#x200B;的新卡片。 <br>升級已完成，且已棄用的卡片已從目的地目錄中移除。 使用目錄中的&#x200B;**[!UICONTROL Microsoft Bing]**&#x200B;連線，以取得新的啟用資料流程。 如果您有任何作用中資料流至&#x200B;**[!UICONTROL （已棄用） Microsoft Bing]**&#x200B;目的地，資料流會自動更新，因此您不需要採取任何動作。 <br><br>如果您透過 [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 建立資料流，則您必須將 [!DNL flow spec ID] 和 [!DNL connection spec ID] 更新為下列值：<ul><li>流程規格 ID：`8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>連線規格 ID：`dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> 此升級後，您的資料流中啟用的設定檔數目&#x200B;**可能會減少到**，人數為[!DNL Microsoft Bing]。 這個下降是由於針對這個目的地平台的所有啟用引入&#x200B;**ECID對應需求**&#x200B;所造成。 |
| [[!DNL LinkedIn]](../../destinations/catalog/social/linkedin.md)和[LinkedIn相符對象](../../destinations/catalog/social/linkedin-b2b.md)目的地的驗證到期詳細資料 | [!DNL LinkedIn]目的地的驗證到期資訊現在會直接顯示在Experience Platform介面中，因此您可以檢視您的驗證將於何時到期並續約，以免對資料流造成任何中斷。 您可以從&#x200B;**[!UICONTROL 帳戶]**&#x200B;或&#x200B;**[[!UICONTROL 瀏覽]](../../destinations/ui/destinations-workspace.md#accounts)**&#x200B;索引標籤中的&#x200B;**[[!UICONTROL 帳戶到期日]](../../destinations/ui/destinations-workspace.md#browse)**&#x200B;欄監視您的權杖到期日。 |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 增強目的地的搜尋、篩選和標籤功能 | 透過[瀏覽](../../destinations/ui/destinations-workspace.md#browse)和[帳戶](../../destinations/ui/destinations-workspace.md#accounts)索引標籤的增強搜尋、篩選和標籤功能，改善您的目的地管理工作流程。 <br>您現在可以依名稱搜尋特定的資料流和帳戶、依各種條件篩選（包括目的地平台、狀態和日期），以及建立自訂標籤來組織您的目的地。 欄排序也可用於關鍵欄位，例如上次資料流執行時間，讓您更容易識別和管理您的目的地連線。<br> ![在[瀏覽]索引標籤中搜尋目的地資料流的動畫示範](../../destinations/assets/ui/workspace/search.gif) |


## 體驗資料模型 (XDM，Experience Data Model) {#xdm}

XDM是開放原始碼規格，針對匯入Experience Platform的資料提供通用結構和定義（結構描述）。 若遵守 XDM 標準，即可將所有客戶體驗資料合併為單一常用表述，以更快速、更整合的方式提供分析洞察。您可以從客戶行為中獲得有價值的分析洞察、透過區段定義客戶客群，並基於個人化目的使用客戶屬性。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 以模型為基礎的結構描述 | 使用以模型為基礎的結構描述簡化資料模型。 您現在可以更輕鬆地建立方案，其中包含完整的作法範例和指引。 此功能目前可供Campaign Orchestration授權持有人使用，並會在GA擴充至Data Distiller客戶，讓資料模型更容易存取且更有效率。 |

如需詳細資訊，請閱讀[XDM總覽](../../xdm/home.md)。

## 即時客戶輪廓 {#profile}

即時客戶設定檔可將所有管道的資料合併為單一設定檔，藉此提供每個客戶的統一可操作檢視。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 增強實體API中的查閱功能 | 實體API現在支援下列專案： <ul><li>人員（設定檔）</li><li>體驗事件</li><li>帳戶</li><li>機會</li></ul> 此更新簡化API使用方式，並有助於確保最佳效能和可靠性。 如果您先前曾使用其他實體型別（包括聯結表格和自訂多實體型別）的查詢，現在就是檢閱API使用情況並利用改良體驗的絕佳機會。 如需詳細資訊，請參閱[Real-Time CDB B2B edition架構升級指南](../../rtcdp/b2b-architecture-upgrade.md)。 |

如需即時客戶個人檔案的詳細資訊，請閱讀[個人檔案總覽](../../profile/home.md)。

## 沙箱 {#sandboxes}

Experience Platform 旨在協助您在全球各地打造更豐富的數位體驗應用程式。公司經常並行執行多個數位體驗應用程式，不但要顧及這些應用程式的開發、測試和部署等需求，也必須確保營運合規性。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 匯入工作流程中的相依性物件去重複化 | 沙箱工具現在一律會在偵測到相同名稱的物件時重複使用現有的物件，以避免物件擴散。 此變更會套用至下列物件： <ul><li>結構描述</li><li>欄位群組</li><li>客群</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> 如需詳細資訊，請閱讀[沙箱工具支援物件指南](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)。 |
| 針對跨組織套件共用的完整沙箱支援 | 沙箱工具現在支援跨組織套件共用中的&#x200B;**整個沙箱**&#x200B;型別。 您現在可以跨組織共用整個沙箱和多物件套件。 如需詳細資訊，請閱讀[沙箱工具支援物件指南](../../sandboxes/ui/sharing-packages-across-orgs.md)。 |

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 對象估計 | 對象預估現在會在區段產生器中自動產生。 此值會在您修改對象時更新，且一律會反映最新的對象規則。 此外，估計值現在會顯示為&#x200B;**範圍**，這是根據取樣資料的信賴區間而定。 |

如需詳細資訊，請閱讀 [[!DNL Segmentation Service]  概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 在UI中支援[!BADGE 的]{type=Informative}Beta[!DNL Azure Private Links] | 您現在可以將[!DNL Azure Private Links]用於UI中選定的來源群組。 使用此功能可建立您的來源可連線的私人端點。 透過私用端點，您可以設定繞過公用網際網路的連線和資料流程，為您提供增強的安全性和網路隔離功能，以隔離敏感資料。 下列來源支援[!DNL Azure Private Links]： <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> 如需詳細資訊，請閱讀[[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md)上的指南。 |
| [!DNL Azure Blob Storage]的增強驗證 | 您現在可以使用以服務主體為基礎的驗證，將您的[!DNL Azure Blob Storage]來源連線至Experience Platform。 使用以服務主體為基礎的驗證來增強安全性、更輕鬆的認證輪換，以及更精細的帳戶存取控制。 如需詳細資訊，請閱讀 [[!DNL Azure Blob Storage]  概觀](../../sources/connectors/cloud-storage/blob.md)。 |

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。