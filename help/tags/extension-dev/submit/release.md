---
title: 發行擴充功能
description: 瞭解如何在Adobe Experience Platform中私下或公開發佈標籤擴充功能。
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 2152cf98d9809654cca7abd7b8469a72e8387b2a
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 25%

---

# 發行擴充功能

>[!NOTE]
>
>Adobe Experience Platform Launch 已進行品牌重塑，現在是 Adobe Experience Platform 中的一套資料彙集技術。 因此，這些產品文件都推出多項幾術語變更。如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

完成測試和檔案整理後，擴充功能即可發行。 目前可執行的發行有兩種：

- **私人發行**：完成的擴充功能可供您公司內的所有屬性使用，但不適用於Adobe Experience Platform中的任何其他公司。
- **公開發行**：所有Adobe Experience Platform使用者皆可在公開Marketplace中取得已完成的擴充功能。

>[!NOTE]
>
>擴充功能一經發行即無法變更，也無法解除發行。  在發行後若要進行錯誤修正和功能新增，必須要 `POST` 新版的擴充功能套件，並且對這個新版本執行前述的測試和發行步驟。

您必須先以私人擴充功能的形式發行擴充功能，才能公開發行。

## 私人發行

要發行具有私人可用性的擴充功能，最簡單的方式是使用[標籤擴充功能發行者](https://www.npmjs.com/package/@adobe/reactor-releaser)。

```bash
npx @adobe/reactor-releaser
```

`npx`可讓您下載並執行npm套件，而無需在機器上實際安裝。 這是執行發行者的最簡單方法。

>[!NOTE]
> 根據預設，發行者需要伺服器對伺服器Oauth流程的Adobe I/O認證。 舊版`jwt-auth`認證
> 可藉由執行`npx @adobe/reactor-releaser@v3.1.3`使用，直到2025年1月1日停止使用。 必要的引數
> 若要執行`jwt-auth`版本，可在[這裡](https://github.com/adobe/reactor-releaser/tree/9ea66aa2c683fe7da0cca50ff5c9b9372f183bb5)找到。

發行者僅需要您輸入幾項資訊。 可以從Adobe I/O主控台擷取`clientId`和`clientSecret`。 導覽至I/O主控台中的[整合頁面](https://console.adobe.io/integrations)。 從下拉式清單中選取正確的組織，尋找正確的整合，然後選取&#x200B;**[!UICONTROL 檢視]**。

- 您的`clientId`是什麼？ 請從I/O主控台複製並貼上。
- 您的`clientSecret`是什麼？ 請從I/O主控台複製並貼上。

發行者將會從您的擴充功能資訊清單中讀取`name`和`platform`欄位，並在API中查詢Development可用性中是否有相符的擴充功能套件。
發行者接著會要求您確認，其是否找到您要發行以供私人使用的正確擴充功能套件。

如果您想要直接使用API以私密可用性發行擴充功能，請參閱API檔案中[私密發行擴充功能套件](../../api/endpoints/extension-packages.md/#private-release)的範例呼叫，以取得詳細資訊。

## 公開發行

在完成私人發行後，您可要求 Adobe 將其公開發行。如此，您的擴充功能就會在公開目錄中提供。 任何資料收集使用者都可將您的擴充功能安裝至任何屬性。

請填妥[公開發行申請表](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest)，開始進行發行程序。
