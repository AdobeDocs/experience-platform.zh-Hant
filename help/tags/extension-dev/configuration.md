---
title: 擴充功能組態
description: 了解如何設定標籤擴充功能，以從Adobe Experience Platform資料收集UI中的使用者收集全域設定。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 59%

---

# 擴充功能組態

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../term-updates.md)。

擴充功能組態是擴充功能據以向使用者收集全域設定的方式。例如，假設擴充功能允許使用者使用「傳送信標」動作來傳送信標，且信標一律須包含帳戶 ID。我們不想勞煩使用者在每次設定「傳送信標」動作時都須提供帳戶 ID。因此，擴充功能只會從擴充功能組態檢視中要求一次帳戶 ID。每當要傳送信標時，「傳送信標」動作程式庫模組都可從擴充功能組態中提取帳戶 ID，並將其新增至信標。

當使用者將擴充功能安裝至Adobe Experience Platform中的標籤屬性時，將會顯示您的擴充功能將提供的擴充功能組態檢視。 使用者若未完成擴充功能組態，就無法完成擴充功能的安裝。請參閱[檢視](./web/views.md)的相關文件，了解如何建立擴充功能組態的檢視。

從擴充功能組態檢視儲存設定後，這些設定就會在標籤執行階段程式庫中發出。 然後，您可以呼叫 [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings)，從擴充功能程式庫模組存取這些設定。

擴充功能組態是選用功能，您可以選擇不使用。
