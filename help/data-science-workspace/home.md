---
keywords: Experience Platform；首頁；資料科學工作區；熱門主題；資料科學工作區；資料科學
solution: Experience Platform
title: 資料科學工作區概觀
topic-legacy: overview
description: 本指南概述與Adobe Experience Platform的Data Science Workspace相關的主要概念。
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 0%

---

# 資料科學工作區概觀

Adobe Experience Platform[!DNL Data Science Workspace]使用機器學習和人工智慧釋放您資料的見解。 [!DNL Data Science Workspace]已整合至Adobe Experience Platform，可協助您跨Adobe解決方案使用內容和資料資產進行預測。

所有技能等級的資料科學家將會找到複雜、簡單易用的工具，以支援快速開發、訓練和調整機器學習方式——所有AI技術的優點，而不需複雜。

有了[!DNL Data Science Workspace]，資料科學家就可輕鬆建立由機器學習提供支援的智慧服務API。 這些服務可與其他Adobe服務(包括Adobe Target和Adobe Analytics Cloud)搭配使用，協助您在網路、案頭和行動應用程式中自動化個人化、針對性的數位體驗。

本指南概述與[!DNL Data Science Workspace]相關的主要概念。

## 簡介

現今的企業非常重視挖掘大資料以取得預測和洞見，這些預測和洞見將協助他們個人化客戶體驗，並為客戶及業務提供更多價值。
同樣重要的是，從資料獲取深入見解的成本很高。 它通常需要熟練的資料科學家進行密集且耗時的資料研究，以開發機器學習模型或配方，為智慧服務提供動力。 這個過程冗長，技術複雜，而熟練的資料科學家也很難找到。

借助[!DNL Data Science Workspace],Adobe Experience Platform可讓您將以體驗為主的人工智慧帶入整個企業，透過以下各項簡化並加速資料轉化為洞見的編碼：
- 機器學習架構與執行時期
- 整合存取您儲存在Adobe Experience Platform的資料
- 基於[!DNL Experience Data Model](XDM)構建的統一資料模式
- 機器學習／人工智慧和管理大資料集的必備計算能力
- 預先建立的機器學習方式，加速向人工智慧驅動體驗的飛躍
- 簡化製作、重複使用和修改各種技能等級的資料科學家配方
- 只需按幾下滑鼠即可發佈和分享智慧型服務——毋需開發人員——並監控和再培訓，以持續最佳化個人化客戶體驗

所有技能等級的資料科學家都能更快地獲得見解，並更有效率地提供數位體驗。

## 快速入門

在深入探討[!DNL Data Science Workspace]的詳細資訊之前，以下是主要術語的簡要摘要：

| 詞語 | 定義 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] 內建 [!DNL Experience Platform] 可讓客戶運用跨Adobe解決方案的資料來建立機器 [!DNL Experience Platform] 學習模型，以產生智慧見解和預測，以打造令人愉悅的使用者數位體驗。 |
| 人工智慧 | 人工智慧是電腦系統的理論和發展，能夠執行通常需要人類智慧的任務，如視覺感知、語音識別、決策和語言間的翻譯。 |
| 機器學習 | 機器學習是一個研究領域，它讓電腦能夠學習，而不需明確寫程式。 |
| [!DNL Sensei] ML Framework | [!DNL Sensei] ML Framework是跨Adobe的統一機器學習框架，可運用相關資料，讓資料科學家以更快速、可擴充且可重複使用的方式，開發機器學習導向的智慧服務。 [!DNL Experience Platform]  |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM)是Adobe為「客戶體驗管理」定義標準方案( [!DNL Profile] 如 [!DNL ExperienceEvent]and)而引導的標準化工作。 |
| [!DNL JupyterLab] | [!DNL JupyterLab] 是Project Jupyter的開放原始碼Web介面，並緊密整合在其中 [!DNL Experience Platform]。 |
| 配方 | 配方是模型規格的Adobe術語，是代表特定機器學習、AI算法或整合演算法、處理邏輯和組態的頂層容器，用來建立並執行已訓練的模型，進而協助解決特定商業問題。 |
| 模型 | 模型是機器學習方式的實例，使用歷史資料和配置進行訓練，以針對業務使用案例進行解決。 |
| 培訓 | 培訓是學習模式和從標籤資料獲得見解的過程。 |
| 訓練的模型 | 訓練模型表示模型訓練過程的可執行輸出，其中一組訓練資料被應用到模型實例。 經過訓練的模型將保留對任何由其建立的智慧Web服務的引用。 該訓練模型適用於計分和建立智慧Web服務。 可將訓練模型的修改視為新版本來追蹤。 |
| 計分 | 計分是使用訓練好的模型，從資料產生見解的程式。 |
| 服務 | 已部署的服務會透過API公開人工智慧、機器學習模型或進階演算法的功能，讓其他服務或應用程式都能使用它來建立智慧型應用程式。 |

下表概述配方、模型、訓練執行和計分執行之間的階層關係。

![](./images/home/recipe_hiearchy_ui.png)

## 瞭解 [!DNL Data Science Workspace]

