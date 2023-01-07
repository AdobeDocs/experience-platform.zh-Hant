---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 控管、隱私權及安全性概述
description: Adobe Experience Platform提供數種服務和工具，讓您放心地控制收集的體驗資料，以符合您的業務實務、法律義務和開發程式。
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 1%

---

# Adobe Experience Platform的控管、隱私權及安全性

Adobe Experience Platform可讓您擷取、分析、最佳化和動作資料，大幅提升客戶體驗。 這些資料龐大、複雜且極具價值。 根據您的資料操作性質、您的業務所在的法律管轄區，以及您有關資料使用的組織策略，您必須小心控制並監控客戶體驗資料的收集和使用，以保護您的業務利益。

Experience Platform提供數種服務和工具，讓您放心地控制收集的體驗資料，以符合您的業務實務、法律義務和開發程式。 以下各節介紹了這些服務，並提供了有關進一步資訊的文檔連結。

服務可分為三個網域：

* [資料控管](#governance)
* [隱私權](#privacy)
* [安全性](#security)

## 資料控管 {#governance}

資料控管是與Experience Platform中的每項功能交織在一起的基本概念。 資料控管代表您能透過Platform在資料的整個歷程中控制及理解資料。 這包括維護資料質量、資料處理、資料編目等。

### Adobe Experience Platform資料控管 {#data-governance}

Adobe Experience Platform資料控管以Platform服務的形式，可讓您管理客戶資料，並確保符合適用於資料使用的法規、限制和政策。 它在Experience Platform內的各個層級（包括資料使用標籤、資料使用策略、策略實施和資料處理）發揮關鍵作用。

請參閱 [資料控管概觀](../../data-governance/home.md) 以取得更多資訊。

### 目錄和資料集 {#catalog}

目錄服務是Platform內用於資料位置和歷程的記錄系統。 雖然所有擷取到Experience Platform中的資料都會以檔案和目錄的形式儲存在Data Lake中，但「目錄」會保留這些檔案和目錄的中繼資料和說明，以供查閱和監控之用。

目錄會將內嵌的資料組織成資料集，每個資料集都包含可用來為其包含的資料加上標籤及分類的中繼資料。

請參閱 [目錄服務概述](../../catalog/home.md) 以取得服務的詳細資訊。 若要了解如何在Experience Platform中管理資料集，請參閱 [資料集概述](../../catalog/datasets/overview.md).

## 隱私權 {#privacy}

隱私權是貴機構、立法者和客戶的關鍵問題。 由於從客戶收集的個人資料是幾乎所有Experience Platform工作流程的核心，因此Platform提供支援這些計畫的服務。

### Adobe Experience Platform 隱私權服務 {#privacy-service}

歐盟的一般資料保護規範(GDPR)和加州消費者隱私法(CCPA)等法律隱私權法規，授予轄區公民存取和刪除您收集和儲存之個人資料的權利。

Adobe Experience Platform Privacy Service提供RESTful API和使用者介面，以協助管理這些要求。 透過Privacy Service，您可以提交從Adobe Experience Cloud應用程式存取或刪除私人或個人客戶資料的請求，協助您自動遵守法律和組織隱私權法規。

請參閱 [Privacy Service概述](../../privacy-service/home.md) 以取得更多資訊。

### 同意處理 {#consent}

許多法律隱私權法規針對資料收集、個人化和其他行銷使用案例，提出了主動和特定同意的要求。 為符合這些需求，Experience Platform可讓您擷取個別客戶設定檔中的同意資訊，並將這些偏好設定用作決定下游Platform工作流程中各客戶資料使用方式的因素。

若要了解如何使用Adobe標準處理客戶同意和偏好資料，請參閱 [同意處理Experience Platform](./consent/adobe/overview.md).

如需依照IAB透明與同意架構(TCF)2.0處理客戶同意資料的相關資訊，請參閱 [平台中的IAB TCF 2.0支援](./consent/iab/overview.md).

## 安全性 {#security}

您的資料的完整性和安全性對於您的業務是不可或缺的，而這一風險需要業界領先的安全功能。 為了應對此挑戰，Platform提供數種工具，可協助保護您的資料操作。

### 資料加密

所有Platform資料在傳輸中和靜止時都經過加密。 請參閱 [平台中的資料加密](./encryption.md) 以取得更多資訊。

### 存取控制 {#access-control}

Experience Platform使用Adobe Admin Console，對各種Platform功能提供角色型存取控制。 此功能會運用Admin Console中的產品設定檔，將使用者與權限和沙箱連結。

請參閱 [存取控制概觀](../../access-control/home.md) 以取得更多資訊。

### 沙箱 {#sandboxes}

Experience Platform的建置目的，是在全球範圍豐富數位體驗應用程式。 公司通常並行運行多個數字型驗應用程式，需要滿足這些應用程式的開發、測試和部署，同時確保操作合規性。

為了因應開發彈性的需求，Experience Platform提供沙箱，可將單一Platform執行個體分割成個別的虛擬環境，以協助您根據自己的開發生命週期來改進數位體驗應用程式。

請參閱 [沙箱概述](../../sandboxes/home.md) 以取得更多資訊。

## 後續步驟

本檔案概述了與資料控管、隱私權和安全性相關的各種Platform服務和工具。 請參閱本指南中連結的檔案，深入了解這些功能。
