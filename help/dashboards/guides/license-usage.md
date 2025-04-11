---
keywords: Experience Platform；使用者介面；UI；自訂；授權使用儀表板；儀表板；授權使用；權益；使用
title: 授權使用情況儀表板
description: Adobe Experience Platform提供一個儀表板，您可以透過它檢視有關您組織授權使用情況的重要資訊。
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3413'
ht-degree: 39%

---

# 授權使用量儀表板 {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="testy-mctestface"
>title="不應該顯示的測試對話框"
>abstract="有人在 {date} 檢視物件 {name}。"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_core"
>title="核心產品表"
>abstract="表格中列出的核心產品有自己的量度、使用情況追蹤和沙箱層級的鑽研式視圖。這些核心產品提供關鍵量度以利追蹤，而且任何附加元件皆包含在這些量度中。"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_addons"
>title="附加元件表"
>abstract="附加元件表列出授權數量與核心產品所支援的量度結合之產品。這些附加元件沒有個別的量度，但能增強與其相關之核心產品的使用情況追蹤。"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage"
>title="授權使用量儀表板"
>abstract="授權使用量儀表板讓您可深入了解您已購買的 Adobe Experience Platform 產品。儀表板概觀會顯示您產品的主要量度，包括每個主要量度的使用量以及您的合約授權數量。詳細資料工作區顯示特定沙箱中每個產品的量度劃分。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="自動化資料集期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_licenseusage"
>title="授權使用量儀表板"
>abstract="授權使用量儀表板讓您可深入了解您已購買的 Adobe Experience Platform 產品。儀表板概觀會顯示您產品的主要量度，包括每個主要量度的使用量以及您的合約授權數量。詳細資料工作區顯示特定沙箱中每個產品的量度劃分。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="自動化資料集期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_computehours"
>title="預測的運算小時數"
>abstract="運算小時數會測量查詢服務引擎在執行批次查詢時，用於讀取、處理和寫入資料的時間。<br>您的使用量可能會達到已授權數量。若要評估或減少使用量，請前往「查詢 > 記錄」，檢閱您的查詢歷史記錄。如果您沒有「查詢」工作區的存取權，請聯絡您的管理員。"
>additional-url="https://experience.adobe.com/#/platform/query/log.html" text="查詢記錄工作區"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_addressableaudience"
>title="預測的可定址對象"
>abstract="可定址對象為您組織有權參與之即時客戶輪廓中的一組個人設定檔。此量度包括直接可識別的設定檔和匿名設定檔兩者。<br>您的使用量可能會達到已授權數量。若要減少使用量，請設定資料集或匿名設定檔資料的過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="體驗事件期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_engageableprofiles"
>title="預測的可參與設定檔"
>abstract="可參與設定檔為您組織在過去 12 個月內，嘗試使用 Journey Optimizer 來參與之即時客戶輪廓中的個人設定檔。<br>您的使用量可能會達到已授權數量。若要減少使用量，請設定資料集或匿名設定檔資料的過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="體驗事件期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_businesspersonprofile"
>title="預測的商業人士設定檔"
>abstract="商業人士設定檔為即時客戶輪廓中的記錄，代表 B2B 內容中之個體。<br>您的使用量可能會達到已授權數量。若要減少使用量，請設定資料集或匿名設定檔資料的過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="體驗事件期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_corehours"
>title="預測的核心時數"
>abstract="核心時數代表整個 Experience Platform 服務所耗費的處理時間。<br>您的使用量可能會達到已授權數量。若要減少使用量，請設定資料集或匿名設定檔資料的過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="體驗事件期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_totaldatavolume"
>title="預測的總資料量"
>abstract="總資料量為即時客戶輪廓中適用於參與度和個人化工作流程的可用資料量。<br>您的使用量可能會達到已授權數量。若要減少使用量，請設定資料集或匿名設定檔資料的過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="體驗事件期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_cjaRowsAvailable"
>title="預測的 CJA 可用列數"
>abstract="CJA 可用列數是指適用於在 Customer Journey Analytics 中進行分析的每日平均可用資料列數。<br>您的使用量可能會達到已授權數量。若要減少使用量，請設定資料集或匿名設定檔資料的過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="體驗事件期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_addressableaudience"
>title="預測的可定址對象"
>abstract="可定址對象為您組織有權參與之即時客戶輪廓中的一組個人設定檔。包括直接可識別的設定檔和匿名設定檔兩者。<br>您的使用量已經超出已授權數量。若要減少使用量，請設定資料集或匿名設定檔資料的過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="體驗事件期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_engageableprofiles"
>title="預測的可參與設定檔"
>abstract="可參與設定檔為您組織在過去 12 個月內，嘗試使用 Journey Optimizer 來參與之即時客戶輪廓中的個人設定檔。<br>您的使用量已經超出已授權數量。若要減少使用量，請設定資料集或匿名設定檔資料的過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="體驗事件期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_businesspersonprofile"
>title="預測的商業人士設定檔"
>abstract="商業人士設定檔為即時客戶輪廓中的記錄，代表 B2B 內容中之個體。<br>您的使用量已經超出已授權數量。若要減少使用量，請設定資料集或匿名設定檔資料的過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="體驗事件期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_corehours"
>title="預測的核心時數"
>abstract="核心時數代表整個 Experience Platform 服務所耗費的處理時間。<br>您的使用量已經超出已授權數量。若要減少使用量，請設定資料集或匿名設定檔資料的過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="體驗事件期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_totaldatavolume"
>title="預測的總資料量"
>abstract="總資料量為即時客戶輪廓中適用於參與度和個人化工作流程的可用資料量。<br>您的使用量已經超出已授權數量。若要減少使用量，請設定資料集或匿名設定檔資料的過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="體驗事件期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_cjaRowsAvailable"
>title="預測的 CJA 可用列數"
>abstract="CJA 可用列數是指適用於在 Customer Journey Analytics 中進行分析的每日平均可用資料列數。<br>您的使用量已經超出已授權數量。若要減少使用量，請設定資料集或匿名設定檔資料的過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="體驗事件期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

