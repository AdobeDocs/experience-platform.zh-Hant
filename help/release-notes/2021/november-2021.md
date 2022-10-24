---
title: Adobe Experience Platform發行說明2021年11月
description: 2021年11月Adobe Experience Platform發行說明。
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 12%

---

# Adobe Experience Platform 發行說明

**發行日期：2021 年 11 月 17 日**

## 新功能

Adobe Experience Platform的新功能：

- [Real-Time Customer Data Platform B2B 版本](#B2B)
- [（測試版）透過臨機啟動API啟動對象區段以批次目的地](#ad-hoc-activation)

## 更新現有功能

Adobe Experience Platform 現有功能更新：

- [Attribution AI](#attribution-ai)
- [Customer AI](#customer-ai)

### Real-Time Customer Data Platform B2B 版本 {#B2B}

**發行日期：2021 年 11 月 12 日**

Real-Time CDP B2B Edition以Real-time Customer Data Platform(Real-Time CDP)為基礎，專為以企業對企業服務模式運作的行銷人員所打造。 它匯集了來自多個來源的資料，並將其結合為人員和帳戶設定檔的單一檢視。 此統一的資料可讓行銷人員精確鎖定特定對象，並參與所有可用管道中的這些對象。

Real-Time CDP B2B版與其B2C版本有所不同，Adobe Experience Platform的各種功能也有所改善。 其中包括針對B2B使用案例改善Experience Data Model(XDM)、升級為身分解析和設定檔分段，以及自訂的連接器和Marketo Engage目的地。 Marketo連接器可讓B2B品牌將其業界領先的B2B參與資料與行為資訊連結，以培育銷售機會並增強以帳戶為基礎的行銷作業。

-[全新B2B和B2P版本](#editions)
-[全新Marketo資料來源和目的地連接器](#marketo)
-[標準B2B XDM](#XDM)

### 全新B2B和B2P版本 {#editions}

現已推出新的B2B和B2P版本，為Real-Time CDP和Platform Activation產品提供B2B資料和功能。

若要進一步了解Real-Time CDP B2B版，請參閱 [概述](../../rtcdp/overview.md).

### 全新Marketo資料來源和目的地連接器 {#marketo}

新的Marketo資料來源和目的地連接器會將Marketo資料串流至Platform和Platform對象，並傳回Marketo。 適用於所有平台使用者。

| 功能 | 說明 |
|----------|-------------|
| Marketo Engage源連接器 | 此 [Marketo Engage源連接器](../../sources/connectors/adobe-applications/marketo/marketo.md) 可讓行銷人員將一或多個Marketo執行個體的資料流暢內嵌至其Adobe Experience Platform執行個體，並為銷售機會管理和B2B行銷人員提供完整的解決方案。 |
| Marketo Engage目標 | 此 [Marketo目的地](../../destinations/catalog/adobe/marketo-engage.md) 可讓行銷人員將在Adobe Experience Platform中建立的區段推送至Marketo，這些區段會顯示為靜態清單。 |

### 標準B2B XDM {#XDM}

所有Platform使用者皆可使用標準B2B XDM類別、欄位群組和資料類型。

| 功能 | 說明 |
|-----------|--------------|
| 標準B2B XDM類別 | Real-time Customer Data Platform B2B版提供數種標準XDM，可擷取關於基本B2B資料實體（例如帳戶、機會、行銷活動等）的詳細資訊。 |

請參閱 [Real-time Customer Data Platform B2B版中的結構描述](../../rtcdp/schemas/b2b.md) 檔案，進一步了解擷取B2B資料實體。

### （測試版）透過臨機啟動API啟動對象區段以批次目的地 {#ad-hoc-activation}

臨機啟動API可讓行銷人員針對需要立即啟動的情況，以快速且有效的方式，以程式設計方式將對象區段啟用至目的地。 僅支援隨選對象啟動 [批次檔案型目的地](../../destinations/destination-types.md#file-based) 目前為測試版。 如需詳細資訊，請參閱 [臨機啟動API檔案](../../destinations/api/ad-hoc-activation-api.md).

### Attribution AI {#attribution-ai}

Attribution AI 可將點數歸因到促成轉換事件的接觸點。 行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

| 功能 | 說明 |
|-----------|---------------|
| 支援多個資料集 | Attribution AI現在可以直接在UI中輕鬆內嵌多個資料集，無需對應及拼接每個資料集。 這項新的省時功能提供來自多個資料集的豐富資料，提供更強大、更精確的分數。 |
| 媒體頻道和行銷活動欄位對應 | Attribution AI現在支援媒體頻道和行銷活動欄位的對應。 資料集之間的媒體管道對應可改善衍生自Attribution AI的深入分析，並協助提供更清楚、易於解讀的結果。 |

如需Attribution AI的詳細資訊，請參閱 [Attribution AI檔案](../../intelligent-services/attribution-ai/overview.md).

### Customer AI {#customer-ai}

Real-time Customer Data Platform提供的Customer AI可產生自訂傾向分數，例如大規模個別設定檔的流失和轉換。 不必將企業需求轉換為機器學習問題、挑選演算法、培訓或部署，就能達成上述目的。

**更新功能**

| 功能 | 說明 |
|-----------|-------------|
| 支援多個資料集 | Customer AI現在可以直接在UI中輕鬆內嵌多個資料集，而無須對應並拼接每個資料集。 這項新的省時功能提供來自多個資料集的豐富資料，提供更強大、更精確的分數。 |
| 自訂設定檔屬性 | 除了標準事件欄位外，Customer AI現在支援在您的資料中定義自訂設定檔資料集欄位（含時間戳記）。 使用此選項可讓您新增您認為有影響的其他設定檔屬性，這可能會改善模型品質，並提供更精確的結果。 |

如需Customer AI的詳細資訊，請參閱 [Customer AI檔案](../../intelligent-services/customer-ai/overview.md).
