---
solution: Experience Platform
title: 教戰手冊的已知限制
description: 進一步了解教戰手冊的已知問題和常見問題，以及如何疑難排解
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: e24334bb4ac788770abe20ec2324efa1e64bc0e8
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---


# 已知限制 {#known-limitations}

瞭解如何在使用使用案例教戰手冊時疑難排解錯誤，並瞭解一般可用性版本的已知限制。

## 已知限制

建立行動手冊例項並產生資產時，會出現幾項已知限制。

* 對於產生的結構描述，如果結構描述是在行動手冊的一個例項中產生，並且您編輯它，則為另一個結構描述 *不會* 如果您啟用行動手冊的另一個例項，則會產生行動手冊。 請改為繼續使用您在執行個體中編輯的結構描述。

* 使用時 [資料感知功能](/help/use-case-playbooks/playbooks/data-awareness.md) 若要將結構描述從啟發性的沙箱提升至開發沙箱，您可能會看到類似以下的一些錯誤：

![結構描述對應工作流程中顯示的錯誤。](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

這是因為從您的結構描述產生的某些欄位，不存在於您要複製至的開發沙箱的結構描述中。 查詢這些欄位。 接著，返回開發沙箱，您可以：

* 建立包含這些欄位的新欄位群組或
* 在您的結構描述中加入標準、預先定義的欄位群組，包括缺少的欄位。

將這些欄位納入開發沙箱的結構描述後，請返回工作流程，將結構描述欄位從勵志沙箱複製到開發沙箱。 錯誤已消失。

如需詳細資訊，請觀看以下影片以建立結構描述欄位群組。

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
