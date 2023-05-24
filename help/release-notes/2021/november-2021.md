---
title: Adobe Experience Platform發行說明2021年11月
description: 2021年11月為Adobe Experience Platform發佈的說明。
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
- [(Beta)通過即席激活API激活受眾段以批處理目標](#ad-hoc-activation)

## 對現有功能的更新

Adobe Experience Platform 現有功能更新：

- [Attribution AI](#attribution-ai)
- [客戶AI](#customer-ai)

### Real-Time Customer Data Platform B2B 版本 {#B2B}

**發行日期：2021 年 11 月 12 日**

Real-Time CDPB2B版本以Real-time Customer Data Platform(Real-Time CDP)為基礎，專門為以企業對企業服務模式運營的營銷人員而設計。 它將來自多個來源的資料匯集在一起，並將其合併到人員和帳戶配置檔案的單個視圖中。 此統一資料使營銷人員能夠精確地瞄準特定受眾，並跨所有可用渠道接觸這些受眾。

Real-Time CDPB2B版與其B2C版的Adobe Experience Platform能力有所提高。 這些改進包括對B2B使用案例的體驗資料模型(XDM)的改進、對身份解析和配置檔案分段的升級，以及定製的連接器和Marketo Engage目標。 Marketo連接器允許B2B品牌將其業界領先的B2B接觸資料與行為資訊相連，以培育銷售線索並增強基於客戶的營銷運作。

-[新的B2B和B2P版本](#editions)
-[新的Marketo資料源和目標連接器](#marketo)
-[標準B2B XDM](#XDM)

### 新的B2B和B2P版本 {#editions}

新的B2B和B2P版本可供購買，這些版本為Real-Time CDP和平台激活產品提供B2B資料和功能。

要瞭解有關Real-Time CDPB2B版的詳細資訊，請參閱 [概述](../../rtcdp/overview.md)。

### 新的Marketo資料源和目標連接器 {#marketo}

新的Marketo資料源和目標連接器將Marketo資料流傳輸到平台和平台受眾，返回Marketo。 適用於所有平台用戶。

| 功能 | 說明 |
|----------|-------------|
| Marketo Engage源連接器 | 的 [Marketo Engage源連接器](../../sources/connectors/adobe-applications/marketo/marketo.md) 使營銷商能夠將來自一個或多個Marketo實例的資料無縫地接收到其Adobe Experience Platform實例中，並為銷售線索管理和B2B營銷商提供一個完整的解決方案。 |
| Marketo Engage目標 | 的 [Marketo](../../destinations/catalog/adobe/marketo-engage.md) 使營銷商能夠將在Adobe Experience Platform建立的段推送到Marketo，在那裡它們將顯示為靜態清單。 |

### 標準B2B XDM {#XDM}

標準B2B XDM類、欄位組和資料類型適用於所有平台用戶。

| 功能 | 說明 |
|-----------|--------------|
| 標準B2B XDM類 | Real-time Customer Data PlatformB2B版提供了幾種標準XDM，它們可捕獲關於基本B2B資料實體的詳細資訊，如客戶、機會、市場活動等。 |

查看 [Real-time Customer Data PlatformB2B版中的架構](../../rtcdp/schemas/b2b.md) 文檔，以瞭解有關捕獲B2B資料實體的詳細資訊。

### (Beta)通過即席激活API激活受眾段以批處理目標 {#ad-hoc-activation}

該即席激活API允許營銷者以快速和有效的方式以寫程式方式將受眾段激活到目的地，以用於需要立即激活的情況。 僅支援即席受眾激活 [基於批檔案的目標](../../destinations/destination-types.md#file-based) 目前處於Beta狀態。 有關詳細資訊，請參見 [即席激活API文檔](../../destinations/api/ad-hoc-activation-api.md)。

### Attribution AI {#attribution-ai}

Attribution AI 可將點數歸因到促成轉換事件的接觸點。 行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

| 功能 | 說明 |
|-----------|---------------|
| 支援多個資料集 | Attribution AI現在可以輕鬆地在用戶介面中直接攝取多個資料集，而無需映射和拼接每個資料集。 這一新的省時功能通過來自多個資料集的更豐富的資料，提供了更強大、更準確的得分。 |
| 媒體頻道和活動欄位映射 | Attribution AI現在支援媒體頻道和活動欄位的映射。 資料集之間的媒體通道映射改進了從Attribution AI中得到的洞察力，並有助於提供更清晰、易於解釋的結果。 |

有關Attribution AI的詳細資訊，請參閱 [Attribution AI文檔](../../intelligent-services/attribution-ai/overview.md)。

### 客戶AI {#customer-ai}

在Real-time Customer Data Platform提供的客戶AI用於生成定制傾向得分，如按比例對單個配置檔案進行流失和轉換。 不必將企業需求轉換為機器學習問題、挑選演算法、培訓或部署，就能達成上述目的。

**已更新功能**

| 功能 | 說明 |
|-----------|-------------|
| 支援多個資料集 | 客戶AI現在可以輕鬆地直接在UI中攝取多個資料集，而無需映射和拼接每個資料集。 這一新的省時功能通過來自多個資料集的更豐富的資料，提供了更強大、更準確的得分。 |
| 自定義配置檔案屬性 | 客戶AI現在支援在資料中定義自定義配置檔案資料集欄位（帶有時間戳）以及標準事件欄位。 使用此選項可以添加您認為具有影響力的附加配置檔案屬性，這些屬性可能會提高模型的質量並提供更準確的結果。 |

有關客戶AI的詳細資訊，請參閱 [客戶AI文檔](../../intelligent-services/customer-ai/overview.md)。
