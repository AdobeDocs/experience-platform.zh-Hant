---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 治理、隱私和安全性概述
description: Adobe Experience Platform提供數種服務和工具，可讓您安心控制所收集的體驗資料，以符合您的業務實務、法律義務和開發程式。
feature: Data Governance,Privacy
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 8%

---

# Adobe Experience Platform中的控管、隱私權和安全性

Adobe Experience Platform可讓您內嵌、分析、最佳化資料並採取行動，以大幅提升客戶體驗。 這些資料非常龐大、複雜且極具價值。 根據您的資料作業性質、您的企業作業所依據的法律管轄區以及您有關資料使用的組織政策，您必須小心地控制和監控客戶體驗資料的收集與使用，以保護您的企業利益。

Experience Platform提供數種服務和工具，可讓您安心控制所收集的體驗資料，以符合您的業務實務、法律義務和開發流程。 以下各節會介紹每項服務，並提供檔案連結，以取得進一步資訊。

這些服務可歸類為三個網域：

* [資料治理](#governance)
* [隱私權](#privacy)
* [安全性](#security)

## 資料治理 {#governance}

資料控管是與Experience Platform中每項功能交織的基本概念。 資料控管代表您能夠控制並理解資料透過Experience Platform的整個歷程。 這涉及到維護資料品質、資料譜系、資料編目等等。

### Adobe Experience Platform資料控管 {#data-governance}

Adobe Experience Platform資料控管可作為Experience Platform服務，讓您管理客戶資料，並確保遵守適用於資料使用的法規、限制和原則。 它在Experience Platform的不同層級上扮演關鍵角色，包括資料使用標籤、資料使用原則、原則執行和資料譜系。

如需詳細資訊，請參閱[資料控管概觀](../../data-governance/home.md)。

### 目錄和資料集 {#catalog}

目錄服務是Experience Platform中資料位置和譜系的記錄系統。 雖然擷取至 Experience Platform 中的所有資料都以檔案和目錄形式儲存在資料湖中，但是為了查詢和監控目的，目錄會留存這些檔案和目錄的中繼資料和說明。

目錄會將擷取的資料整理到資料集中，每個資料集都包含可用於標籤其所包含資料並將之分類的中繼資料。

如需服務的詳細資訊，請參閱[目錄服務總覽](../../catalog/home.md)。 若要瞭解如何在Experience Platform中管理資料集，請參閱[資料集總覽](../../catalog/datasets/overview.md)。

## 隱私權 {#privacy}

隱私權對您的企業、立法者和客戶而言都是重要問題。 由於從客戶收集的個人資料是幾乎所有的Experience Platform工作流程的核心，Experience Platform提供服務以支援這些計畫。

### Adobe Experience Platform Privacy Service {#privacy-service}

歐盟一般資料保護規範(GDPR)和加州消費者隱私保護法(CCPA)等法律隱私權法規授予轄區內公民存取和刪除您從他們那裡收集和儲存之個人資料的權利。

Adobe Experience Platform Privacy Service提供RESTful API和使用者介面，以協助管理這些請求。 透過Privacy Service，您可以提交存取或刪除Adobe Experience Cloud應用程式中私人或個人客戶資料的請求，協助促進法律與組織隱私法規的自動合規性。

如需詳細資訊，請參閱[Privacy Service概觀](../../privacy-service/home.md)。

### 同意處理 {#consent}

許多法律隱私權法規在資料收集、個人化和其他行銷使用案例方面，都引入了對主動和特定同意的需求。 為了滿足這些要求，Experience Platform可讓您擷取個別客戶設定檔中的同意資訊，並使用這些偏好設定作為決定因素，來決定如何將每個客戶的資料用於下游Experience Platform工作流程。

若要瞭解如何使用Adobe標準處理客戶同意和偏好設定資料，請參閱Experience Platform[&#128279;](./consent/adobe/overview.md)中同意處理的概述。

如需有關如何根據IAB透明與同意架構(TCF) 2.0處理客戶同意資料的資訊，請參閱Experience Platform[&#128279;](./consent/iab/overview.md)中IAB TCF 2.0支援的概觀。

## 安全性 {#security}

資料完整性與安全性對您的業務而言是不可或缺的，而這項風險需要業界領先的安全性功能。 為了迎接這項挑戰，Experience Platform提供了數種工具來協助保護您的資料作業。

### 資料加密

所有Experience Platform資料在傳輸和存放時都會經過加密。 如需詳細資訊，請至 [Experience Platform 中的資料加密](./encryption.md)參閱文件。

### 存取控制 {#access-control}

Experience Platform使用Adobe Admin Console為各種Experience Platform功能提供角色型存取控制。 此功能運用Admin Console中的產品設定檔，將使用者與許可權和沙箱連結。

如需詳細資訊，請參閱[存取控制總覽](../../access-control/home.md)。

### 沙箱 {#sandboxes}

Experience Platform的建置可豐富全球的數位體驗應用程式。 公司通常會同時執行多個數位體驗應用程式，而且需要滿足這些應用程式的開發、測試和部署需求，同時確保營運合規性。

為了滿足開發靈活性的需求，Experience Platform提供可將單一Experience Platform執行個體分割成個別虛擬環境的沙箱，以幫助您根據自己的開發生命週期來改進數位體驗應用程式。

如需詳細資訊，請參閱[沙箱概觀](../../sandboxes/home.md)。

## 後續步驟

本檔案提供與資料控管、隱私權和安全性相關的各種Experience Platform服務和工具的概觀。 請參閱本指南中的檔案連結，深入瞭解這些功能。
