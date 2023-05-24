---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；標識；資料類型；資料類型；
solution: Experience Platform
title: 標識資料類型
description: 此文檔概述了Identity XDM資料類型。
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 3%

---

# [!UICONTROL 身份] 資料類型

[!UICONTROL 身份] 是一種標準的XDM資料類型，用於清晰地區分與數字型驗交互的人。 標識由標識提供程式建立，它本身在 `namespace` 屬性。 每個 `namespace`，標識是唯一的。

<img src="../images/data-types/identity.png" width="550" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `namespace` | 物件 | 包含單個字串欄位(`code`)，指示與提供的 `id` 屬性。 |
| `authenticatedState` | 字串 | 在觀察到的體驗事件時此標識的已驗證狀態。 查看 [附錄](#authenticatedState) 以獲取接受的值和定義。 |
| `id` | 字串 | 相關命名空間中的使用者的標識。 |
| `primary` | 布林值 | 指示這是否是個人的主要標識。 每個個人只能有一個主標識。 |
| `xid` | 字串 | 當存在時，此值表示跨命名空間標識符，該標識符在所有命名空間中所有命名空間範圍內的標識符之間都是唯一的。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 附錄

以下部分包含有關 [!UICONTROL 身份] 資料類型。

## authenticatedState的接受值 {#authenticatedState}

下表概述了 `authenticatedState` 及其相關含義：

| 值 | 說明 |
| --- | --- |
| `ambiguous` | 已驗證狀態不明確。 |
| `authenticated` | 用戶由在事件觀察時有效的登錄或類似操作標識。 |
| `loggedOut` | 用戶在以前某個時間點由登錄操作標識，但在事件觀察時未登錄。 |
