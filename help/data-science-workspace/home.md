---
keywords: Experience Platform；家庭；資料科學工作區；熱門主題；資料科學工作區；資料科學
solution: Experience Platform
title: 資料科學工作區概述
description: 本指南概述了與Adobe Experience Platform資料科學工作區相關的關鍵概念。
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 0%

---

# 資料科學工作區概述

Adobe Experience Platform [!DNL Data Science Workspace] 利用機器學習和人工智慧從資料中釋放洞見。 融入Adobe Experience Platform, [!DNL Data Science Workspace] 幫助您跨Adobe解決方案使用內容和資料資產進行預測。

所有技能級別的資料科學家將找到複雜、易用的工具來支援機器學習方法的快速開發、培訓和調整 — 所有AI技術的好處都沒有複雜性。

與 [!DNL Data Science Workspace]資料科學家可以輕鬆建立智慧服務API — 由機器學習驅動。 這些服務與其他Adobe服務(包括Adobe Target和Adobe Analytics Cloud)協作，幫助您自動化Web、案頭和移動應用中的個性化、有針對性的數字型驗。

本指南概述了與 [!DNL Data Science Workspace]。

## 簡介

今天的企業將挖掘大資料作為重中之重來進行預測和洞察，這將有助於他們個性化客戶體驗，為客戶和業務提供更多價值。
儘管這一點很重要，從資料到洞察力的成本也很高。 它通常需要熟練的資料科學家來進行密集且耗時的資料研究，以開發能夠支援智慧服務的機器學習模型或配方。 這個過程很長，技術複雜，而熟練的資料科學家很難找到。

與 [!DNL Data Science Workspace],Adobe Experience Platform允許您將注重經驗的AI帶到整個企業中，通過以下方式簡化並加速資料到深入的代碼轉換：
- 機器學習框架和運行時
- 整合訪問儲存在Adobe Experience Platform的資料
- 基於的統一資料架構 [!DNL Experience Data Model] (XDM)
- 機器學習/人工智慧和管理大資料集所需的計算能力
- 預構建的機器學習配方，加速向人工智慧驅動體驗的飛躍
- 為不同技能級別的資料科學家簡化配方的編寫、重用和修改
- 只需點擊幾下即可實現智慧服務發佈和共用，無需開發人員參與，並監控和再培訓，以持續優化個性化客戶體驗

所有技能級別的資料科學家將更快地獲得更快、更有效的數字型驗。

## 快速入門

在深入瞭解 [!DNL Data Science Workspace]以下是關鍵術語的簡要摘要：