您可以透過Adobe Experience Platform [!UICONTROL 授權使用情況]儀表板，檢視貴組織授權使用情況的重要資訊。 此處顯示的資訊是在Experience Platform執行個體的每日快照期間擷取。

授權使用報告提供高度精細度。 大多數量度會在多個產品之間共用，並反映所有使用它們的產品的彙總使用量，而非每個產品的總計。 儀表板提供這些量度在所有生產或開發沙箱中的綜合使用方式，以及來自特定沙箱的使用量度。 下列Experience Platform應用程式可透過使用量度進行追蹤：Real-Time Customer Data Platform、Adobe Journey Optimizer和Customer Journey Analytics。

本指南概述如何存取和使用UI中的授權使用儀表板，並提供有關儀表板中顯示的視覺效果的更多資訊。

如需Experience Platform UI的一般概觀，請參閱[Experience Platform UI指南](../../landing/ui-guide.md)。

## [!UICONTROL 授權使用情況]儀表板資料

[!UICONTROL 授權使用情況]儀表板會顯示您已購買的所有Experience Platform產品清單，以及這些產品的任何附加元件。 在此控制面板中，您可以找到組織在任何相關沙箱中用於Experience Platform的授權相關資料快照。

此儀表板中的資料會完全依照快照拍攝時的特定時間點顯示。 它不是近似值或範例，但儀表板不會即時更新。

>[!NOTE]
>
>儀表板中的大部分量度都會根據您的Experience Platform執行個體快照每日更新。 [!UICONTROL 可用的CJA資料列]為例外狀況，每月都會更新。 標示為「套件」的量度，例如[!UICONTROL Adhoc Query Service Users Pack]、[!UICONTROL Profile Richness No of Pack]和[!UICONTROL Streaming Segmentation No of Pack]，反映附加元件產品的授權權益，且不會追蹤目前使用情況。 在拍攝下一個快照之前，不會顯示快照之後所做的變更。

