---
keywords: Experience Platform；首頁；資料科學工作區；熱門主題；資料科學工作區；資料科學
solution: Experience Platform
title: Data Science Workspace概述
topic-legacy: overview
description: 本指南概述Adobe Experience Platform中Data Science Workspace的相關重要概念。
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 0%

---

# Data Science Workspace概觀

Adobe Experience Platform [!DNL Data Science Workspace] 使用機器學習和人工智慧，釋放資料的深入見解。 整合至Adobe Experience Platform, [!DNL Data Science Workspace] 可協助您跨Adobe解決方案使用內容和資料資產進行預測。

所有技能級別的資料科學家都將找到複雜、易於使用的工具，以支援機器學習方法的快速開發、培訓和調整 — AI技術的所有好處，而不存在複雜性。

使用 [!DNL Data Science Workspace]，資料科學家可輕鬆建立由機器學習提供技術支援的智慧服務API。 這些服務可與其他Adobe服務(包括Adobe Target和Adobe Analytics Cloud)搭配使用，協助您在網頁、案頭和行動應用程式中，自動化個人化、鎖定目標的數位體驗。

本指南概述與 [!DNL Data Science Workspace].

## 簡介

今天的企業將挖掘大資料作為高度優先事項，以便進行預測和洞察，幫助他們個性化客戶體驗，為客戶和業務提供更多價值。
同樣重要的是，從資料獲取見解可能需要付出高昂的成本。 通常，需要技術嫻熟的資料科學家進行密集且耗時的資料研究，以開發支援智慧服務的機器學習模型或配方。 這個過程耗時長，技術複雜，而熟練的資料科學家可能很難找到。

使用 [!DNL Data Science Workspace], Adobe Experience Platform可讓您將以體驗為中心的AI整合到整個企業中，透過以下功能簡化並加速資料轉化為深入分析的程式碼：
- 機器學習框架和運行時
- 整合存取儲存在Adobe Experience Platform中的資料
- 基於的統一資料架構 [!DNL Experience Data Model] (XDM)
- 機器學習/人工智慧和管理大資料集所需的計算能力
- 預先建立的機器學習訣竅，加速向人工智慧驅動體驗的飛躍
- 為不同技能級別的資料科學家簡化編寫、重複使用和修改配方
- 只需按幾下即可發佈和共用智慧服務（無需開發人員），並監控和再培訓，以持續最佳化個人化客戶體驗

所有技能水準的資料科學家都能更快地獲得見解，並更有效地實現數位體驗。

## 快速入門

在了解 [!DNL Data Science Workspace]，主要術語的摘要如下：

| 詞語 | 定義 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] with [!DNL Experience Platform] 讓客戶能夠利用資料建立機器學習模型 [!DNL Experience Platform] 和Adobe解決方案，產生智慧型深入分析和預測，打造令人愉悅的最終使用者數位體驗。 |
| 人工智慧 | 人工智慧是電腦系統的理論和發展，能夠執行通常需要人類智慧的任務，如視覺感知、語音識別、決策和語言之間的翻譯。 |
| 機器學習 | 機器學習是研究領域，它使電腦能夠學習而不被明確寫程式。 |
| [!DNL Sensei] ML框架 | [!DNL Sensei] ML Framework是跨Adobe的統一機器學習框架，可利用 [!DNL Experience Platform] 以更快、可擴展和可重複使用的方式，在開發機器學習驅動的智慧服務時增強資料科學家的能力。 |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM)是依Adobe主導的標準化工作，用來定義標準結構，例如 [!DNL Profile] 和 [!DNL ExperienceEvent]，以管理客戶體驗。 |
| [!DNL JupyterLab] | [!DNL JupyterLab] 是專案Jupyter的開放原始碼網頁型介面，並緊密整合至 [!DNL Experience Platform]. |
| 訣竅 | 配方是模型規範的Adobe術語，是表示特定機器學習、AI算法或整合演算法、處理邏輯和配置的頂級容器，用於構建和執行受訓模型，從而幫助解決特定業務問題。 |
| 模型 | 模型是機器學習方式的例項，會使用歷史資料和設定進行訓練，以針對業務使用案例進行解析。 |
| 訓練 | 培訓是學習模式和從標籤資料中洞察資訊的過程。 |
| 訓練模型 | 訓練模型表示模型訓練過程的可執行輸出，其中一組訓練資料被應用到模型實例。 經過訓練的模型將保留對任何從中建立的智慧Web服務的引用。 訓練後的模型適用於評分和建立智慧Web服務。 對已訓練模型的修改可視為新版本來追蹤。 |
| 分數 | 計分是使用經過訓練的模型，從資料產生深入分析的程式。 |
| 服務 | 已部署的服務會透過API公開人工智慧、機器學習模型或進階演算法的功能，以便可供其他服務或應用程式使用，以建立智慧應用程式。 |

下圖概述方式、模型、培訓執行和計分執行之間的階層關係。

![](./images/home/recipe_hiearchy_ui.png)

## 瞭解 [!DNL Data Science Workspace]

