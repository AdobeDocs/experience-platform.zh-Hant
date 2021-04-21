---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 管理、隱私權與安全性概觀
topic-legacy: overview
description: Adobe Experience Platform提供數種服務和工具，讓您放心地控制所收集的體驗資料，以符合您的商業慣例、法律義務和開發程式。
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 1%

---

# Adobe Experience Platform的治理、隱私和安全

Adobe Experience Platform可讓您收集、分析、最佳化和動作資料，以大幅提升客戶體驗。 這些資料龐大、複雜，而且極具價值。 根據您的資料作業性質、您的業務所在的法律管轄區，以及您的組織有關資料使用的政策，您必須謹慎控制並監控客戶體驗資料的收集與使用，以保護您的業務利益。

Experience Platform提供數種服務和工具，讓您放心地控制所收集的體驗資料，以符合您的商業慣例、法律義務和開發程式。 以下各節介紹了這些服務，並提供了文檔的連結，以瞭解詳細資訊。

服務可分為三個網域：

* [資料治理](#governance)
* [隱私](#privacy)
* [安全性](#security)

## 資料治理{#governance}

資料治理是與Experience Platform中的每項功能交織在一起的一個基本概念。 資料治理代表您透過平台在整個資料歷程中控制和理解資料的能力。 這包括維護資料品質、資料承繼、資料編目等。

### Adobe Experience Platform資料治理{#data-governance}

作為平台服務，Adobe Experience Platform資料治理允許您管理客戶資料並確保遵守適用於資料使用的法規、限制和策略。 它在Experience Platform的各個層級中發揮關鍵作用，包括資料使用標籤、資料使用政策、原則實施和資料世系。

如需詳細資訊，請參閱[資料治理概觀](../../data-governance/home.md)。

### 目錄和資料集{#catalog}

目錄服務是平台內資料位置和世系的記錄系統。 雖然所有吸收到Experience Platform中的資料都會以檔案和目錄的形式儲存在資料湖中，但目錄會保留這些檔案和目錄的中繼資料和說明，以供查閱和監控之用。

目錄將收錄的資料組織成資料集，每個資料集都包含可用來標籤及分類資料的中繼資料。

有關服務的詳細資訊，請參閱[目錄服務概述](../../catalog/home.md)。 要瞭解如何管理Experience Platform中的資料集，請參見[資料集概述](../../catalog/datasets/overview.md)。

## 隱私權 {#privacy}

隱私權是您的企業、立法者和客戶的重要問題。 由於從客戶收集到的個人資料幾乎是所有Experience Platform工作流程的核心，因此Platform會提供支援這些計畫的服務。

### Adobe Experience Platform 隱私權服務 {#privacy-service}

歐盟的通用資料保護規則(GDPR)和加州消費者隱私法(CCPA)等法律隱私權法規授予其管轄區內公民存取和刪除您收集和儲存的個人資料的權利。

Adobe Experience Platform Privacy Service提供REST風格的API和使用者介面，以協助管理這些要求。 有了Privacy Service，您可以提交請求，要求從Adobe Experience Cloud應用程式存取或刪除私人或個人客戶資料，以利自動符合法律和組織的隱私法規。

如需詳細資訊，請參閱[Privacy Service概觀](../../privacy-service/home.md)。

### 許可處理{#consent}

許多法律隱私權法規在資料收集、個人化和其他行銷使用案例時，都引入了主動和特定同意的要求。 為符合這些要求，Experience Platform允許您在個別客戶個人檔案中擷取同意資訊，並將這些偏好用作決定每個客戶資料在下游平台工作流程中使用的因素。

要瞭解如何使用Adobe標準處理客戶同意和偏好資料，請參閱Experience Platform](./consent/adobe/overview.md)中關於[同意處理的概述。

有關如何根據IAB透明度和同意框架(TCF)2.0處理客戶同意資料的資訊，請參閱平台](./consent/iab/overview.md)中[IAB TCF 2.0支援的概述。

## 安全性 {#security}

您的資料的完整性和安全性對於您的業務而言不可或缺，而此風險需要業界領先的安全性功能。 為了應對這項挑戰，Platform提供了數種工具來協助保護您的資料運作。

### 訪問控制{#access-control}

Experience Platform使用Adobe Admin Console為各種平台功能提供基於角色的訪問控制。 此功能運用Admin Console中的產品設定檔，將使用者與權限和沙盒連結。

有關詳細資訊，請參閱[訪問控制概述](../../access-control/home.md)。

### 沙盒 {#sandboxes}

Experience Platform是專為在全球範圍豐富數位體驗應用程式而設計。 公司通常並行執行多種數位體驗應用程式，並需要滿足這些應用程式的開發、測試和部署需求，同時確保運作符合規範。

為了因應開發靈活性的需求，Experience Platform提供沙盒，將單一平台實例分割為不同的虛擬環境，以協助您根據自己的開發生命週期來開發數位體驗應用程式。

如需詳細資訊，請參閱[沙盒概述](../../sandboxes/home.md)。

## 後續步驟

本檔案概述了與資料管理、隱私權和安全性相關的各種平台服務與工具。 請參閱本指南中連結的檔案，以進一步瞭解這些功能。
