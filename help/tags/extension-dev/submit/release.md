---
title: 釋放擴展
description: 瞭解如何在Adobe Experience Platform私下或公開發佈標籤擴展。
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 60d88be5d710314cdc6900f4b63643c740b91fa6
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 44%

---

# 發行擴充功能

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

測試和記錄完成後，擴展即可發佈。 目前可執行的發行有兩種：

- **私有版本**:已完成的展期可供您公司內的所有物業使用，但不可供Adobe Experience Platform的任何其他公司使用。
- **公開發佈**:完成的擴展功能可在公開市場上為所有Adobe Experience Platform用戶提供。

>[!NOTE]
>
>釋放擴展後，您不能再對其進行更改，也不能取消釋放它。  在發行後若要進行錯誤修正和功能新增，必須要 `POST` 新版的擴充功能套件，並且對這個新版本執行前述的測試和發行步驟。

您必須先以私人擴充功能的形式發行擴充功能，才能公開發行。

## 私人發行

使用私有可用性釋放擴展的最簡單方法是使用 [標籤擴展釋放器](https://www.npmjs.com/package/@adobe/reactor-releaser)。 如需詳細指示，請參閱其文件。

如果您希望直接使用API以私有可用性釋放擴展，請參閱的示例調用 [私下發佈擴展包](../../api/endpoints/extension-packages.md/#private-release) 的雙曲余弦值。

## 公開發行

在完成私人發行後，您可要求 Adobe 將其公開發行。如此，您的擴充功能就會在公開目錄中提供。任何資料收集用戶都可以將擴展安裝到任何屬性。

請填妥[公開發行申請表](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest)，開始進行發行程序。
