---
solution: Experience Platform
title: Adobe Experience Platform multi-cloud概述
description: 瞭解在Microsoft Azure和Amazon Web Services上執行Experience Platform有何差異。
source-git-commit: d3654573cec338f173d151fd5e62ef5c8b893c11
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 3%

---


# Adobe Experience Platform multi-cloud概述

Adobe Experience Platform是多雲端產品，可讓您選擇在[[!DNL Microsoft Azure]](https://azure.microsoft.com/en-us)或[[!DNL Amazon Web Services (AWS)]](https://aws.amazon.com/)上執行。 此彈性可讓您選擇最符合業務與技術需求的方式。

>[!AVAILABILITY]
>
>在Amazon Web Services (AWS)上執行的Adobe Experience Platform目前可供有限數量的客戶使用。 若要進一步瞭解AWS上的Experience Platform，請聯絡您的Adobe客戶團隊。

本頁提供兩種可用雲端基礎建設的高層級概觀，並包含如何為您的企業選擇正確基礎建設的指引。

## 哪個雲端實作適合我？ {#which-cloud-is-right}

在Azure或AWS上選擇Experience Platform取決於您業務的特定因素：

* **業務和技術需求**：評估您組織的需求和長期雲端策略。
* **現有基礎結構**：考慮您目前的雲端基礎結構和整合需求。
* **雲端技術依賴**：如果您的業務嚴重依賴Microsoft技術，Azure可能更適合。 如果您更依賴Amazon服務，AWS可能是更好的選擇。
* **資料常駐考量事項**：評估您組織的資料常駐需求，並確保所選的雲端平台提供符合這些法規的地區。

基於上述因素，使用此簡化的決策樹，協助您根據業務需求決定正確的雲端實作。

![顯示託管位置之地理分佈的影像。](assets/multi-cloud/diagram-cloud.png){align="center" zoomable="yes"}

## 託管位置 {#available-cloud-regions}

選擇合適的雲端區域對於滿足資料駐留需求及確保最佳效能至關重要。

![顯示託管位置之地理分佈的影像。](assets/multi-cloud/hosting-locations-map.png){align="center" zoomable="yes"}

Experience Platform可在6個Microsoft Azure代管位置和1個Amazon Web Services (AWS)代管位置使用，並透過分散在世界各地的七個[Edge Network節點](../collection/home.md#edge)將資料路由至Adobe服務。

### Microsoft Azure地區 {#azure-regions}

下表指出託管Experience Platform的Microsoft Azure區域。

| 國家/地區 | 地區代碼 | 位置 |
|---------|-------------|----------|
| 美國 | VA7 | 維吉尼亞 |
| 英國 | GBR9 | 倫敦 |
| 荷蘭 | NDL2 | 阿姆斯特丹 |
| 加拿大 | CAN2 | 多倫多 |
| 印度 | IND2 | 馬哈拉施特拉邦 |
| 澳大利亞 | AUS5 | 新南威爾斯州 |

{style="table-layout:auto"}

### Amazon Web Services (AWS)地區 {#aws-regions}

下表指出託管Experience Platform的AWS區域。 請定期回來檢視，以瞭解是否已新增其他位置。

| 國家/地區 | 地區代碼 | 位置 |
|---------|-------------|----------|
| 美國 | VA6 | 維吉尼亞 |

{style="table-layout:auto"}

## 功能同位 {#feature-parity}

Adobe致力於為在Experience Platform上執行的所有應用程式提供跨雲端平台的功能對等功能，例如：

* [Real-Time Customer Data Platform](../rtcdp/home.md)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/ajo-home)
* [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-landing)

不過，Azure和AWS實作之間的某些功能可能會有所不同。 以下章節及產品檔案其他部分（如適用）會概述這些差異。

### 在Microsoft Azure和AWS上執行Experience Platform的差異 {#azure-aws-differences}

下表著重說明在Microsoft Azure和AWS上執行Experience Platform的主要差異。

| 特色/功能 | Microsoft Azure | Amazon Web Services |
| --- | --- | --- |
| [符合HIPAA規範](https://www.adobe.com/trust/compliance/hipaa-ready.html) | 支援 | 不支援 |
| [來源聯結器的目錄](/help/sources/home.md) | 支援來源目錄中的所有聯結器 | 可用的來源聯結器數量有限。 AWS實作可用的任何來源聯結器都會在其各自檔案頁面的頁面頂端註解中出現。 |

{style="table-layout:auto"}

<!-- To be determined if we need to add this part about the AI Assistant 

| [Experience Platform AI Assistant](/help/ai-assistant/home.md) | Supported | Not supported |

-->

## 結論 {#conclusion}

Experience Platform提供在Microsoft Azure或Amazon Web Services上執行的選項，讓您擁有彈性和選擇。 評估您的業務需求和現有基礎架構，以針對使用哪個雲端平台做出明智的決策。
