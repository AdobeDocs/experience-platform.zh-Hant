---
title: Adobe Experience Platform中的AI助理概述
description: 瞭解AI Assistant、其細微差別和使用案例，以及如何使用它來加快您與Adobe Experience Platform和Real-time Customer Data Platform的工作流程。
source-git-commit: dd3a7d07c0c78d76c552affef892d5e5c0f0bfb5
workflow-type: tm+mt
source-wordcount: '2371'
ht-degree: 0%

---

# Adobe Experience Platform中的AI助理

請閱讀本檔案，瞭解Adobe Experience Platform中的AI助理。

Adobe Experience Platform中的AI助理是一種對話式體驗，可用來加速Adobe應用程式中的工作流程。 您可以使用AI Assistant來進一步瞭解產品知識、疑難排解問題，或搜尋資訊並尋找營運見解。 AI助理支援Experience Platform、Real-time Customer Data Platform、Adobe Journey Optimizer和Customer Journey Analytics。

>[!IMPORTANT]
>
>* 您必須同意 [使用者協定](https://adobe.sharepoint.com/:w:/s/ExCUserExperience/EVzJv1jFBiZGnaFEufsfIqwBC_9ehv3KaXTkEMTGpQFRpg?e=qzwOo8) 才能使用AI助理。 使用者合約也包含公開測試版合約。 這樣一來，您就可以在以Beta版容量推出其他AI Assistant功能時使用它們。

![首次觸發使用者體驗的AI助理介面。](./images/blank.png)

## 瞭解AI助理 {#understanding-ai-assistant}

AI Assistant會查詢資料庫，然後將資料庫中的資料轉譯成人類看得懂的答案，以回應您提交的問題。

這種基礎資料的內部表示法也稱為 **[!DNL Knowledge Graph]**  — 特定答案的概念、資料和中繼資料的完整網路。

此 [!DNL Knowledge Graph] 由每次提交查詢時參考的子圖表組成：

* 客戶營運分析。
* 各種中繼商店的客戶營運分析。
* Experience League檔案。

在查詢AI Assistant之前，需要考慮兩種型別的問題：

### 產品知識 {#product-knowledge}

產品知識是以Experience League檔案為根據的概念和主題。 產品知識問題可進一步指定到下列子群組中：

| 產品知識 | 範例 |
| --- | --- |
| 點式學習 | <ul><li>身分識別與主要或外部索引鍵之間有何差異？</li><li>如何計算設定檔豐富度？</li></ul> |
| 開啟探索 | <ul><li>如何匯出此資料集？</li><li>是否有適用於醫療保健客戶的結構描述？</li></ul> |
| 疑難排解 | <ul><li>為什麼我無法為設定檔開啟Adobe擁有的結構描述？</li><li>我為何刪除不了區段？</li></ul> |

{style="table-layout:auto"}

### 營運分析 {#operational-insights}

>[!IMPORTANT]
>
>營運見解答案為測試版。 任何可存取此 **檢視營運分析** 許可權將可存取操作見解答案。

營運深入分析是指回答AI助理產生的中繼資料物件（屬性、受眾、資料流、資料集、目的地、歷程、結構描述和來源），包括計數、查閱和歷程影響。 它不會檢視沙箱中的任何資料。

* 我有多少資料集？
* 有多少結構描述屬性從未使用過？
* 已啟用哪些對象？

您可以在下列網域中向AI Assistant詢問有關您的營運見解的問題：

* 屬性
* 對象
* 資料流
* 資料集
* 目的地 _（關於帳戶的問題和資料流的一些問題目前無法回答。）_
* 歷程
* 方案 _（目前無法回答有關欄位群組的問題。）_
* 來源 _（目前無法回答有關帳戶的問題。）_

若是操作見解問題，答案可能不會反映UI的目前狀態。 支援這些問題的資料每24小時更新一次。 例如，使用者白天在Real-Time CDP中所做的變更會在夜間與資料存放區同步，然後早上就可供使用者提問。 您需要登入沙箱以查詢與物件相關的特定資料。

### 功能範圍 {#feature-scope}

目前，AI助理的範圍如下：

* [產品知識](./home.md#product-knowledge)： AI助理可以回答Experience Platform、Real-time Customer Data Platform和Adobe Journey Optimizer的產品知識問題。 您也可以深入探討Customer Journey Analytics的產品知識主題，但必須透過Customer Journey AnalyticsUI。
* [營運分析](./home.md#operational-insights)：您可以向AI助理詢問有關下列資料物件的操作深入分析的問題：屬性、受眾、資料流程、資料集、目的地、歷程、結構描述和來源。

## 功能存取 {#feature-access}

對AI助理的存取受下列引數控制：

* **存取應用程式：** 您可以在Adobe Experience Platform、Adobe Real-Time CDP、Adobe Journey Optimizer中存取AI助理 [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
* **合約存取：** 貴公司必須同意特定的 [!DNL GenAI] — 相關法律條款，您的組織才能使用AI助理。 如果您無法存取AI助理，請聯絡貴組織的管理員或您的Adobe帳戶團隊。
* **許可權：** 使用 [許可權UI](../access-control/abac/ui/permissions.md) 來授予或撤銷貴組織中AI Assistant的存取權。 為了使用AI助理，指定的使用者必須屬於以布建的角色 **啟用AI助理** 和 **檢視營運分析** 許可權。
   * 身為管理員，您可以新增 **啟用AI助理** 並新增使用者至該角色，讓他們可存取您組織中的AI助理。
   * 身為管理員，您可以新增 **檢視營運分析** 將使用者新增至指定角色，讓他們能夠使用AI助理的作業深入分析功能。 營運見解目前處於Beta版。

![許可權UI頁面具有給定角色中包含的啟用AI助理和檢視操作深入分析許可權。](./images/permissions.png)

## 範例問題 {#example-questions}

本節概述您可在工作流程中參考的範例問題。 問題分為三個部分：營運見解、目標和物件。

### 按營運見解分組的範例問題 {#operational-insights-questions}

+++選取以檢視營運分析問題的範例及其各自的使用案例：

| 問題型別 | 使用案例 | 範例 |
| --- | --- | --- | 
| 資料譜系 | 追蹤其他Experience Platform物件中一或多個物件的使用情況 | <ul><li>哪些資料集使用「ACME結構描述」結構描述？</li><li>使用相同結構描述擷取了多少資料集？</li><li>啟用的受眾中使用了哪些資料集？</li><li>列出具有用於已啟動受眾之屬性的結構描述。</li><li>顯示啟用至「ACME目的地」且有1000多個設定檔的對象。</li><li>顯示啟用對象中所使用的屬性，這些對象在2023年1月之後已修改。</li><li>透過「ACME Amazon S3」來源擷取的資料集是什麼？</li><li>哪些資料流與「ACME忠誠度資料流」相關聯？</li><li>列出與啟用的對象相關且建立於過去1年的結構描述。</li></ul> |
| 分佈與彙總 | 關於Experience Platform物件使用情況的摘要式問題 | <ul><li>啟用的對象百分比為何？</li><li>區段中使用了多少欄位？</li><li>哪些對象啟用的目的地數量最多？</li><li>列出重複的對象。</li><li>顯示啟用至「ACME目的地」的受眾，並按設定檔大小排名。</li><li>尚未啟用但擁有超過100個設定檔的對象百分比為何？ 顯示他們的姓名。</li><li>列出將資料擷取到我的資料集中的3個來源聯結器。</li><li>根據啟用對象的發生次數，列出前5個用於啟用對象的屬性。</li></ul> |
| 物件查詢 | 擷取或存取Experience Platform物件或其屬性。 | <ul><li>哪些資料集沒有任何相關聯的結構描述</li><li>列出用於「ACME對象」的屬性？</li><li>給我已啟用設定檔但自建立以來未修改的結構描述清單。</li><li>上週修改了哪些對象？</li><li>列出具有相同區段定義的對象及其建立日期。</li><li>哪些資料集已啟用設定檔，並且包括已從每個資料集建立多少對象。</li><li>哪些來源帳戶與資料集XYZ相關聯？</li><li>顯示「ACME對象」的區段定義和修改日期。</li></ul> |
| 物件比較 | 識別重複的對象。 | <ul><li>根據其區段定義，列出重複的對象。</li><li>啟用至「ACME目的地」的重複受眾。</li></ul> |

{style="table-layout:auto"}

+++

### 按目標分組的範例問題 {#objectives-questions}

+++選取此選項可檢視您可以使用AI助理完成的目標清單

| 目標 | 說明 | 範例 |
| --- | --- | --- |
| 學習概念和持續工作流程 | <ul><li>身為新手使用者，您可以使用AI Assistant來瞭解Real-Time CDP和Adobe Journey Optimizer概念，並且將自己帶入你不熟悉的產品和功能。</li><li>身為經驗豐富的使用者，您可以使用AI Assistant來解決可能阻礙您工作流程的邊緣案例。 | <ul><li>如何在Journey Analytics中設定儀表板？</li><li>告訴我一些Real-Time CDP的使用案例。</li></ul> |
| 疑難排解 | 使用AI助理瞭解如何偵錯工作流程中可能遇到的基本錯誤。 | <ul><li>發生此錯誤的原因 {ERROR_MESSAGE} 平均值？</li><li>我為何無法刪除名為「Luma：電子郵件對象」的對象？</li></ul> |
| 沙箱衛生 | 使用AI助理來識別任何重複專案或未使用的物件，以便您能夠有效地維護您的沙箱。 | <ul><li>您可以顯示類似的對象嗎？</li><li>是否有任何沒有關聯資料集的結構描述？</li></ul> |
| 值分析 | 使用AI助理可以識別您最常用的資料物件，並評估任何績效指標或尋找最有價值的資料物件。 | <ul><li>我們的「Luma：電子郵件對象」區段定義中有多少設定檔？</li><li>對象何時啟用以Experience Cloud對象目的地？</li></ul> |
| 搜尋 | 使用AI助理來尋找支援的Experience Platform物件，例如對象、資料集、目的地、結構描述和來源。 | <ul><li>列出在上季建立的名稱中包含「Luma」的對象。</li><li>「Luma：自訂動作」XDM結構描述中有哪些屬性？</li></ul> |
| 影響分析 | 使用AI助理來識別某些工作流程中使用的資料物件，以便您評估任何變更的影響。 | <ul><li>使用哪些對象 `homeAddress.city` 在「Luma：PersonProfiles」結構描述中？</li><li>哪些資料集是 `consents.marketing.push.val` 設定檔屬性儲存在中？</li></ul> |

{style="table-layout:auto"}

+++

### 依物件分組的範例問題 {#objects-questions}

+++選取此選項可檢視AI助理可以協助您的範例問題清單：

| 物件 | 說明 |
| --- | --- |
| 受眾 — 營運深入分析 | <ul><li>哪些對象使用其他對象？</li><li>不同對象中的設定檔數量分佈情況如何？</li><li>顯示上次修改的對象 {RELATIVE_DATE}.</li><li>哪些對象有0個設定檔？</li><li>是 {USE_AUTOCOMPLETE_TO_FILL_AUDIENCE_NAME} 用於任何其他對象？</li></ul> |
| 屬性 — 營運深入分析 | <ul><li>哪些對象具有XDM屬性 {ATTRIBUTE_PATH} 在他們的區段定義中？</li><li>有多少個XDM結構描述屬性未用於任何受眾？</li><li>哪些結構描述具有XDM屬性 {ATTRIBUTE_PATH} 在裡面？</li><li>會啟用哪些XDM屬性？</li><li>具有超過10個設定檔的對象會使用哪些XDM屬性</li></ul> |
| 資料流 — 營運深入分析 | <ul><li>哪些資料流參與 {DATASET_NAME} 資料集？</li><li>未使用哪些來源資料流，或是哪些資料不再流入？</li><li> |
| 資料集 — 營運深入分析 | <ul><li>使用相同結構描述擷取了多少資料集？</li><li>與哪個來源聯結器相關聯 {DATASET_NAME} 資料集></li><li>每個對象會使用哪些資料集？</li><li>哪些結構描述沒有用於任何資料集？</li><li>我有多少資料集？</li></ul> |
| 目的地 — 營運深入分析 | <ul><li>哪些目的地處於作用中狀態？</li><li>哪些目的地帳戶已啟用0個對象？</li><li> |
| 歷程 — 營運深入分析 | <ul><li>我有多少個歷程？</li><li>已在哪些歷程中建立 {RELATIVE_DATE} （例如上週）或 {RELATIVE_DATE} （例如特定日期之前/之後/當天）？</li><li>顯示在中修改的歷程清單 {RELATIVE_DATE} （例如上週）或 {RELATIVE_DATE} （例如特定日期之前/之後/當天）？</li><li>列出我的歷程。</li><li>列出即時歷程中使用的對象。</li></ul> |
| 結構描述 — 營運深入分析 | <ul><li>哪些結構描述的欄位貢獻了最多的受眾？</li><li>設定檔已啟用多少個結構描述？</li><li>列出上週修改的所有結構描述。</li><li>哪些結構描述沒有用於任何資料集？</li><li>列出上週建立的所有結構描述。</li></ul> |
| 來源 — 營運分析 | <ul><li>哪些來源處於作用中狀態？</li><li>哪個來源聯結器與資料集相關聯 {DATASET_NAME}？</li><li>哪個來源聯結器具有最高數目的關聯帳戶？</li><li>顯示資料流及其關聯的來源聯結器。</li></ul> |
| 直接學習 — 產品知識(Real-Time CDP和Journey Optimizer) | <ul><li>AI助理可以提供哪些協助？</li><li>哪些對象具有相似性？</li><li>使用者群組與角色有何關係？</li><li>何時應使用資料型別與欄位群組？</li><li>身分識別與主要或外部索引鍵之間有何差異？</li><li>如何計算設定檔豐富度？</li></ul> |
| 疑難排解 — 產品知識(Real-Time CDP和Journey Optimizer) | <ul><li>AI助理可以提供哪些協助？</li><li>我可以在擷取資料後刪除已啟用設定檔的結構描述嗎？</li><li>我為何刪除不了對象？</li><li>評估對象和鎖定目標結果需要多久時間？</li></ul> |

{style="table-layout:auto"}

+++

## 用詞說明問題 {#phrasing-your-questions}

您必須用清楚和具體的語境向AI Assistant提問，才能儘可能獲得準確的回應。 請參閱下列提示清單，以取得如何透過內容提出明確問題的指引：

* 以簡明的方式陳述您的任務和/或問題。
* 避免使用含糊不清的語言或過於複雜的語法，以方便理解。
* 提供有關您任務和/或問題的相關內容，因為內容可協助AI助理產生更相關的回應。

請閱讀下表，深入瞭解向AI助理提出問題時應遵循的最佳實務。

+++選取以檢視在提出問題時遵循的最佳實務範例

| 執行 | 範例 |
| --- | --- |
| <ul><li>請指定要擷取或分析的物件或資訊的特定資訊。</li><li>請嘗試將資料物件名稱放在引號中。 如果您只知道物件名稱的一部分，您也可以在問題中指定。</li><li>使用 [物件自動完成](./ui-guide.md#use-auto-complete) 以協助AI助理更清楚瞭解您的查詢內容。</li></ul> | <ul><li>哪些資料集使用「Luma — 忠誠度」方案？</li><li>顯示名稱中有「Luma」的已啟動區段。 依設定檔計數對其排名。</li></ul> |
| <ul><li>避免模稜兩可，使用清楚的語言</li><li>使用精確術語，確保查詢內容更清楚。</li><li>在詢問有關Adobe Experience Platform的問題時，請嘗試使用Experience Platform的特定術語，以改善回應的相關性。</li></ul> | <ul><li>「ACME對象」中有多少個設定檔。</li><li>顯示啟用的對象中使用的前5大XDM屬性。</li></ul> |
| <ul><li>提供內容或指定條件以篩選結果。</li><li>在問題中使用篩選條件來限制回應中的資料量。</li></ul> | <ul><li>顯示尚未啟用且建立日期超過6個月且從未修改過的對象。</li><li>向我顯示啟用至「ACME目的地」且擁有超過10000個設定檔的對象。</li></ul> |

{style="table-layout:auto"}

| 不要 | 範例 |
| --- | --- |
| 使用模糊或不明確的語言。 | <ul><li>提供資料集的相關資訊。</li><li>「ACME對象」中有多少位使用者？</li><li>顯示區段。</li><li>清單屬性。</li></ul> |
| 提出不完整的請求。 | 「Luma — 忠誠度資料集」 |
| 假設知識沒有上下文。 | <ul><li>過去6個月的對象。</li><li>為我建立查詢。</li></ul> |
| 制定過於複雜的查詢。 | 提供跨所有物件及其相依性之資料譜系的全面分析。 |
| 省略條件或引數。 | 顯示資料集。 |

{style="table-layout:auto"}

+++

## 後續步驟

現在您已大致瞭解AI助理，您可以繼續並在工作流程中使用AI助理。 如需詳細資訊，請參閱下列檔案：

* [AI助理使用者介面指南](./ui-guide.md)
* [AI助理的隱私權、安全性和控管](./privacy.md)
* [常見問題集](./faq.md)