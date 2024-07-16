---
title: 發行擴充功能
description: 瞭解如何在Adobe Experience Platform中私下或公開發佈標籤擴充功能。
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 60d88be5d710314cdc6900f4b63643c740b91fa6
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 32%

---

# 發行擴充功能

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../term-updates.md)，以取得術語變更的彙總參考資料。

完成測試和檔案整理後，擴充功能即可發行。 目前可執行的發行有兩種：

- **私人發行**：完成的擴充功能可供您公司內的所有屬性使用，但不適用於Adobe Experience Platform中的任何其他公司。
- **公開發行**：所有Adobe Experience Platform使用者皆可在公開Marketplace中取得已完成的擴充功能。

>[!NOTE]
>
>擴充功能一經發行即無法變更，也無法解除發行。  在發行後若要進行錯誤修正和功能新增，必須要 `POST` 新版的擴充功能套件，並且對這個新版本執行前述的測試和發行步驟。

您必須先以私人擴充功能的形式發行擴充功能，才能公開發行。

## 私人發行

要發行具有私人可用性的擴充功能，最簡單的方式是使用[標籤擴充功能發行者](https://www.npmjs.com/package/@adobe/reactor-releaser)。 如需詳細指示，請參閱其文件。

如果您想要直接使用API以私密可用性發行擴充功能，請參閱API檔案中[私密發行擴充功能套件](../../api/endpoints/extension-packages.md/#private-release)的範例呼叫，以取得詳細資訊。

## 公開發行

在完成私人發行後，您可要求 Adobe 將其公開發行。如此，您的擴充功能就會在公開目錄中提供。 任何資料收集使用者都可將您的擴充功能安裝至任何屬性。

請填妥[公開發行申請表](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest)，開始進行發行程序。
