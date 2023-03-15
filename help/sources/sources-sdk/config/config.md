---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
title: 自助來源（批次SDK）中的設定選項
description: 本檔案概述使用自助來源（批次SDK）所需準備的設定。
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 自助來源（批次SDK）中的設定選項

本檔案概述使用自助來源（批次SDK）所需準備的設定。

## 連接規範

連接規範返回源的連接器屬性。 它們包括與建立基本連接和源連接相關的驗證規範，以及分配給特定源的固定連接規範ID。 連線規格不受租用戶和組織限制。 典型的連接規範包含有關給定源的基本資訊以及三個不同的部分： `authSpec`, `sourceSpec`，和 `exploreSpec`.

| 規格 | 說明 |
| --- | --- |
| `authSpec` | 此 `authSpec` array包含將源連接到平台所需的身份驗證參數的資訊。 任何給定的源都可支援多種不同類型的身份驗證。 |
| `sourceSpec` | 此 `sourceSpec` array包含與來源相關的一般資訊，包括在UI中呈現來源所需屬性的相關資訊、檔案連結，以及關於分頁、標題、內文和排程的參數。 此外， `sourceSpec` 描述了從基連接建立源連接所需的參數的架構，並且是建立源連接所必需的。 |
| `exploreSpec` | 此 `exploreSpec` array定義探索和檢查源中包含的對象所需的參數。 此 `exploreSpec` 也會定義探索和檢查對象時傳回的回應格式。 |

{style="table-layout:auto"}

## 填充連接規範值

連接規範可分為三個不同部分：驗證規範、源規範和瀏覽規範。

有關如何填入連接規範每個部分的值的說明，請參閱以下文檔：

* [配置身份驗證規範](./authspec.md)
* [配置源規範](./sourcespec.md)
* [配置瀏覽規範](./explorespec.md)