使用[!DNL Data Science Workspace]，您的資料科學家可以簡化在大型資料集中發現見解的繁瑣程式。 [!DNL Data Science Workspace]建立在通用的機器學習架構和執行時期上，提供進階的工作流程管理、模型管理和擴充能力。 智慧型服務支援重複使用機器學習方式，以支援使用Adobe產品和解決方案建立的各種應用程式。

### 一站式資料存取

資料是人工智慧和機器學習的基石。

[!DNL Data Science Workspace] 已與Adobe Experience Platform完全整合，包括資料 [!DNL Real-time Customer Profile]湖和 [!DNL Unified Edge]。一次探索您儲存在Adobe Experience Platform的所有組織資料，以及常見的大資料和深入學習資料庫，例如[!DNL Spark] ML和[!DNL TensorFlow]。 如果您找不到所需，請使用XDM標準架構來收錄您自己的資料集。

### 預先建立的機器學習方式

[!DNL Data Science Workspace] 包括符合一般商業需求的預先建立機器學習方式，例如零售銷售預測和異常偵測，因此資料科學家和開發人員不必從頭開始。目前提供三種方式：[產品購買預測](./pre-built-recipes/product-purchase-prediction.md)、[產品建議](./pre-built-recipes/product-recommendations.md)和[零售銷售](./pre-built-recipes/retail-sales.md)。

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

如果您喜歡，您可以依需求調整預先建立的配方、匯入配方或從頭開始建立自訂配方。 不過，一旦您開始訓練並超調配方，建立自訂的智慧服務並不需要開發人員——只要按幾下滑鼠，您就可以建立目標明確的個人化數位體驗。

### 以資料科學家為主的工作流程

無論您擁有何種程度的資料科學專業知識，[!DNL Data Science Workspace]都有助於簡化並加速尋找資料見解並將之套用至數位體驗的流程。

### 資料探索

尋找正確的資料並準備資料是建立有效配方最耗費人力的部分。 [!DNL Data Science Workspace] 而Adobe Experience Platform將幫助您更快地從資料獲取見解。

在Adobe Experience Platform，您的跨通道資料會集中並儲存在XDM標準架構中，因此資料更容易找到、瞭解和清理。 以通用模式為基礎的單一資料存放區可為您節省無數的資料探索與準備時間。

在瀏覽時，使用R、[!DNL Python]或Scala搭配整合的代管[!DNL Jupyter Notebook]來瀏覽[!DNL Platform]上的資料目錄。 使用其中一種語言，您也可以利用[!DNL Spark] ML和TensorFlow。 從頭開始，或使用針對特定商業問題提供的其中一個筆記型電腦模板。

在資料探索工作流程中，您也可以擷取新資料或使用現有功能來協助準備資料。

### 製作

使用[!DNL Data Science Workspace]，您可決定製作方式。

- 瀏覽預先建立的方式，以符合您的業務需求，並依現狀使用或設定，以節省時間。
- 從頭開始建立配方，使用Jupyter Notebook中的製作執行時期來開發和註冊配方。
- 使用[!DNL Git]和[!DNL Data Science Workspace]之間的驗證和整合，將在Adobe Experience Platform以外創作的配方上傳到[!DNL Data Science Workspace]或從儲存庫導入配方代碼，如[!DNL Git]。

### 實驗

資料科學工作區為實驗程式帶來極大的彈性。 從您的配方開始。 然後使用相同的核心演算法建立個別的執行個體，並搭配獨特的特性，例如超調參數。 您可以建立您所需的例項數，並視需要對每個例項進行訓練和計分。 在您進行培訓時，[!DNL Data Science Workspace]會追蹤方式、方式例項和訓練例項，以及評估量度，因此您不需要。

### 操作化

當您對食譜感到滿意時，只需按幾下滑鼠，就能建立智慧型服務。 不需撰寫程式碼——您可以自行完成，毋需請開發人員或工程師。 最後，將智慧型服務發佈至AdobeIO，讓您的數位體驗團隊可以使用。

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### 持續改進

[!DNL Data Science Workspace] 追蹤智慧型服務的叫用位置及執行方式。當資料捲入時，您可以評估智慧型服務的準確度以關閉迴路，並視需要重新訓練配方以提升效能。 結果是客戶個人化的精確度不斷提升。

### 存取新功能和資料集

資料科學家可以在新技術和資料集透過Adobe服務推出時立即加以運用。 透過頻繁的更新，我們將資料集和技術整合到平台中，因此您不必再擔心。

### 安全與心安

保護您的資料是Adobe的首要任務。 Adobe利用為符合業界公認的標準、法規和認證而開發的安全流程和控制功能來保護您的資料。

安全性內建在軟體和服務中，作為Adobe安全產品生命週期的一部分。
若要瞭解Adobe資料和軟體安全性、合規性等，請造訪安全性網頁：https://www.adobe.com/security.html。

## [!DNL Data Science Workspace] 實際運作

預測和洞見可提供您所需的資訊，為造訪您網站、聯絡您的客服中心或參與其他數位體驗的每位客戶提供高度個人化的體驗。 以下是您的日常工作如何透過[!DNL Data Science Workspace]進行。