| 詞語 | 定義 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] 內 [!DNL Experience Platform] 使客戶能夠利用資料建立機器學習模型 [!DNL Experience Platform] 和Adobe解決方案，以生成智慧洞察和預測，從而創造令人愉快的最終用戶數字型驗。 |
| 人工智慧 | 人工智慧是電腦系統的理論和發展，能夠執行通常需要人類智慧的任務，如視覺感知、語音識別、決策和語言間的翻譯。 |
| 機器學習 | 機器學習是一個研究領域，它使電腦能夠在不經過明確寫程式的情況下學習。 |
| [!DNL Sensei] ML框架 | [!DNL Sensei] ML Framework是一個跨Adobe的統一機器學習框架，它利用 [!DNL Experience Platform] 以更快、可擴展和可重用的方式，使資料科學家在開發機器學習驅動的智慧服務方面獲得能力。 |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM)是通過Adobe來定義標準架構(如 [!DNL Profile] 和 [!DNL ExperienceEvent]，用於客戶體驗管理。 |
| [!DNL JupyterLab] | [!DNL JupyterLab] 是Project Jupyter的一個基於Web的開源介面，並緊密整合到 [!DNL Experience Platform]。 |
| 食譜 | 配方是模型規範的Adobe術語，是代表特定機器學習、AI算法或算法、處理邏輯和配置的頂級容器，用於構建和執行經過訓練的模型，從而幫助解決特定的業務問題。 |
| 模型 | 模型是使用歷史資料和配置進行訓練以針對業務使用案例解決的機器學習配方的實例。 |
| 訓練 | 培訓是從標籤資料中學習模式和洞察力的過程。 |
| 訓練的模型 | 訓練後的模型表示模型訓練過程的可執行輸出，其中一組訓練資料被應用到模型實例。 經過訓練的模型將維護對任何由其建立的智慧Web服務的引用。 該訓練模型適用於評分和建立智慧Web服務。 可以作為新版本跟蹤對訓練模型的修改。 |
| 評分 | 評分是使用訓練好的模型從資料生成洞見的過程。 |
| 服務 | 已部署的服務通過API公開人工智慧、機器學習模型或高級算法的功能，以便其他服務或應用程式可以使用它來建立智慧應用。 |

下圖概述了配方、模型、培訓運行和評分運行之間的層次關係。

![](./images/home/recipe_hiearchy_ui.png)

## 瞭解 [!DNL Data Science Workspace]

與 [!DNL Data Science Workspace]您的資料科學家可以簡化在大型資料集中發現洞見的繁瑣過程。 建立在通用的機器學習框架和運行時， [!DNL Data Science Workspace] 提供高級的工作流管理、模型管理和可擴充性。 智慧服務支援重新使用機器學習方法，為使用Adobe產品和解決方案建立的各種應用程式提供動力。

### 一站式資料存取

資料是人工智慧和機器學習的基石。

[!DNL Data Science Workspace] 與Adobe Experience Platform，包括資料湖， [!DNL Real-Time Customer Profile], [!DNL Unified Edge]。 同時瀏覽儲存在Adobe Experience Platform的所有組織資料，以及常見的大資料和深度學習庫，如 [!DNL Spark] ML和 [!DNL TensorFlow]。 如果找不到所需內容，請使用XDM標準化架構攝取自己的資料集。

### 預構建的機器學習配方

[!DNL Data Science Workspace] 包括滿足常見商業需求的預構建機器學習方法，如零售銷售預測和異常檢測，因此資料科學家和開發人員不必從零開始。 目前有三個食譜， [產品採購預測](./pre-built-recipes/product-purchase-prediction.md)。 [產品建議](./pre-built-recipes/product-recommendations.md), [零售銷售](./pre-built-recipes/retail-sales.md)。

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

如果您願意，您可以根據需要調整預構建的配方、導入配方或從頭開始構建自定義的配方。 但是，一旦您開始訓練和超調配方，建立定制智慧服務並不需要開發人員 — 只需點擊幾下，您就準備好構建有針對性的個性化數字型驗。

### 以資料科學家為核心的工作流

不管你的資料科學專業水準如何， [!DNL Data Science Workspace] 有助於簡化和加速在資料中發現洞見並將其應用於數字型驗的過程。

### 資料勘探

找到正確的資料並準備資料是構建有效配方中最耗費人力的部分。 [!DNL Data Science Workspace] 而Adobe Experience Platform會幫助你更快地從資料中獲得見解。

在Adobe Experience Platform，您的跨通道資料集中並儲存在XDM標準化架構中，因此資料更易於查找、理解和清理。 基於通用模式的單個資料儲存可以為您節省無數時間的資料探索和準備。

瀏覽時，使用R [!DNL Python]，或使用整合、托管的Scala [!DNL Jupyter Notebook] 瀏覽資料目錄 [!DNL Platform]。 使用其中一種語言，您還可以 [!DNL Spark] ML和TensorFlow。 從頭開始，或使用針對特定業務問題提供的筆記本模板之一。

作為資料探索工作流的一部分，您還可以接收新資料或使用現有功能來幫助準備資料。

### 製作

與 [!DNL Data Science Workspace]，您可以決定如何編寫食譜。

- 通過瀏覽預構建的處方來節省時間，該處方可滿足您的業務需求，您可以按原樣使用或配置以滿足特定需求。
- 從頭開始建立配方，使用Jupyter筆記本中的創作運行庫來開發和註冊配方。
- 將在Adobe Experience Platform以外創作的處方上載到 [!DNL Data Science Workspace] 或從儲存庫中導入處方代碼，如 [!DNL Git]，使用在 [!DNL Git] 和 [!DNL Data Science Workspace]。

### 實驗

Data Science Workspace為實驗過程帶來了巨大的靈活性。 從你的食譜開始。 然後使用相同的核心算法建立一個單獨的實例，並配以獨特的特性，如超調參數。 您可以根據需要建立任意多個實例，並根據需要對每個實例進行多次培訓和評分。 在你訓練他們時， [!DNL Data Science Workspace] 跟蹤配方、處方實例和經過培訓的實例，以及評估度量，因此您不必執行。

### 操作化

當你對你的食譜感到滿意時，只需點擊幾下就可以建立出智慧服務。 無需編碼 — 您可以自行編寫，無需徵聘開發人員或工程師。 最後，將智慧服務發佈到AdobeIO，它已準備好供您的數字型驗團隊使用。

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### 持續改進

[!DNL Data Science Workspace] 跟蹤調用智慧服務的位置及其執行方式。 隨著資料滾入，您可以評估智慧服務準確性以關閉循環，並根據需要重新培訓配方以提高效能。 結果是客戶個性化的精確性不斷得到提高。

### 訪問新功能和資料集

資料科學家一旦通過Adobe服務獲得新技術和資料集，就可以利用它們。 通過頻繁的更新，我們將資料集和技術整合到平台中，這樣您就不必做了。

### 安全與心安

保護資料是Adobe的頭等大事。 Adobe使用為幫助遵守業界公認的標準、法規和認證而開發的安全流程和控制來保護您的資料。

安全性內置在軟體和服務中，作為Adobe安全產品生命週期的一部分。
要瞭解Adobe資料和軟體安全性、合規性等，請訪問安全頁面：https://www.adobe.com/security.html。

## [!DNL Data Science Workspace] 行動

預測和洞察力提供您需要的資訊，以便為訪問您的網站、聯繫您的呼叫中心或參與其他數字型驗的每個客戶提供高度個性化的體驗。 這是您日常工作的方式 [!DNL Data Science Workspace]。

### 定義問題

一切都始於一個商業問題。 例如，線上呼叫中心需要上下文來幫助他們將負面的客戶情緒轉變為正面情緒。

關於客戶的資料很多。 他們瀏覽了網站，把物品放在購物車裡，甚至下了訂單。 他們可能已經收到電子郵件、使用優惠券，或曾聯繫過呼叫中心。 因此，處方需要使用客戶及其活動的可用資料來確定購買傾向，並建議客戶可能喜歡和使用的優惠。

![](./images/home/example_problem.png)

在呼叫中心聯繫時，客戶仍在推車中有兩雙鞋，但已卸下一件襯衫。 有了這些資訊，智慧服務可能會建議呼叫中心代理在呼叫期間提供鞋類優惠券20%。 如果客戶使用優惠券，則該資訊會被添加到資料集中，並且下次客戶呼叫時，預測結果會更好。

### 瀏覽和準備資料

根據定義的業務問題，您知道處方應查看客戶的所有Web事務，包括網站訪問、搜索、頁面視圖、按一下的連結、購物車操作、收到的優惠、收到的電子郵件、呼叫中心交互等。

資料科學家通常花費75%的時間來建立探索和轉換資料的配方。 資料通常來自多個儲存庫，並保存在不同的架構中 — 必須先組合併映射資料，然後才能用於建立處方。

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

如果您從頭開始或配置現有配方，則可以在組織的集中且標準化的資料目錄中開始資料搜索，這大大簡化了搜索。 你甚至可能發現，你組織中的另一個資料科學家已經識別出一個類似的資料集，並選擇對該資料集進行微調，而不是從頭開始。
Adobe Experience Platform的所有資料都符合標準化的XDM模式，無需建立用於連接資料或從資料工程師那裡獲得幫助的複雜模型。

如果您沒有立即找到所需的資料，但它存在於Adobe Experience Platform之外，那麼接收額外的資料集是一項相對簡單的任務，這也將轉化為標準化的XDM架構。\
您可以使用 [!DNL Jupyter Notebook] 簡化資料預處理 — 可能從您以前習慣購買的筆記本模板或筆記本開始。

![](./images/home/notebook_templates-new.png)

### 編寫配方

如果你已經找到了滿足你所有需求的配方，你可以轉向實驗。 或者，您可以修改配方，或者從頭開始建立配方 — 利用 [!DNL Data Science Workspace] 創作運行時 [!DNL Jupyter Notebook]。 使用創作運行時可確保您都可以 [!DNL Data Science Workspace] 培訓和評分工作流，並稍後轉換處方，以便其可以儲存並由組織中的其他人重複使用。

您也可以將處方導入至 [!DNL Data Science Workspace] 並在建立智慧服務時利用實驗工作流。

### 試用配方

使用包含核心機器學習算法的配方，可以使用單個配方建立許多配方實例。 這些處方實例稱為模型。 一個模型需要進行培訓和評估，以優化其運行效率和效能，這個過程通常由試錯組成。

![](./images/home/recipe_hiearchy_ui.png)

在您訓練模型時，會生成培訓運行和評估。 [!DNL Data Science Workspace] 跟蹤每個唯一模型的評估度量及其培訓運行。 通過實驗生成的評估指標將允許您確定表現最佳的培訓運行。

![](./images/home/evaluation_metrics.png)

訪問 [API](./models-recipes/train-evaluate-model-api.md) 或 [UI](./models-recipes/train-evaluate-model-ui.md) 有關如何訓練和評估模型的教程 [!DNL Data Science Workspace]。

### 將模型運作

當您選擇了經過培訓的最佳配方來滿足您的業務需求時，您可以在 [!DNL Data Science Workspace] 沒有開發人員的幫助。 只需點擊幾下，無需編碼。 組織中的其他成員無需重新建立模型即可訪問已發佈的智慧服務。

已發佈的智慧服務可配置為在新資料可用時使用新資料自動進行不時培訓。 這可確保您的服務在時間持續時保持其效率和功效。

## 後續步驟

[!DNL Data Science Workspace] 幫助簡化資料科學工作流，從資料收集到算法，到為各技能級別的資料科學家提供智慧服務。 使用先進的工具 [!DNL Data Science Workspace] 提供，您可以顯著縮短從資料到洞察的時間。

更重要的是， [!DNL Data Science Workspace] 將Adobe領先營銷平台的資料科學和算法優化能力交給企業資料科學家。 企業首次可以將專有算法帶入平台，利用Adobe強大的機器學習和人工智慧功能大規模提供高度個性化的客戶體驗。

憑借品牌專業知識和Adobe的機器學習和人工智慧能力的結合，企業有能力在客戶要求之前，給客戶他們想要的東西，從而推動更多商業價值和品牌忠誠度。

有關其他資訊（如完整的日常工作流），請首先閱讀 [Data Science Workspace漫遊](./walkthrough.md) 文檔。

## 其他資源

以下視頻旨在支援您對 [!DNL Data Science Workspace]。

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)