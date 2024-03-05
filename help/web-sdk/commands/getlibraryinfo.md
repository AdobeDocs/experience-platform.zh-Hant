---
title: getLibraryInfo
description: 擷取目前Web SDK程式庫版本的相關資訊。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

此 `getLibraryInfo` command會提供您目前所使用Web SDK程式庫版本的相關資訊。 您可以使用此命令來追蹤您部署到不同Web屬性的Web SDK版本。

## 使用Web SDK標籤擴充功能的程式庫資訊

標籤擴充功能不提供傳送此命令的介面。 依照JavaScript程式庫語法，使用自訂程式碼編輯器。

如果您使用標籤擴充功能執行此命令，則會同時包含標籤擴充功能版本和程式庫版本，並串連至 `+` 符號。 首先列出Web SDK程式庫版本，然後是標籤擴充功能版本。

## 使用Web SDK JavaScript程式庫的程式庫資訊

執行 `getLibraryInfo` 命令來呼叫Web SDK的已設定執行個體。 此命令通常會與JavaScript Promise搭配，讓您擷取其所填入的物件。

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## 回應物件

如果您決定 [處理回應](command-responses.md) 使用此命令，回應物件中可以使用下列屬性：

* **`libraryInfo.commands`**：此版本的Web SDK支援的命令陣列。
* **`libraryInfo.configs`**：此版本的Web SDK支援的一系列組態設定。
* **`libraryInfo.version`**：Web SDK程式庫的版本。
