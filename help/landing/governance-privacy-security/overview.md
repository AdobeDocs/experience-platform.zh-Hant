---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 治理、隱私和安全概述
description: Adobe Experience Platform提供了多種服務和工具，讓您能夠放心地控制收集的體驗資料，以便遵守您的業務實踐、法律義務和開發流程。
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 2%

---

# Adobe Experience Platform的治理、隱私和安全

Adobe Experience Platform使您能夠攝取、分析、優化和操作資料，從而大大增強客戶體驗。 這些資料是巨大的、複雜的，並且極其有價值。 根據資料操作的性質、您的業務所在的法律管轄區以及您有關資料使用的組織策略，您必須仔細控制和監控客戶體驗資料的收集和使用，以保護您的業務利益。

Experience Platform提供了多種服務和工具，使您能夠放心地控制收集的體驗資料，以便遵守業務實踐、法律義務和開發流程。 以下各節介紹了這些服務中的每一項，並提供了文檔連結以獲取進一步資訊。

服務可分為三個域：

* [資料治理](#governance)
* [隱私權](#privacy)
* [安全性](#security)

## 資料治理 {#governance}

資料治理是一個基本概念，它與Experience Platform中的所有功能交織在一起。 資料治理代表了您在整個平台過程中控制和理解資料的能力。 這包括維護資料質量、資料沿襲、資料編目等。

### Adobe Experience Platform資料治理 {#data-governance}

作為平台服務，Adobe Experience Platform資料治理允許您管理客戶資料並確保遵守適用於資料使用的法規、限制和策略。 它在Experience Platform的不同級別中起著關鍵作用，包括資料使用標籤、資料使用策略、策略實施和資料沿襲。

查看 [資料治理概述](../../data-governance/home.md) 的子菜單。

### 目錄和資料集 {#catalog}

目錄服務是平台內資料位置和沿襲的記錄系統。 雖然所有被攝取到Experience Platform中的資料都作為檔案和目錄儲存在資料湖中，但目錄保存這些檔案和目錄的元資料和說明，以便進行查找和監視。

目錄將所攝取的資料組織到資料集中，每個資料集都包含可用於標籤其所包含資料並將其分類的元資料。

查看 [目錄服務概述](../../catalog/home.md) 的子菜單。 要瞭解如何管理Experience Platform中的資料集，請參見 [資料集概述](../../catalog/datasets/overview.md)。

## 隱私權 {#privacy}

隱私是您的業務、立法者和客戶的一個關鍵問題。 由於從客戶收集的個人資料是幾乎所有Experience Platform工作流的核心，因此平台提供支援這些計畫的服務。

### Adobe Experience Platform 隱私權服務 {#privacy-service}

法律隱私法規，如歐盟的一般資料保護條例(GDPR)和加利福尼亞消費者隱私法(CCPA)授予其管轄範圍內的公民訪問和刪除您從他們那裡收集和儲存的個人資料的權利。

Adobe Experience Platform Privacy Service提供了REST風格的API和用戶介面來幫助管理這些請求。 通過Privacy Service，您可以提交訪問或刪除Adobe Experience Cloud應用程式中的私人或個人客戶資料的請求，從而促進自動遵守法律和組織隱私法規。

查看 [Privacy Service概述](../../privacy-service/home.md) 的子菜單。

### 同意處理 {#consent}

許多法律隱私法規都在資料收集、個性化和其他營銷使用案例方面引入了主動和特定同意的要求。 為了滿足這些要求，Experience Platform允許您捕獲單個客戶配置檔案中的同意資訊，並將這些首選項作為決定每個客戶資料在下游平台工作流中使用方式的因素。

要瞭解如何使用Adobe標準處理客戶同意和首選項資料，請參閱 [Experience Platform中的同意處理](./consent/adobe/overview.md)。

有關如何按照IAB透明度和同意框架(TCF)2.0處理客戶同意資料的資訊，請參閱 [平台中的IAB TCF 2.0支援](./consent/iab/overview.md)。

## 安全性 {#security}

資料的完整性和安全性對於您的業務來說是必不可少的，而這種風險需要業界領先的安全功能。 為了應對這一挑戰，平台提供了多種工具來幫助保護您的資料操作。

### 資料加密

所有平台資料在傳輸和靜止時都加密。 查看上的文檔 [平台中的資料加密](./encryption.md) 的子菜單。

### 存取控制 {#access-control}

Experience Platform使用Adobe Admin Console為各種平台功能提供基於角色的訪問控制。 此功能利用Admin Console中的產品配置檔案，將用戶與權限和沙箱連結起來。

查看 [訪問控制概述](../../access-control/home.md) 的子菜單。

### 沙箱 {#sandboxes}

Experience Platform旨在在全球範圍內豐富數字型驗應用。 公司通常並行運行多個數字型驗應用程式，需要滿足這些應用程式的開發、測試和部署需要，同時確保操作合規性。

為了滿足對開發靈活性的需要，Experience Platform提供了沙箱，可將單個平台實例分區為獨立的虛擬環境，以幫助您根據自己的開發生命週期來開發數字型驗應用程式。

如需詳細資訊，請參閱[沙箱概觀](../../sandboxes/home.md)。

## 後續步驟

本文檔概述了與資料治理、隱私和安全相關的各種平台服務和工具。 請參閱本指南中連結的文檔，以瞭解有關這些功能的詳細資訊。
