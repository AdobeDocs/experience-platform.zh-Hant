---
solution: Experience Platform
title: 行業資料模型概述
description: 瞭解使用標準體驗資料模型(XDM)元件可構建的各種行業垂直行業的標準化資料模型。
exl-id: 8fa9a610-36b5-470f-ad63-f2a4a060e0f1
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# 行業資料模型概述

體驗資料模型(XDM)允許您建立高度可定製的架構，以捕獲與您的業務相關的關鍵客戶體驗資料。 為幫助簡化為符合XDM的資料建模過程，Adobe Experience Platform提供了一套通用的標準XDM元件，這些元件捕獲了在多個行業中常用的概念。

>[!NOTE]
>
>新的標準XDM元件正在不斷發佈，以滿足最佳的消費者需求。 對於最新元件的清單，您可以 [瀏覽UI中的現有資源](../../ui/explore.md) 或參考 [正式XDM儲存庫](https://github.com/adobe/xdm/tree/master/components) 在GitHub上。

根據您的業務所處的行業，某些XDM元件將比其他元件更適合您的需求。 此外，您在XDM架構之間建立的關係將因您所在行業而異。

為了幫助根據特定行業指導您的資料建模策略，本指南提供了幾個受支援行業的實體關係圖(ERD)的參考。

## 先決條件

要閱讀本指南中引用的ERD，您必須瞭解XDM元件如何交互以形成架構以及XDM架構如何作為一個整體在Experience Platform中運行。 確保在繼續之前已閱讀以下概述文檔：

* [XDM系統概述](../../home.md):瞭解XDM在平台生態系統中的運行方式。
* [架構組合的基礎](../../schema/composition.md):瞭解XDM元件（如架構欄位組、類和資料類型）如何對架構結構以及標識欄位的角色作出貢獻。

還建議您查看 [資料建模最佳做法指南](../../schema/best-practices.md) 有關如何將資料映射到XDM的一般指導。

## 行業資料模型ERDs {#erds}

ERD適用於以下行業垂直領域：

* [[!UICONTROL 零售業]](./retail.md)
* [[!UICONTROL 金融服務]](./financial.md)
* [[!UICONTROL 保健]](./healthcare.md)
* [[!UICONTROL 電信]](./telecom.md)
* [[!UICONTROL 旅行和招待]](./travel-hospitality.md)

## 後續步驟

本文檔概述了行業資料模型ERDs以及如何解釋它們。 要查看ERD，請從上面的清單中選擇一個。