## 探索授權使用儀表板 {#explore}

若要導覽至Experience Platform UI中的授權使用儀表板，請在左側邊欄中選取&#x200B;**[!UICONTROL 授權使用]**。 儀表板包含兩個標籤： **[!UICONTROL Metrics]**&#x200B;和&#x200B;**[!UICONTROL Products]**。

>[!NOTE]
>
>授權使用儀表板預設為未啟用。 必須授予使用者「檢視授權使用儀表板」許可權才能檢視儀表板。 如需授與存取許可權的步驟，請參閱[儀表板許可權指南](../permissions.md)。

## [!UICONTROL 量度]標籤 {#metrics-tab}

**[!UICONTROL Metrics]**&#x200B;索引標籤可讓您集中檢視整個組織中的所有授權使用量度。 由於大部分的量度會在產品之間共用，因此這些量度沒有個別的個別產品劃分。

量度表格包含下列各欄：

| 欄名稱 | 說明 |
|---|---|
| **[!UICONTROL 量度名稱]** | 授權使用量度的名稱。 每個專案都包含一個資訊圖示(`ⓘ`)，顯示相關產品的說明和清單。 |
| **[!UICONTROL 已授權]** | 貴組織有權使用的單位數量（如合約所定義）。 此量度的值與[產品]索引標籤中的&#x200B;**授權金額**&#x200B;相同。 |
| **[!UICONTROL 已測量]** | 您的組織目前使用的量度數量。 |
| **[!UICONTROL 使用狀況%]** | 目前使用中的授權值百分比。 |
| **[!UICONTROL 預計使用量%]** | 未來6週內量度使用的預測範圍。 |

使用&#x200B;**[!UICONTROL 生產]**&#x200B;或&#x200B;**[!UICONTROL 開發]**&#x200B;沙箱切換來篩選沙箱顯示的量度。

>[!NOTE]
>
>消耗報告是依沙箱型別的累計。 選取[!UICONTROL 生產]或[!UICONTROL 開發]會顯示該型別所有沙箱的組合使用情形。

![授權使用儀表板[量度]索引標籤會顯示量度、授權金額和使用量資料的清單。](../images/license-usage/metrics-tab.png)

>[!WARNING]
>
>必須在沙箱層級指定檢視授權使用儀表板的許可權。 新增許可權至每個個別沙箱，以在控制面板中檢視它們。 此限制將在未來版本中解決。 同時，提供下列因應措施：
>
>1. 在Adobe Admin Console中建立產品設定檔。
>2. 在沙箱類別的許可權下，新增您想在授權使用儀表板中檢視的所有沙箱。
>3. 在「使用者儀表板許可權」類別下方，新增「檢視授權使用儀表板」許可權。

### 檢視量度詳細資訊 {#view-metric-details}

若要檢視特定測量結果的使用狀況詳細資訊，請在清單中選取測量結果名稱。 此時會出現量度的詳細檢視，包括：

- 顯示一段時間使用情況的歷史折線圖
- 授權值與測量值的比較
- 依個別沙箱的使用情況
- 用於篩選資料的沙箱選擇器
- CSV下載的匯出選項

此視覺效果可讓您追蹤趨勢、瞭解每個沙箱對整體使用量的貢獻，並匯出資料以供離線分析。

每個圖表都包含用於篩選資料的下拉式選單。 使用日期範圍下拉式清單來調整回顧期間（預設值：過去30天），或使用沙箱下拉式清單來檢視特定生產或開發沙箱的使用量。

![包含歷史使用圖形、沙箱表格和匯出按鈕的「可定址對象」量度詳細資料檢視。](../images/license-usage/metric-details-view.png)

您也可以選取&#x200B;**[!UICONTROL 自訂日期]**&#x200B;以選擇顯示的時段。

![授權使用儀表板的[概觀]索引標籤中反白顯示自訂日期範圍選項。](../images/license-usage/custom-date-range.png)

