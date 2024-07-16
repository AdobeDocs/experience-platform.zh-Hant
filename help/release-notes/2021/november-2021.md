---
title: Adobe Experience Platform發行說明2021年11月
description: Adobe Experience Platform 2021年11月版本注意事項。
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 20%

---

# Adobe Experience Platform 發行說明

**發行日期： 2021年11月17日**

## 新功能

Adobe Experience Platform中的新功能：

- [Real-Time Customer Data Platform B2B 版本](#B2B)
- [(Beta)透過臨機啟動API啟用批次目的地的受眾區段](#ad-hoc-activation)

## 現有功能的更新

Adobe Experience Platform 現有功能的更新：

- [Attribution AI](#attribution-ai)
- [Customer AI](#customer-ai)

### Real-Time Customer Data Platform B2B 版本 {#B2B}

**發行日期： 2021年11月12日**

在 Real-Time Customer Data Platform (Real-Time CDP) 上建置的 Real-Time CDP B2B 版本是專為採用企業對企業服務模式操作的行銷人員所建置的。它將來自多個來源的資料集中在一起，並將其合併成包含人員和帳戶設定檔的單一檢視。這種統一的資料讓行銷人員可以精確地以特定對象為目標，並在所有可用的管道中和這些對象互動。

有各種Adobe Experience Platform功能的改善，可區分Real-Time CDP B2B版本與其B2C對應版本。 其中包括改善B2B使用案例的Experience Data Model (XDM)、升級身分解析和設定檔細分，以及自訂的聯結器和Marketo Engage目的地。 Marketo聯結器可讓B2B品牌將其領先業界的B2B參與資料與行為資訊連結，以培育銷售機會及增強以帳戶為基礎的行銷作業。

-[新的B2B和B2P版本](#editions)
-[新的Marketo資料來源和目的地聯結器](#marketo)
-[標準B2B XDM](#XDM)

### 新B2B和B2P版本 {#editions}

您可購買將B2B資料與功能整合至Real-Time CDP和Platform Activation產品的新B2B和B2P版本。

若要進一步瞭解Real-Time CDP B2B版本，請參閱[總覽](../../rtcdp/overview.md)。

### 全新Marketo資料來源和目的地聯結器 {#marketo}

新的Marketo資料來源和目的地聯結器可將Marketo資料串流至Platform，並將Platform受眾傳回Marketo。 適用於所有Platform使用者。

| 功能 | 說明 |
|----------|-------------|
| Marketo Engage來源聯結器 | [Marketo Engage來源聯結器](../../sources/connectors/adobe-applications/marketo/marketo.md)可讓行銷人員順暢地將一或多個Marketo執行個體的資料擷取到其Adobe Experience Platform執行個體，並提供適用於潛在客戶管理和B2B行銷人員的完整解決方案。 |
| Marketo Engage目的地 | [Marketo目的地](../../destinations/catalog/adobe/marketo-engage.md)可讓行銷人員將在Adobe Experience Platform中建立的區段推送至Marketo，以便顯示為靜態清單。 |

### 標準B2B XDM {#XDM}

標準B2B XDM類別、欄位群組和資料型別適用於所有Platform使用者。

| 功能 | 說明 |
|-----------|--------------|
| 標準B2B XDM類別 | Real-time Customer Data Platform B2B Edition提供數個標準XDM，可擷取基本B2B資料實體的詳細資訊，例如帳戶、機會、促銷活動等。 |

請參閱Real-time Customer Data Platform B2B Edition](../../rtcdp/schemas/b2b.md)檔案中的[結構描述，深入瞭解如何擷取B2B資料實體。

### (Beta)透過臨機啟動API啟用批次目的地的受眾區段 {#ad-hoc-activation}

臨機啟動API可讓行銷人員針對需要立即啟動的情況，以快速且有效率的方式以程式設計方式啟用目的地的受眾區段。 僅[批次檔案型目的地](../../destinations/destination-types.md#file-based)支援隨選對象啟用，目前為測試版。 如需詳細資訊，請參閱[臨機啟動API檔案](../../destinations/api/ad-hoc-activation-api.md)。

### Attribution AI {#attribution-ai}

Attribution AI 可將點數歸因到促成轉換事件的接觸點。行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

| 功能 | 說明 |
|-----------|---------------|
| 支援多個資料集 | Attribution AI現在可以輕鬆地直接在UI中擷取多個資料集，而不需要對應和拼接每個資料集。 這項新的省時功能提供更強大且更精確的分數，包含來自多個資料集的更豐富資料。 |
| 媒體頻道和行銷活動欄位對應 | Attribution AI現在支援對應媒體頻道與行銷活動欄位。 資料集之間的媒體管道對應可改善從Attribution AI衍生的深入分析，並提供更清楚且易於解讀的結果。 |

如需Attribution AI的詳細資訊，請參閱[Attribution AI檔案](../../intelligent-services/attribution-ai/overview.md)。

### Customer AI {#customer-ai}

Real-time Customer Data Platform中可用的Customer AI可產生自訂傾向分數，例如大規模個別設定檔的流失和轉換情形。 不必將企業需求轉換為機器學習問題、挑選演算法、訓練或部署，即可達成上述目的。

**更新的功能**

| 功能 | 說明 |
|-----------|-------------|
| 支援多個資料集 | Customer AI現在可以輕鬆地直接在UI中擷取多個資料集，而不需要對應和拼接每個資料集。 這項新的省時功能提供更強大且更精確的分數，包含來自多個資料集的更豐富資料。 |
| 自訂設定檔屬性 | 除了標準事件欄位外，Customer AI現在還支援在資料中定義自訂設定檔資料集欄位（含時間戳記）。 使用此選項可讓您新增您認為有影響力的其他設定檔屬性，這些屬性可能會改善模型的品質，並提供更準確的結果。 |

如需Customer AI的詳細資訊，請參閱[Customer AI檔案](../../intelligent-services/customer-ai/overview.md)。