### 定義問題

一切都始於商業問題。 例如，線上客服中心需要情境來協助他們將負面客戶情緒轉化為正面情緒。

關於客戶的資料非常多。 他們瀏覽了網站，將商品放入購物車，甚至下了訂單。 他們可能以前曾收到過電子郵件、使用過抵用券或與客服中心聯絡。 因此，配方需要使用客戶及其活動的可用資料來判斷購買傾向，並建議客戶可能喜歡和使用的優惠。

![](./images/home/example_problem.png)

在呼叫中心聯絡時，客戶在購物車中仍有兩雙鞋，但已移除一件襯衫。 有了這些資訊，智慧型服務可能會建議呼叫中心代理在呼叫期間提供鞋類折扣20%的優惠券。 如果客戶使用抵用券，該資訊會加入資料集，而且下次客戶呼叫時，預測效果會更好。

### 探索並準備資料

根據定義的業務問題，您知道配方應查看客戶的所有Web交易，包括網站造訪、搜尋、頁面檢視、點按的連結、購物車動作、收到的優惠、收到的電子郵件、客服中心互動等。

資料科學家通常花費高達75%的時間來建立探索和轉換資料的方式。 資料通常來自多個儲存庫，並儲存在不同的結構中——必須先加以合併並映射，才能用來建立方式。

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

如果您從頭開始或設定現有的方式，您就可以在組織的集中式標準化資料目錄中開始資料搜尋，如此可大幅簡化搜尋作業。 您甚至會發現，您組織中的另一位資料科學家已經識別出類似的資料集，並選擇微調該資料集，而非從頭開始。
Adobe Experience Platform的所有資料都符合標準的XDM模式，無需建立複雜的模型來連接資料或獲得資料工程師的幫助。

如果您不能立即找到所需的資料，但它存在於Adobe Experience Platform以外，那麼，收集更多資料集是一項相對簡單的任務，這也將轉化為標準化的XDM模式。\
您可以使用[!DNL Jupyter Notebook]來簡化資料預處理——可能從您先前習慣購買的筆記型電腦範本或筆記型電腦開始。

![](./images/home/notebook_templates.png)

### 編寫配方

如果您已找到符合您所有需求的配方，您可以繼續進行實驗。 或者，您也可以修改配方，或從頭開始建立配方——運用[!DNL Jupyter Notebook]中的[!DNL Data Science Workspace]製作執行階段。 使用編寫執行時期可確保您同時使用[!DNL Data Science Workspace]訓練和計分工作流程，並稍後轉換配方，以便組織中的其他人儲存和重複使用配方。

您也可以將配方匯入至[!DNL Data Science Workspace]，並在建立智慧型服務時運用實驗工作流程。

### 試用配方

透過整合核心機器學習演算法的配方，許多配方例項可以使用單一配方來建立。 這些方式例項稱為模型。 模型需要訓練和評估以優化其運行效率和效能，這一過程通常由試驗和錯誤組成。

![](./images/home/recipe_hiearchy_ui.png)

在您訓練模型時，會產生訓練執行和評估。 [!DNL Data Science Workspace] 追蹤每個獨特模型及其訓練執行的評估度量。透過實驗產生的評量度可讓您決定最佳的訓練執行。

![](./images/home/evaluation_metrics.png)

請造訪[API](./models-recipes/train-evaluate-model-api.md)或[UI](./models-recipes/train-evaluate-model-ui.md)教學課程，瞭解如何在[!DNL Data Science Workspace]中訓練和評估模型。

### 實施模型

當您選擇最佳的訓練方式來滿足您的業務需求時，您可以在[!DNL Data Science Workspace]中建立智慧型服務，毋需開發人員協助。 只需按幾下滑鼠，不需要撰寫程式碼。 發佈的智慧型服務可供貴組織的其他成員存取，而不需重新建立模型。

已發佈的智慧型服務可設定為在新資料可用時，使用新資料自動自動進行培訓。 這可確保您的服務在時間持續時仍能維持其效率和效能。

## 後續步驟

[!DNL Data Science Workspace] 有助於簡化和簡化資料科學工作流程，從資料收集到演算法，到智慧服務，讓所有技能等級的資料科學家都能使用。使用[!DNL Data Science Workspace]提供的精密工具，您可以大幅縮短從資料到深入資訊的時間。

更重要的是，[!DNL Data Science Workspace]將Adobe領先行銷平台的資料科學與演算法最佳化功能交由企業資料科學家掌控。 企業首次將專屬的演算法帶入平台，運用Adobe強大的機器學習和人工智慧功能，大規模提供高度個人化的客戶體驗。

隨著品牌專業知識與Adobe的機器學習與人工智慧的結合，企業有能力在客戶要求之前，先提供他們想要的東西，從而推動更多商業價值和品牌忠誠度。

如需詳細資訊，例如完整的日常工作流程，請先閱讀[資料科學工作區逐步說明檔案](./walkthrough.md)。

## 其他資源

以下視頻旨在支援您對[!DNL Data Science Workspace]的理解。

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)