### CSV匯出 {#export-metric-usage-data}

您可以直接從量度詳細資料檢視，將所選量度和沙箱的歷史使用資料匯出為CSV檔案。 選取&#x200B;**[!UICONTROL 匯出]**&#x200B;圖示，以表格格式下載圖表資料。 匯出的CSV可讓您輕鬆離線分析趨勢，或在團隊之間分享使用見解。

## [!UICONTROL 產品]索引標籤 {#products-tab}

**[!UICONTROL Products]**&#x200B;索引標籤顯示依購買的產品和任何相關附加元件分組的授權使用資料。 [!UICONTROL Products]索引標籤包含兩個表格：

- **[!UICONTROL 核心產品]表格**：此表格列出貴組織授權的主要Adobe Experience Platform產品。 每個產品都列出其主要量度、使用追蹤和預測使用。
- **[!UICONTROL 附加元件]資料表**：列出授權金額對核心產品量度有貢獻的附加專案。 附加元件沒有獨立的量度，但可加強對相關核心產品的使用追蹤。

| 欄名稱 | 說明 |
|---|---|
| **[!UICONTROL 產品]** | 您的組織授權的Adobe解決方案。 |
| **[!UICONTROL 主要量度]** | 該產品中用於追蹤的主要量度。 |
| **[!UICONTROL 授權金額]** | 主要量度最大量的約定值。 |
| **[!UICONTROL 使用狀況]** | 您使用的主要量度數量。 |
| **[!UICONTROL 使用狀況%]** | 根據您的授權數量使用的主要量度百分比。 |
| **[!UICONTROL 預計使用量]** | 主要量度的預測使用百分比。 |

>[!NOTE]
>
>附加元件的[!UICONTROL 授權金額]包含在核心產品的授權總金額中。 系統不會個別追蹤附加元件，但會增強其相關產品的功能。 例如，如果您購買一包5個沙箱作為附加元件，則金額會加入基本產品的金額中。 附加元件表格顯示附加元件特定的[!UICONTROL 授權金額]，但實際使用量會透過基礎產品追蹤。

![授權使用儀表板產品索引標籤，包含核心產品和附加元件的表格。](../images/license-usage/products-tab.png)

### 預估使用量 {#predicted-usage}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="預估使用量"
>abstract="根據過去 6 至 7 個月的使用量進行預估，並每週一次於星期五產生預估結果。請注意，授權用量預估是根據過去使用量計算的近似值。您有責任了解組織的實際使用量，並確保使用量不會超過組織獲得 Adobe 授權的範圍。若要減少使用量，您可以針對沙箱和資料集設定資料集或匿名設定檔的資料過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="自動化資料集期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

>[!CONTEXTUALHELP]
>id="platform_licenseusage_prediction"
>title="預估使用量"
>abstract="根據過去 6 至 7 個月的使用量進行預估，並於每月 15 日產生預估結果。請注意，授權用量預估是根據過去使用量計算的近似值。您有責任了解組織的實際使用量，並確保使用量不會超過組織獲得 Adobe 授權的範圍。若要減少使用量，您可以針對沙箱和資料集設定資料集或匿名設定檔的資料過期時限。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="自動化資料集期限"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="匿名設定檔資料期限"

透過準確且最新的使用預測，主動管理並最佳化您的授權資源。 [!UICONTROL 預計使用量]欄預測所有已購買產品的所有生產及開發沙箱中沙箱層級的未來授權使用量。 預測現在每週更新，根據最新使用資料提供六週預測。 每個預測都包含上下限，以支援明智的規劃。

>[!IMPORTANT]
>
>預測每週五都會重新整理。 重新整理的日期包含在資訊圖示中(![此資訊圖示。](../images/license-usage/info-icon.png))在欄標題上方。

從[!UICONTROL 核心產品]資料表下的[!UICONTROL 產品]索引標籤，檢視產品的權益使用摘要。

