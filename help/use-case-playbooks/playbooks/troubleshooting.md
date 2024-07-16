---
solution: Experience Platform
title: 教戰手冊的已知限制和疑難排解問題
description: 進一步了解教戰手冊的已知問題和常見問題，以及如何疑難排解
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 0faf3187c0b32e0be70033e501939412ade37d7e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# 疑難排解 {#troubleshooting}

檢視使用使用案例教戰手冊時常見錯誤的疑難排解建議

## 未設定Adobe Journey Optimizer表面 {#surfaces-not-configured}

建立教戰手冊的執行個體時，您可能會看到下方顯示的訊息。

![疑難排解](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

這是因為Journey Optimizer教戰手冊會為電子郵件、推播和簡訊頻道建立訊息。 閱讀[開始使用](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer)指南，以設定不同的介面。

## 建立新執行個體時狀態&#x200B;*失敗* {#status-failed}

如果您在嘗試建立執行個體時看到失敗訊息，這可能是因為您的管理員未授予您必要的使用者許可權。 行動手冊包含許多不同的資產，您的使用者需要許可權才能建立這些資產，才能成功建立行動手冊的執行個體。 請參閱本指南的[許可權](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions)一節，瞭解如何設定許可權。

## 匯入失敗 {#import-failure}

客戶在不同測試環境中操作，有時候，從他們的環境匯入執行個體到Adobe沙箱時，可能會失敗。 若要檢視這些匯入的狀態，請從左側導覽選取「沙箱」，然後選取「工作」。 您可以在此檢視匯入檔案的所有詳細資訊。 選取狀態為失敗的檔案，然後選取檢視工作詳細資訊。 強制回應視窗隨即顯示。 選取「檢視JSON檔案」 ，然後向下捲動並複製「訊息」下顯示的錯誤訊息。 可能會出現多個錯誤訊息，因此請務必複製所有訊息。 嘗試記錄Bug票證時，將這些訊息傳送給您的Adobe團隊。 這會加快解決流程，並為您的團隊提供更多有關問題的情境。
