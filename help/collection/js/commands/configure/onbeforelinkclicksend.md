---
title: onBeforeLinkClickSend
description: 在傳送連結追蹤資料之前執行的回呼。
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>已棄用此回呼。 請改用[`clickCollection.filterClickDetails`](clickcollection.md)。

`onBeforeLinkClickSend`回呼可讓您註冊JavaScript函式，該函式可變更您在將資料傳送至Adobe之前所傳送的連結追蹤資料。 它可讓您操作`xdm`或`data`物件，包括新增、編輯或移除元素的功能。 您也可以有條件地完全取消傳送資料，例如使用偵測到的使用者端機器人流量。

此回呼只有在已啟用[`clickCollectionEnabled`](clickcollectionenabled.md)且`filterClickDetails`不包含已登入函式時才執行。

如果[`onBeforeEventSend`](onbeforeeventsend.md)和`onBeforeLinkClickSend`都包含已登入的功能，則會先執行`onBeforeLinkClickSend`。

>[!WARNING]
>
>此回呼允許使用自訂程式碼。 如果您包含在回呼中的任何程式碼擲回未攔截到的例外狀況，處理事件時就會中止。 資料不會傳送至Adobe。

## `onBeforeLinkClickSend` 和 `filterClickDetails`

[`clickCollection.filterClickDetails`](clickcollection.md)回呼設計用來取代`onBeforeLinkClickSend`。 Adobe強烈建議不要同時指派回呼函式給兩者。 如果您將回呼函式同時指派給`filterClickDetails`和`onBeforeLinkClickSend`，程式庫會使用以下邏輯：

* 只有`filterClickDetails`執行；`onBeforeLinkClickSend`不執行。
* 事件群組`clickCollection.eventGroupingEnabled`無法運作。