使用 [!DNL Data Science Workspace]，您的資料科學家就能簡化揭露大型資料集深入分析的繁瑣程式。 構建於通用的機器學習框架和運行時， [!DNL Data Science Workspace] 提供高級的工作流管理、模型管理和可擴充性。 智慧服務支援重新使用機器學習方法，以支援使用Adobe產品和解決方案建立的各種應用程式。

### 一站式資料存取

資料是人工智慧和機器學習的基石。

[!DNL Data Science Workspace] 已與Adobe Experience Platform完全整合，包括Data Lake, [!DNL Real-Time Customer Profile]，和 [!DNL Unified Edge]. 一次探索儲存在Adobe Experience Platform中的所有組織資料，以及常見的大資料和深層學習程式庫，例如 [!DNL Spark] ML和 [!DNL TensorFlow]. 如果您找不到所需內容，請使用XDM標準化結構擷取自己的資料集。

### 預先建立的機器學習訣竅

[!DNL Data Science Workspace] 包括符合常見業務需求的預先建立機器學習秘訣，例如零售銷售預測和異常偵測，因此資料科學家和開發人員不必從頭開始。 目前有三種配方， [產品購買預測](./pre-built-recipes/product-purchase-prediction.md), [產品建議](./pre-built-recipes/product-recommendations.md)，和 [零售銷售](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

您可以視需要調整預先建立的方式、匯入方式，或從頭開始建立自訂方式。 不過，一旦您開始訓練並超調配方，建立自訂智慧服務就不需要開發人員，只需按幾下滑鼠，您就可以建立目標式個人化數位體驗。

### 以資料科學家為重點的工作流程

無論您具備何種資料科學專業知識， [!DNL Data Science Workspace] 有助於簡化及加速尋找資料深入分析並將其套用至數位體驗的程式。

### 資料探索

找到正確的資料並準備好資料，是構建有效方法中最耗費人力的部分。 [!DNL Data Science Workspace] 而Adobe Experience Platform可協助您更快從資料獲得深入分析。

在Adobe Experience Platform上，您的跨管道資料會集中儲存在XDM標準結構中，因此資料更容易尋找、理解和清除。 以通用結構為基礎的單一資料儲存，可為您節省無數的資料探索和準備時間。

瀏覽時，使用R [!DNL Python]，或透過整合、托管 [!DNL Jupyter Notebook] 瀏覽上的資料目錄 [!DNL Platform]. 使用其中一種語言，您也可以 [!DNL Spark] ML和TensorFlow。 從頭開始，或使用為特定業務問題提供的筆記型電腦模板之一。

在資料探索工作流程中，您也可以內嵌新資料或使用現有功能來協助資料準備。

### 製作

使用 [!DNL Data Science Workspace]，您可以決定要如何製作食譜。

- 瀏覽滿足您業務需求的預建方式，節省時間，您可依原樣使用或設定，以符合您的特定需求。
- 從頭建立配方，使用Jupyter筆記型電腦中的製作執行階段來開發和註冊配方。
- 將在Adobe Experience Platform以外製作的方式上傳至 [!DNL Data Science Workspace] 或從存放庫匯入方式代碼，例如 [!DNL Git]，使用之間的驗證和整合 [!DNL Git] 和 [!DNL Data Science Workspace].

### 實驗

Data Science Workspace為實驗程式提供極大的彈性。 從你的食譜開始。 然後使用與獨特特性（例如超調參數）配對的相同核心演算法，建立個別例項。 您可以建立任何需要的例項，並訓練每個例項並評分任意次數。 當你訓練他們時， [!DNL Data Science Workspace] 追蹤方式、方式例項和訓練的例項，以及評估量度，因此您不需要。

### 操作化

當您對食譜感到滿意時，只需按幾下即可建立智慧服務。 無需編碼 — 您可以自行完成，無需邀請開發人員或工程師。 最後，將智慧服務發佈到AdobeIO，您的數位體驗團隊就可以使用它了。

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### 持續改進

[!DNL Data Science Workspace] 跟蹤調用智慧服務的位置及其執行方式。 當資料滾入時，您可以評估智慧服務準確度以關閉回圈，並視需要重新訓練配方以改善效能。 結果是客戶個人化的精確度持續提高。

### 存取新功能和資料集

資料科學家可以透過Adobe服務取得新技術和資料集時，立即加以運用。 我們會經常更新，致力將資料集和技術整合至平台，因此您不必再進行此工作。

### 安全與心安

保護資料是Adobe的首要任務。 Adobe通過為遵守業界接受的標準、法規和認證而開發的安全流程和控制來保護您的資料。

安全性內建在軟體和服務中，是Adobe安全產品生命週期的一部分。
要了解Adobe資料和軟體安全性、合規性等，請訪問安全頁，網址為https://www.adobe.com/security.html。

## [!DNL Data Science Workspace] 執行中

預測和深入分析可提供您所需的資訊，為造訪您的網站、聯絡您的客服中心或參與其他數位體驗的每位客戶提供高度個人化的體驗。 以下是您日常工作的方式 [!DNL Data Science Workspace].

### 定義問題

一切都始於商業問題。 例如，線上客服中心需要內容，協助他們將負面客戶情緒轉為正面。

有很多關於客戶的資料。 他們瀏覽了網站，將商品放入購物車，甚至下了訂單。 他們可能已收到電子郵件、使用的抵用券，或先前已聯絡客服中心。 然後，方式需要使用客戶及其活動的可用資料來判斷購買傾向，並建議客戶可能喜歡和使用的優惠方案。

![](./images/home/example_problem.png)

客服中心聯絡人時，客戶購物車中仍有兩雙鞋，但已移除一件襯衫。 有了這項資訊，智慧服務可能會建議客服中心代理在呼叫期間提供鞋子優惠20%的優惠券。 如果客戶使用抵用券，該資訊會新增至資料集，而客戶下次呼叫時，預測結果會更好。

### 探索並準備資料

根據所定義的業務問題，您知道方式應該查看客戶的所有網路交易，包括網站造訪、搜尋、頁面檢視、點按的連結、購物車動作、收到的優惠、收到的電子郵件、客服中心互動等。

資料科學家通常花費高達75%的時間來建立探索和轉換資料的方式。 資料通常來自多個存放庫，並儲存在不同的結構 — 必須先結合併對應資料，才能用來建立方式。

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

如果您從頭開始或配置現有方式，您將開始在組織的集中化標準化資料目錄中進行資料搜索，這大大簡化了搜索過程。 您甚至會發現組織中的其他資料科學家已經識別了類似的資料集，並選擇微調該資料集，而非從頭開始。
Adobe Experience Platform中的所有資料都符合標準化的XDM架構，不需要建立複雜的模型來加入資料，或向資料工程師尋求協助。

如果您沒有立即找到所需的資料，但資料存在於Adobe Experience Platform之外，內嵌其他資料集是一項相對簡單的工作，這也會轉換為標準化的XDM結構。\
您可以使用 [!DNL Jupyter Notebook] 簡化資料預處理 — 可能從筆記型電腦模板或您以前用於購買傾向的筆記型電腦開始。

![](./images/home/notebook_templates-new.png)

### 編寫配方

如果您已找到符合所有需求的配方，您可以繼續進行實驗。 或者，您也可以修改配方，或從頭建立配方 — 善用 [!DNL Data Science Workspace] 在 [!DNL Jupyter Notebook]. 使用製作執行階段可確保您都可以使用 [!DNL Data Science Workspace] 培訓和計分工作流程，並稍後轉換配方，以便儲存和重複使用。

您也可以將配方匯入至 [!DNL Data Science Workspace] 並在您建立智慧服務時，善用實驗工作流程。

### 試用配方

有了整合核心機器學習演算法的配方，許多配方例項都可以使用單一配方建立。 這些方式例項稱為模型。 模型要求進行培訓和評估，以優化其運行效率和效能，這個過程通常由試驗和錯誤組成。

![](./images/home/recipe_hiearchy_ui.png)

當您訓練模型時，會產生訓練執行和評估。 [!DNL Data Science Workspace] 跟蹤每個唯一模型及其培訓運行的評估度量。 通過實驗生成的評估度量將允許您確定表現最佳的培訓運行。

![](./images/home/evaluation_metrics.png)

造訪 [API](./models-recipes/train-evaluate-model-api.md) 或 [UI](./models-recipes/train-evaluate-model-ui.md) 有關如何訓練和評估模型的教學課程，請參閱 [!DNL Data Science Workspace].

### 操作模型

當您選擇了最佳培訓配方來滿足您的業務需求時，您可以在 [!DNL Data Science Workspace] 無需開發人員協助。 只需點按幾下，無需編碼。 已發佈的智慧服務可供組織的其他成員存取，而無需重新建立模型。

已發佈的智慧服務可設定成在新資料可用時，不時使用新資料自動進行訓練。 這可確保您的服務隨著時間的流逝而保持其效率和效能。

## 後續步驟

[!DNL Data Science Workspace] 有助於簡化資料科學工作流程，從資料收集到演算法，再到為所有技能水準的資料科學家提供的智慧服務。 使用精密的工具 [!DNL Data Science Workspace] 提供，您可以大幅縮短從資料到深入分析的時間。

更重要的是， [!DNL Data Science Workspace] 將Adobe領先行銷平台的資料科學和演算法最佳化功能交給企業資料科學家。 企業首次將專有的演算法帶入平台，利用Adobe強大的機器學習和人工智慧功能，以大規模提供高度個人化的客戶體驗。

憑借品牌專業知識和Adobe的機器學習和人工智慧的結合，企業有能力在客戶要求之前，通過提供他們想要的東西來提升業務價值和品牌忠誠度。

如需詳細資訊，例如完整的日常工作流程，請先閱讀 [Data Science Workspace逐步說明](./walkthrough.md) 檔案。

## 其他資源

以下影片旨在支援您了解 [!DNL Data Science Workspace].

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)