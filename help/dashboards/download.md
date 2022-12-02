---
solution: Experience Platform
title: 下載Experience Platform控制面板以PDF
type: Documentation
description: 使用Experience PlatformUI中提供的「下載至PDF」功能，儲存控制面板視覺效果的副本。
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
source-git-commit: 5d9428c4323e65c2605fd116160e160af7d9086d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# 下載控制面板以PDF

Adobe Experience Platform中的控制面板可從Platform使用者介面下載至PDF，以方便與組織成員共用資訊。

本檔案提供如何使用Platform UI下載控制面板，以及使用預設瀏覽器列印功能表儲存控制面板以進行PDF的摘要。

>[!WARNING]
>
>控制面板中包含的資料可能包含客戶的個人識別資訊(PII)，或與組織相關的敏感資料。 儲存至PDF的任何控制面板資料，都應根據貴組織的資料隱私權准則加以適當處理。

## 下載控制面板

若要開始下載控制面板，請導覽至您要下載的控制面板(例如 [!UICONTROL 設定檔] 控制面板)，然後選取「更多選項」功能表(**`...`**)。 下一步，選擇 **[!UICONTROL 下載]**.

![Experience Platform描述檔控制面板，反白顯示省略號和下載下拉式清單。](images/download/download-button.png)

## 預覽PDF

選取後 **[!UICONTROL 下載]**，則會開啟瀏覽器的預設列印功能表。 在此範例中，會顯示Google Chrome列印功能表。

列印功能表可讓您預覽要儲存的PDF。 PDF是Platform UI中顯示之控制面板小工具的真實表示，且PDF的大小會自動調整，以顯示單一頁面上所有目前可見的控制面板小工具。

![「配置檔案」概述以單頁格式顯示，右側是「打印選項」面板。](images/download/download-chrome-print.png)

PDF包含自動產生的標題，其中包含Experience Platform標誌、控制面板的名稱、您的名稱，以及控制面板下載的日期和時間。 此資訊為唯讀，無法在PDF中編輯。

![打印預覽的特寫，自動生成的標題突出顯示。](images/download/download-pdf.png)

## 另存為PDF

預覽PDF後，選取 **儲存** ，選擇要保存PDF的位置。

>[!NOTE]
>
>如有必要，您可以使用 **目的地** 下拉式清單選取 **另存為PDF** 如果未自動為您選取該選項。

![單頁格式顯示配置檔案概覽，其中「目標」下拉式清單「另存為PDF」打印選項突出顯示。](images/download/download-chrome-print-destination.png)

## 自訂控制面板PDF

產生的PDF會符合您在UI中看到的控制面板，並僅包含目前顯示在控制面板上的小工具。 某些控制面板可以自定義，以更改小部件的大小和位置，或添加小部件並從視圖中刪除小部件。 在Platform UI中自訂控制面板的外觀，也會變更產生的PDF外觀。

例如，您可以修改設定檔控制面板的外觀，以包含多個堆疊在三個標準介面工具集上的全寬介面工具集。

![展示細長構件的「配置檔案」儀表板。](images/download/download-modify.png)

選取以下載更新的控制面板，會產生符合自訂設定檔控制面板外觀的新PDF預覽。 它也會自動調整PDF的大小，以確保所有可見介面工具集都包含在單頁PDF中。

![「配置檔案」概述以單頁格式顯示，右側是「打印選項」面板。](images/download/download-chrome-print-modified.png)

若要進一步了解自訂控制面板，請先閱讀 [控制面板自訂概觀](customize/overview.md).

## 後續步驟

現在您已下載控制面板並儲存為PDF，您可以重複這些步驟來下載其他控制面板，或與組織成員共用PDF。
