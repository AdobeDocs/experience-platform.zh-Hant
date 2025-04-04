---
solution: Experience Platform
title: 將Experience Platform儀表板下載至PDF
type: Documentation
description: 使用Experience Platform UI中提供的下載至PDF功能來儲存控制面板視覺效果的副本。
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---

# 將儀表板下載至PDF

Adobe Experience Platform中的儀表板可以從PDF使用者介面下載到Experience Platform，以促進與組織成員共用資訊。

本檔案摘要說明如何使用Experience Platform UI下載控制面板，以及使用預設瀏覽器列印選單將控制面板儲存至PDF。

>[!WARNING]
>
>儀表板中包含的資料可能包括關於您客戶的個人識別資訊(PII)，或與您的組織相關的敏感資料。 任何儲存至PDF的儀表板資料，都應根據貴組織的資料隱私權指引進行適當處理。

## 下載儀表板

若要開始下載儀表板，請導覽至您要下載的儀表板（例如[!UICONTROL 設定檔]儀表板），然後從儀表板的右上角選取更多選項功能表(**`...`**)。 接著，選取&#x200B;**[!UICONTROL 下載]**。

![反白顯示省略符號和下載下拉式清單的Experience Platform設定檔儀表板。](images/download/download-button.png)

## 預覽PDF

選取&#x200B;**[!UICONTROL 下載]**&#x200B;後，瀏覽器的預設列印功能表會開啟。 此範例中顯示Google Chrome列印功能表。

列印功能表可讓您預覽將儲存的PDF。 PDF能真實呈現儀表板Widget在Experience Platform UI中的顯示方式，而PDF的大小會自動調整，以便在單一頁面上顯示所有目前可見的儀表板Widget。

![設定檔概述會以單頁格式顯示，列印選項面板在右側。](images/download/download-chrome-print.png)

PDF包含自動產生的標頭，其中包含Experience Platform標誌、控制面板的名稱、您的名稱，以及下載控制面板的日期和時間。 此資訊是唯讀的，無法在PDF中編輯。

![反白顯示自動產生標題的列印預覽特寫。](images/download/download-pdf.png)

## 另存為PDF

預覽PDF後，選取「**儲存**」以選擇要將PDF儲存到的位置。

>[!NOTE]
>
>如有必要，您可以使用&#x200B;**目的地**&#x200B;下拉式清單來選取&#x200B;**儲存為PDF** （如果未自動為您選取該選項）。

![設定檔概述會以單頁格式顯示，且「目的地」下拉式功能表的「另存為PDF」列印選項會強調顯示。](images/download/download-chrome-print-destination.png)

## 自訂儀表板PDF

產生的PDF會符合您在UI中看到的儀表板，且僅包含目前顯示在儀表板上的Widget。 您可以自訂某些儀表板，以變更Widget的大小和位置，或從檢視中新增和移除Widget。 在Experience Platform UI中自訂控制面板的外觀也會變更所產生PDF的外觀。

例如，您可以修改設定檔控制面板的外觀，將數個全寬Widget棧疊在三個標準Widget上方。

![展示延伸介面工具集的設定檔儀表板。](images/download/download-modify.png)

選取以下載更新的儀表板會導致新的PDF預覽，符合自訂設定檔儀表板的外觀。 它也會自動調整PDF的大小，確保所有可見的Widget都包含在單頁PDF中。

![設定檔概述會以單頁格式顯示，列印選項面板在右側。](images/download/download-chrome-print-modified.png)

若要深入瞭解自訂儀表板，請先閱讀[儀表板自訂概觀](customize/overview.md)。

## 後續步驟

現在您已下載儀表板並將其儲存為PDF，您可以重複這些步驟以下載其他儀表板或與組織成員共用PDF。
