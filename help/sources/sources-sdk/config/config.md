---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；源sdk;sdk;SDK
title: 自助源（批處理SDK）中的配置選項
topic-legacy: overview
description: 本文檔概述了使用自助源（批處理SDK）所需準備的配置。
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---

# 自助源（批處理SDK）中的配置選項

本文檔概述了使用自助源（批處理SDK）所需準備的配置。

## 連接規範

連接規範返回源的連接器屬性。 它們包括與建立基本連接和源連接相關的驗證規範以及分配給特定源的固定連接規範ID。 連接規範與租戶和組織無關。 典型的連接規範包含有關給定源的基本資訊，以及三個不同的部分： `authSpec`。 `sourceSpec`, `exploreSpec`。

| 規格 | 說明 |
| --- | --- |
| `authSpec` | 的 `authSpec` array包含有關將源連接到平台所需的身份驗證參數的資訊。 任何給定源都可支援多種不同類型的身份驗證。 |
| `sourceSpec` | 的 `sourceSpec` 陣列包含與源相關的一般資訊，包括有關在UI中顯示源所需的屬性、文檔連結以及有關分頁、標題、正文和調度的參數的資訊。 而且， `sourceSpec` 描述了從基連接建立源連接所需參數的模式，並且是建立源連接所必需的。 |
| `exploreSpec` | 的 `exploreSpec` 陣列定義了探測和檢查源中包含的對象所需的參數。 的 `exploreSpec` 還定義在探索和檢查對象時返回的響應格式。 |

{style=&quot;table-layout:auto&quot;}

## 填充連接規範值

連接規範可分為三個不同部分：驗證規範、源規範和瀏覽規範。

有關如何填充連接規範各部分值的說明，請參閱以下文檔：

* [配置身份驗證規範](./authspec.md)
* [配置源規範](./sourcespec.md)
* [配置瀏覽規範](./explorespec.md)
