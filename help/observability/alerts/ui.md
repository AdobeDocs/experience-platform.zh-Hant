---
keywords: Experience Platform；首頁；熱門主題；日期範圍
title: 警報UI指南
description: 瞭解如何在Experience Platform使用者介面中管理警報。
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: 8d63e9fa4c7eb09ffb90edca612a6e6d44dd18fa
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# 警報UI指南

Adobe Experience Platform使用者介面可讓您根據Adobe Experience Platform可觀察性深入解析顯示的量度，檢視已接收警報的歷史記錄。 UI也可讓您檢視、啟用、停用及訂閱可用的警報規則。

>[!NOTE]
>
>如需Experience Platform中警示的簡介，請參閱 [警報概觀](./overview.md).

若要開始使用，請選取 **[!UICONTROL 警報]** ，位於左側導覽器中。

![警示頁面醒目提示 [!UICONTROL 警報] ，位於左側導覽器中。](../images/alerts/ui/workspace.png)

## 管理警示規則

此 **[!UICONTROL 瀏覽]** 索引標籤會列出可觸發警示的可用規則。

![可用的警報清單會顯示在 [!UICONTROL 瀏覽] 標籤。](../images/alerts/ui/rules.png)

從清單中選取規則，即可在右側邊欄中檢視其說明和設定引數，包括臨界值和嚴重度。

![右側邊欄中醒目提示的警報規則會顯示詳細資訊。](../images/alerts/ui/rule-details.png)

選取省略符號(**...**)，下拉式清單則會顯示啟用或停用警報（視其目前狀態而定），以及訂閱或取消訂閱警報電子郵件通知的控制項。

![選取的橢圓會顯示下拉式功能表。](../images/alerts/ui/disable-subscribe.png)

## 管理警報訂閱者

>[!NOTE]
>
> 若要將警報指派給Adobe使用者ID、外部電子郵件地址或電子郵件群組清單，您必須是管理員。

此 **[!UICONTROL 瀏覽]** 索引標籤會列出可觸發警示的可用規則。

![顯示的可用警示規則清單 [!UICONTROL 瀏覽] 標籤。](../images/alerts/ui/rules.png)

選取省略符號(**...**)規則名稱旁會出現下拉式清單，顯示控制項。 選取 **[!UICONTROL 管理警報訂閱者]**.

![選取橢圓以顯示下拉式功能表。 此 [!UICONTROL 管理警報訂閱者] 選項會反白顯示。](../images/alerts/ui/manage-alert-subscribers.png)

此 [!UICONTROL 管理警報訂閱者] 頁面便會顯示。 若要將通知指派給特定使用者，請輸入其Adobe使用者ID、外部電子郵件地址或電子郵件群組清單，然後按Enter鍵。

>[!NOTE]
>
>若要一次將本通知傳送給數位使用者，請提供使用者ID的清單或以逗號分隔的電子郵件地址。

![管理警示訂閱者頁面會顯示輸入的電子郵件地址。](../images/alerts/ui/manage-alert-add-email.png)

電子郵件地址會顯示在目前列出的訂閱者清單中。 選取「**[!UICONTROL 更新]**」。

![管理警示訂閱者頁面會醒目顯示訂閱者與 [!UICONTROL 更新].](../images/alerts/ui/manage-alert-subscribers-added-email.png)

您已成功新增使用者至您的警報通知清單。 提交的使用者現在將收到此警報的電子郵件通知，如下圖所示。

![所收到警示通知的電子郵件範例。](../images/alerts/ui/manage-alert-subscribers-email.png)

## 啟用電子郵件警示

警示通知可以直接傳送到您的電子郵件。

選取鈴鐺圖示(![鈴鐺圖示](../images/alerts/ui/bell-icon.png))，位於右上角功能區，顯示通知和公告。 在出現的下拉式清單中，選取齒輪圖示(![齒輪圖示](../images/alerts/ui/cog-icon.png))以存取Experience Cloud偏好設定頁面。

![醒目提示鈴鐺圖示和齒輪圖示的警報清單。](../images/alerts/ui/edit-preferences.png)

此 **個人資料** 頁面隨即顯示。 選取 **[!UICONTROL 通知]** 以存取電子郵件警示偏好設定。

![設定檔頁面醒目提示 [!UICONTROL 通知] ，位於左側導覽器中。](../images/alerts/ui/profile.png)

捲動至 **電子郵件** 區段並選取 **[!UICONTROL 即時通知]**

![電子郵件區段在設定檔頁面中反白顯示。](../images/alerts/ui/notifications.png)

您訂閱的任何警報現在都會傳送到連線至您Adobe ID帳戶的電子郵件地址。

## 檢視警示歷史記錄

此 **[!UICONTROL 歷史記錄]** 索引標籤顯示貴組織收到警示的歷史記錄，包括觸發警示、觸發日期和解決日期（如果適用）的規則。

![收到的警示清單會顯示在 [!UICONTROL 歷史記錄] 標籤。](../images/alerts/ui/history.png)

選取列出的警報，右側邊欄中會顯示更多詳細資料，包括觸發警報之事件的簡短摘要。

![在右側邊欄中顯示詳細資訊的醒目提示警報。](../images/alerts/ui/history-details.png)

## 後續步驟

本文概述如何在Platform UI中檢視及管理警報。 請參閱以下主題的概觀： [可觀察性深入分析](../home.md) 以取得有關服務功能的詳細資訊。