![產品及預測使用量資料行醒目提示的[!UICONTROL 授權使用量] [!UICONTROL 產品]標籤。](../images/license-usage/product-predicted-usage.png)

>[!NOTE]
>
>請注意，授權用量預估是根據過去使用量計算的近似值。您有責任瞭解貴組織的實際使用情況，並確保使用情況不會超出貴組織使用Adobe的授權範圍。

預計使用量的百分比取決於以下因素：

- 如果上下界限明顯不同，則會顯示為範圍（例如32% - 35%）。
- 如果上下界限幾乎完全相同且不為零，則會顯示為近似值（例如，~34%）。
- 如果上下界限幾乎完全相同且為0，則會顯示為0%。

>[!NOTE]
>
>在此上下文中，「幾乎相同」表示值對於小數點兩位數的統計顯著性（例如，0.342的下限和0.344的上限都會四捨五入為34%）。

預測的使用量功能支援下列量度：

- [!UICONTROL 可定址對象]
- [!UICONTROL 商務人員設定檔]
- [!UICONTROL 計算時數]
- [!UICONTROL 客戶歷程對象列數]
- [!UICONTROL 可參與的設定檔]
- [!UICONTROL 資料磁碟區總數]

## 可用量度 {#available-metrics}

>[!IMPORTANT]
>
>自8月20日起，擁有&#39;[!UICONTROL 平均設定檔豐富度]&#39;和&#39;[!UICONTROL 總儲存空間]&#39;許可權的客戶在授權使用儀表板中看到&#39;[!UICONTROL 總資料量]&#39;。 客戶權益沒有變動，只是追蹤量度的簡化。 [!UICONTROL 總資料量]代表即時客戶個人檔案中可供參與和個人化工作流程使用的資料。 此簡化量度改善了即時客戶個人檔案使用的管理和測量。 我們鼓勵客戶連絡其Adobe代表，進一步釐清這項變更。

授權使用儀表板會報告適用於組織中多個產品的多個不重複量度。 可用的量度包括：

