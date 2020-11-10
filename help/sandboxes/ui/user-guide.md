---
keywords: Experience Platform;home;popular topics;sandbox user guide;sandbox guide
solution: Experience Platform
title: 沙盒使用指南
topic: user guide
description: 本檔案提供如何在Adobe Experience Platform使用者介面中執行與沙盒相關之各種作業的步驟。
translation-type: tm+mt
source-git-commit: 2d1a9699866bd39de7251731e9f0cd2f753a5083
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---


# 沙盒使用指南

本檔案提供如何在Adobe Experience Platform使用者介面中執行與沙盒相關之各種作業的步驟。

## 檢視沙盒

在Experience Platform UI中，選取左側導 **[!UICONTROL 覽中的]** 「沙盒」以開啟「 **[!UICONTROL 沙盒]** 」控制面板。 控制面板會列出您組織的所有可用沙盒，包括沙盒類型（生產或開發）和狀態（作用中、建立、刪除或失敗）。

![](../images/ui/view-sandboxes.png)

## 在沙盒之間切換

畫面 **左上角的沙盒切換器** ，會顯示目前作用中的沙盒。

![](../images/ui/sandbox-switcher.png)

若要在沙盒之間切換，請選取沙盒切換器，並從下拉式清單中選取所要的沙盒。

![](../images/ui/switcher-menu.png)

選取沙盒後，畫面會重新整理，而沙盒切換器現在包含選取的沙盒。

![](../images/ui/switched.png)

## 沙盒作業

您可以使用沙盒切換器選單中的搜尋功能，在可用沙盒的清單中導覽。 輸入您要存取的沙盒名稱，以篩選組織可用的所有沙盒。

![](../images/ui/sandbox-search.png)

## 建立新的沙盒

使用下列影片快速概述如何在Experience Platform中使用沙盒。

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

若要在UI中建立新沙盒，請選取畫面右上 **[!UICONTROL 方的「建立沙盒]** 」按鈕。

![](../images/ui/create-sandbox.png)

此時會 **[!UICONTROL 出現「建立沙盒]** 」對話方塊，提示您提供沙盒的顯示標題和名稱。 顯 **示標題** (Display Title)應為人類可讀，且應具備足夠的描述性，以方便識別。 沙盒名 **[!UICONTROL 稱]** (Sandbox Name)是全小寫的識別碼，可用於API呼叫，因此應是唯一且簡明的。 沙盒名 **[!UICONTROL 稱]** (Sandbox Name **)只能由英數字元和連字型大小(-)組成**，它必須以字母開頭，且最多包含256個字元。

完成後，選擇「 **[!UICONTROL 建立」]**。

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>由於您僅限於建立非生產沙盒類型， **[!UICONTROL type]** （類型）選項會鎖定在「非生產」，因此無法加以控制。

建立完沙盒後，請重新整理頁面，新沙盒就會出現在 **[!UICONTROL Sandboxs]** （沙盒）控制面板中，狀態為「[!UICONTROL Creating]」。 新沙盒需要約15分鐘的時間才能由系統布建，之後其狀態會變更為「[!UICONTROL Active]」。

![](../images/ui/creating.png)

## 重設沙盒

>[!NOTE]
>
>此功能僅適用於非生產沙盒。 無法重設生產沙盒。

重設非生產沙盒會刪除與該沙盒（結構、資料集等）相關的所有資源，同時仍會保留沙盒的名稱和相關權限。 對於具有存取權的使用者，這個「乾淨」的沙盒仍以相同名稱提供。

若要在UI中重設沙盒，請在左導覽中選取「 **[!UICONTROL 沙盒」]** ，然後選取您要重設的沙盒。 在顯示在畫面右側的對話方塊中，選取「重設沙 **[!UICONTROL 盒」]**。

![](../images/ui/reset-sandbox.png)

出現對話方塊提示您確認選擇。 選擇 **[!UICONTROL 重置]** ，繼續。

![](../images/ui/reset-confirm.png)

出現確認訊息，沙盒的狀態會變更為「重&#x200B;**[!UICONTROL 設]」**。 在系統布建它後，其狀態將更新為「活 **動」** 或「失敗 **」**。

![](../images/ui/resetting.png)

## 刪除沙盒

>[!NOTE]
>
>此功能僅適用於非生產沙盒。 無法刪除生產沙盒。

刪除非生產沙盒會永久移除與該沙盒相關的所有資源，包括權限。

若要刪除UI中的沙盒，請在左導覽中選取「 **[!UICONTROL 沙盒」]** ，然後選取您要刪除的沙盒。 在顯示在畫面右側的對話方塊中，選取「刪除沙盒」( **[!UICONTROL Delete Sandbox)]**。

![](../images/ui/delete-sandbox.png)

出現對話方塊提示您確認選擇。 選擇 **[!UICONTROL 刪除]** ，繼續。

![](../images/ui/delete-confirm.png)

隨即出現確認訊息，沙盒會從「沙盒」工作區 **[!UICONTROL 移除]** 。

## 後續步驟

本檔案示範如何在Experience Platform UI中管理沙盒。 如需如何使用沙盒API管理沙盒的詳細資訊，請參閱沙盒開 [發人員指南](../api/getting-started.md)。