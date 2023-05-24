---
solution: Experience Platform
title: 將Experience Platform儀表板下載到PDF
type: Documentation
description: 使用Experience PlatformUI中提供的下載到PDF功能保存儀表板可視化效果的副本。
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
source-git-commit: 5d9428c4323e65c2605fd116160e160af7d9086d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# 將儀表板下載到PDF

Adobe Experience Platform內的儀表板可以從平台用戶介面下載到PDF中，以便與貴組織成員共用資訊。

本文檔提供了如何使用平台UI下載儀表板以及使用預設瀏覽器打印菜單將儀表板保存到PDF的摘要。

>[!WARNING]
>
>儀表板中包含的資料可能包含有關客戶的個人身份資訊(PII)或與您的組織相關的敏感資料。 保存到PDF的任何儀表板資料都應根據您組織的資料隱私准則進行適當處理。

## 下載儀表板

要開始下載儀表板，請導航到要下載的儀表板(例如， [!UICONTROL 配置檔案] )，然後選擇「更多選項」菜單(**`...`**)。 下一步，選擇 **[!UICONTROL 下載]**。

![突出顯示了「Experience Platform配置式」儀表板，其中省略號和「下載」下拉清單。](images/download/download-button.png)

## 預覽PDF

選擇後 **[!UICONTROL 下載]**，瀏覽器的預設打印菜單開啟。 在此示例中，顯示了GoogleChrome打印菜單。

打印菜單允許您預覽要保存的PDF。 PDF是儀表板小部件在平台UI中顯示時的真實表示形式，並且PDF的大小將自動調整以在單個頁面上顯示所有當前可見的儀表板小部件。

![單頁格式上顯示的「配置式」概述，右側是「打印選項」面板。](images/download/download-chrome-print.png)

PDF包括自動生成的標題，其中包含Experience Platform徽標、儀表板名稱、您的名稱以及下載儀表板的日期和時間。 此資訊是只讀的，無法在PDF中編輯。

![自動生成的標題突出顯示的打印預覽的特寫。](images/download/download-pdf.png)

## 另存為PDF

預覽PDF後，選擇 **保存** 選擇要保存PDF的位置。

>[!NOTE]
>
>如有必要，可使用 **目標** 下拉清單選擇 **另存為PDF** 選項。

![單頁格式上顯示的「配置式」概述，「目標」下拉清單「另存為PDF」打印選項突出顯示。](images/download/download-chrome-print-destination.png)

## 自定義儀表板PDF

生成的PDF與您在UI中可以看到的儀表板匹配，並且只包括儀表板上當前可見的小部件。 可以自定義某些儀表板以更改小部件的大小和位置，或從視圖中添加和刪除小部件。 在平台UI中自定義儀表板的外觀還會更改生成的PDF的外觀。

例如，您可以修改配置檔案操控板的外觀，以包括堆疊在三個標準小部件之上的多個全寬小部件。

![演示細長構件顯示的「配置檔案」儀表板。](images/download/download-modify.png)

選擇以下載更新的儀表板會生成與自定義的配置檔案儀表板的外觀相匹配的新PDF預覽。 它還自動調整PDF的大小，以確保所有可見小部件都包含在一頁PDF中。

![單頁格式上顯示的「配置式」概述，右側是「打印選項」面板。](images/download/download-chrome-print-modified.png)

要瞭解有關自定義儀表板的詳細資訊，請首先閱讀 [儀表板自定義概述](customize/overview.md)。

## 後續步驟

現在，您已下載儀表板並將其保存為PDF，您可以重複這些步驟以下載其他儀表板或與組織成員共用PDF。