| 量度 | 說明 |
|---|---|
| [!UICONTROL Audience Activation大小] | 一年內針對任何基於檔案的目的地所啟用的輪廓總大小。注意：這不包括透過串流目的地所傳送的輪廓。 |
| [!UICONTROL 可定址對象] | 您的組織有權參與的即時客戶個人檔案中的人員個人檔案集，包括直接可識別的和假名個人檔案。 這些設定檔可能包含屬性、行為和區段成員資格資料。 設定檔磁碟區是使用Adobe Experience Platform的預設確定性身分圖表來計算，且視為共用功能。 |
| [!UICONTROL Adhoc Query Service使用者套件] | 此附加元件可增加您的已授權並行查詢服務使用者權益，每個套組可增加五個額外的並行查詢服務使用者和一個額外的並行執行的臨時查詢。可以授權多個額外的臨時查詢使用者套組。 |
| [!UICONTROL 平均設定檔豐富度] | **已棄用** — 任何時間點儲存在集線器設定檔服務中的所有生產資料總和，除以授權企業人員設定檔數目的五倍。 [!UICONTROL 平均設定檔豐富度]是共用功能。 |
| [!UICONTROL 可用的CJA資料列] | Customer Journey Analytics 內可供分析的每日平均資料列數。 |
| [!UICONTROL 計算屬性] | 根據體驗事件的彙總設定檔行為資料，這些體驗事件會轉換為設定檔屬性，並可包含在個人設定檔中。 |
| [!UICONTROL 消費者對象] | 銷售訂單上識別為「消費者對象」的個人設定檔數目。 |
| [!UICONTROL 資料匯出大小] | 一年內透過資料集啟用所傳送的資料量。 |
| [!UICONTROL 資料匯出] | 一年內可匯出至任何非 Adobe 解決方案 (直接或間接) 的資料集總大小。 |
| [!UICONTROL 資料湖儲存空間] | Adobe Experience Platform 內分析資料存放區的使用數量。 |
| [!UICONTROL 可參與的對象] | 即時客戶設定檔中的一組人員設定檔，您在過去12個月內嘗試使用Journey Optimizer的編寫、決策、傳送、實驗或協調功能與其互動。 |
| [!UICONTROL 相似對象] | 消費者相似對象是透過模型化現有消費者對象來產生的對象，以識別具有類似屬性或行為的個人設定檔。 |
| [!UICONTROL 個AMM模型] | 用於根據您的投資來測量和/或預測指定結果的機器學習模型 (內建於 Adobe Mix Modeler) 的計數。 |
| [!UICONTROL 沙箱數目] | 存取 Adobe Experience Platform 的任何 Adobe 隨選服務執行個體內隔離資料和作業的邏輯分區計數。 |
| [!UICONTROL 設定檔豐富度（Pack數目）] | 對於每個額外的輪廓豐富度套組，每個輪廓的授權總資料量將增加 25KB。 |
| [!UICONTROL 查詢服務計算時數] | 在執行批次查詢時，查詢服務引擎讀取、處理資料並將資料寫入資料湖所花費的時間量測量。 |
| [!UICONTROL 串流區段數Pack] | 當新資料透過串流資料流進入細分服務時，套組便會更新人員輪廓的細分群體會籍。細分群體會籍是根據目前的人員輪廓屬性和目前的事件值進行評估，而不考慮歷史行為。串流細分是一項共用功能。 |
| [!UICONTROL 資料磁碟區總數] | 可用於參與工作流程中的即時客戶個人檔案的總資料量。 如需瞭解詳細資訊，請參閱關於總資料量](../../landing/license-usage-and-guardrails/total-data-volume.md)的[常見問題。 |
| [!UICONTROL 資料輸出總量] | 從Adobe Experience Platform匯出至第三方資料倉儲的累積年度資料量。 |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

>[!TIP]
>
>您可以檢查銷售訂單中的授權權益，以計算量度，例如「儲存空間津貼」。<br>例如，<ul><li>儲存容量=合約中「授權設定檔」的數量X平均設定檔豐富度</li></ul>

這些量度的可用性，以及每個量度的特定定義，會因貴組織已購買的授權而有所不同。 如需每個量度的詳細定義，請參閱適當的產品說明檔案：

| 授權 | 產品說明 |
| --- | --- |
| <ul><li>Adobe Experience Platform：OD LITE</li><li>Adobe Experience Platform：OD STANDARD</li><li>Adobe Experience Platform：OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform：OD</li></ul> | [Experience Platform、應用程式服務和智慧型服務](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT客戶資料平台：OD</li><li>RT CUSTOMER DATA PLATFORM：OD PRFL至10M</li><li>RT客戶資料平台：OD PRFL至50M</li></ul> | [Adobe Real-Time Customer Data Platform](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP：OD啟用</li><li>AEP：OD啟用PRFL至10M</li><li>AEP：OD啟用PRFL，最高50米</li></ul> | [Adobe Experience Platform啟用](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP：OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>Journey Optimizer SELECT：OD</li><li>Journey Optimizer PRIME：OD</li><li>Journey Optimizer ULTIMATE：OD</li><li>UNP AJO PRIME簡易版：OD</li><li>UNP AJO ULTIMATE簡易版：OD</li><li>UNP Real-Time CDP：OD設定檔協調流程</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/tw/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>授權使用儀表板只會報告貴組織已布建的最新授權。 如果貴組織布建的最新授權未出現在上表中的話，授權使用儀表板可能無法正確顯示。 計畫在未來的版本中，支援單一組織中的其他授權和多個授權。

## 後續步驟

閱讀本檔案後，您可以找到授權使用儀表板，並檢視每個已購買產品、所有生產或開發沙箱以及特定沙箱的使用量度。 您可以根據貴組織已購買的授權，找到更多有關貴組織可用量度的資訊。

若要進一步瞭解Experience Platform UI中可用的其他功能，請參閱[Experience Platform UI指南](../../landing/ui-guide.md)。
