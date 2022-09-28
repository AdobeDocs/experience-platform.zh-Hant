---
title: 適用於標籤的Premium CDN支援
description: 了解標籤的付費CDN功能，以及如何在多個地理區域傳送內容。
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 適用於標籤的Premium CDN支援（測試版）

>[!IMPORTANT]
>
>標籤的進階CDN功能目前仍在測試階段，而您的組織可能尚無法存取。 本檔案可能會有所變更。

若您使用 [Adobe管理主機](./hosts/managed-by-adobe-host.md) 為了在您的網站上傳送Adobe Experience Platform標籤資產，這些資產會分散在全球各地的各種內容傳遞網路(CDN)中，以提供最快的下載速度。 不過，某些地區會要求複製所有網站資產，並在該地區的伺服器上托管。

為此，Experience Platform中的標籤提供付費的CDN功能，可讓您將內容傳送至這些特殊地區。

Premium CDN支援是付費功能，您的組織必須購買才能啟用和使用。 本指南涵蓋購買後如何在Experience PlatformUI或資料收集UI中設定和使用此功能。

## 為貴組織啟用優質CDN

Premium CDN會在公司層級啟用。 貴組織購買進階CDN功能後，Adobe管理員就會在貴公司的UI中啟用該功能。

## 使用更新的內嵌程式碼重建和安裝標籤程式庫

Premium CDN一經啟用，並不表示您的標籤資產會立即複製，並準備在新地區內使用。 這隻表示您現在可以選擇何時加入此功能。

>[!IMPORTANT]
>
>在啟用進階CDN之前建置的程式庫，將可繼續如現運作。 這也適用於非由Adobe管理的程式庫，因為 [封存環境](./environments.md#archive) 僅對其資產路徑使用相對URL。 請注意，在您啟用Premium CDN後，任何您建置且未由Adobe管理的程式庫，都會以未啟用Premium CDN功能的方式運作。

啟用進階CDN並重新建置任何您想從新托管區域使用的程式庫後，您就可以擷取新托管區域的內嵌程式碼，以新增至您的網站。

>[!NOTE]
>
>列於 [!UICONTROL 標準] 托管區域將可繼續原樣運作，以及網站上已有的任何Page Top或Page Bottom內嵌程式碼。

造訪 **[!UICONTROL 環境]** 頁面或從「程式庫編輯」畫面檢視環境安裝指示，以尋找新的內嵌程式碼。 每個新支援的托管區域會顯示在 [!UICONTROL 標準] 托管區域（用於全球不提供進階CDN支援的區域）。 下面的螢幕擷圖顯示中國地區的內嵌程式碼，該區域使用 `.cn` 作為其頂層網域(TLD)。

![中國地區的內嵌程式碼](../../images/ui/publishing/premium-cdn/embed-codes.png)

選擇適當的網頁內嵌程式碼，並貼到 `<head>` 標籤。 如需使用內嵌程式碼來安裝標籤程式庫的詳細資訊，請參閱 [environments UI指南](./environments.md#installation).

## 後續步驟

本指南說明如何啟用和安裝您標籤實作的進階CDN功能。 如需在Web和行動屬性上安裝和測試標籤程式庫的詳細資訊，請參閱 [發佈概述](./overview.md).
