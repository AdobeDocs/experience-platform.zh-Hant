---
solution: Experience Platform
title: 教戰手冊的已知限制和疑難排解問題
description: 進一步了解教戰手冊的已知問題和常見問題，以及如何疑難排解
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: d6be5d3e21ea924ff98c400b972709b1f60c25eb
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 2%

---


# 疑難排解和已知限制 {#troubleshooting-known-limitations}

## 疑難排解 {#troubleshooting}

### 未設定Adobe Journey Optimizer表面

建立教戰手冊的執行個體時，您可能會看到下方顯示的訊息。

![疑難排解](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

這是因為Journey Optimizer教戰手冊會為電子郵件、推播和簡訊頻道建立訊息。 閱讀 [開始使用](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) 設定不同曲面的指南。

### 狀態 *失敗* 建立新執行個體時

如果您在嘗試建立執行個體時看到失敗訊息，這可能是因為您的管理員未授予您必要的使用者許可權。 行動手冊包含許多不同的資產，您的使用者需要許可權才能建立這些資產，才能成功建立行動手冊的執行個體。 請參閱 [許可權](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) 本指南中有關如何設定許可權的區段。

## 已知限制

建立行動手冊例項並產生資產時，會出現幾項已知限制。

* 對於產生的結構描述，如果結構描述是在行動手冊的一個例項中產生，並且您編輯它，則為另一個結構描述 *不會* 如果您啟用行動手冊的另一個例項，則會產生行動手冊。 請改為繼續使用您在執行個體中編輯的結構描述。

* 使用時 [資料感知功能](/help/use-case-playbooks/playbooks/data-awareness.md) 若要將結構描述從啟發性的沙箱提升至開發沙箱，您可能會看到類似以下的一些錯誤：

![schema-error](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png)

這是因為從您的結構描述產生的某些欄位，不存在於您要複製至的開發沙箱的結構描述中。 查詢這些欄位。 接著，返回開發沙箱，您可以：

* 建立包含這些欄位的新欄位群組或
* 在您的結構描述中加入標準、預先定義的欄位群組，包括缺少的欄位。

將這些欄位納入開發沙箱的結構描述後，請返回工作流程，將結構描述欄位從勵志沙箱複製到開發沙箱。 錯誤已消失。

如需詳細資訊，請觀看以下影片以建立結構描述欄位群組。

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
