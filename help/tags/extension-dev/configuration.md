---
title: 擴充功能組態
description: 瞭解如何配置標籤擴展以從Adobe Experience PlatformUI或資料收集UI中的用戶收集全局設定。
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 68%

---

# 擴充功能組態

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../term-updates.md)。

擴充功能組態是擴充功能據以向使用者收集全域設定的方式。例如，假設擴充功能允許使用者使用「傳送信標」動作來傳送信標，且信標一律須包含帳戶 ID。我們不想勞煩使用者在每次設定「傳送信標」動作時都須提供帳戶 ID。因此，擴充功能只會從擴充功能組態檢視中要求一次帳戶 ID。每當要傳送信標時，「傳送信標」動作程式庫模組都可從擴充功能組態中提取帳戶 ID，並將其新增至信標。

當用戶在Adobe Experience Platform安裝標籤屬性的擴展時，他們將顯示您的擴展提供的擴展配置視圖。 使用者若未完成擴充功能組態，就無法完成擴充功能的安裝。請參閱[檢視](./web/views.md)的相關文件，了解如何建立擴充功能組態的檢視。

從擴展配置視圖保存設定後，這些設定將在標籤運行時庫中發出。 然後，您可以呼叫 [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings)，從擴充功能程式庫模組存取這些設定。

擴充功能組態是選用功能，您可以選擇不使用。
