---
title: 發行擴充功能
description: 了解如何在Adobe Experience Platform中私下或公開發行標籤擴充功能。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 39%

---

# 發行擴充功能

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

完成測試和檔案分析後，擴充功能即可發行。 目前可執行的發行有兩種：

- **私人發行**:已完成的擴充功能可供您公司內的所有屬性使用，但不適用於Adobe Experience Platform中的任何其他公司。
- **公開發行**:所有Adobe Experience Platform使用者皆可在公開市集中取得已完成的擴充功能。

>[!NOTE]
>
>擴充功能一經發行即無法再進行變更，也無法解除發行。  在發行後若要進行錯誤修正和功能新增，必須要 `POST` 新版的擴充功能套件，並且對這個新版本執行前述的測試和發行步驟。

您必須先以私人擴充功能的形式發行擴充功能，才能公開發行。

## 私人發行

要透過私人可用性發行擴充功能，最簡單的方式是使用[標籤擴充功能發行器](https://www.npmjs.com/package/@adobe/reactor-releaser)。 如需詳細指示，請參閱其文件。

如果您想要直接使用API以私人可用性方式發行擴充功能，請參閱API檔案中[私下發行擴充功能套件](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/)的範例呼叫，以取得詳細資訊。

## 公開發行

在完成私人發行後，您可要求 Adobe 將其公開發行。如此，您的擴充功能就會在公開目錄中提供。任何資料收集使用者都可以將您的擴充功能安裝至任何屬性。

請填妥[公開發行申請表](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=7DRB5U)，開始進行發行程序。
