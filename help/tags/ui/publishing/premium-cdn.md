---
title: Experience Platform 標籤 (中國)
description: 瞭解用於標籤的Experience Platform標籤（中國）功能，以及如何將其用於在多個地理區域傳遞您的內容。
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 9c39fd5d0353cc171230818d79ac213ce200dc1e
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 1%

---

# Experience Platform 標籤 (中國)

當您使用 [Adobe管理主機](./hosts/managed-by-adobe-host.md) 為了在您的網站上傳遞Adobe Experience Platform標籤資產，這些資產會分散到全球各地的各種內容傳遞網路(CDN)中，以提供最快的下載速度。 不過，有些地區會要求將所有網站資產複製並託管於該地區的伺服器。

為了說明此問題，Experience Platform中的標籤提供Experience Platform標籤（中國）功能，可讓您傳送內容給這些特殊區域。

Experience Platform標籤（中國）支援是一項付費功能，貴組織必須購買該功能才能啟用及使用。 本指南說明購買此功能後，如何在Experience Platform UI或資料收集UI中設定和使用。

## 為您的組織啟用Experience Platform標籤（中國）

Experience Platform標籤（中國）在公司層級啟用。 您的組織購買Experience Platform標籤（中國）功能後，Adobe管理員將在您公司的UI中啟用該功能。

## 使用更新的內嵌程式碼重新建置並安裝標籤程式庫

啟用Experience Platform標籤（中國）後，並不表示您的標籤資產會立即複製並準備在新的地區使用。 這僅表示您現在可以選擇何時加入此功能。

>[!IMPORTANT]
>
>在中國啟用標籤之前建立的程式庫仍會照常運作，就像現在一樣。 這也適用於未由Adobe管理的程式庫，因為 [封存的環境](./environments.md#archive) 僅將相對URL用於其資產路徑。 請注意，啟用「Experience Platform標籤（中國）」後，您建置且非Adobe管理的任何程式庫，其行為就像未啟用中國標籤功能一樣。

一旦您在中國啟用了標籤，並重新建置任何您想要從新託管區域使用的程式庫，您就可以擷取新的託管區域內嵌程式碼，以新增至您的網站。

>[!NOTE]
>
>列於「 」下方的程式庫內嵌程式碼 [!UICONTROL 標準] 託管區域可繼續正常運作，網站上的任何Page Top或Page Bottom內嵌程式碼亦可正常運作。

造訪 **[!UICONTROL 環境]** 從「程式庫編輯」畫面頁面或檢視環境安裝指示，以尋找新的內嵌程式碼。 每個新支援的託管區域都會顯示在 [!UICONTROL 標準] 託管區域(用於世界上沒有Experience Platform標籤支援的區域（中國）)。 以下熒幕擷圖顯示中國地區的內嵌程式碼，該程式碼使用 `.cn` 作為其頂層網域(TLD)。

![中國地區的內嵌程式碼](../../images/ui/publishing/premium-cdn/embed-codes.png)

為網頁選擇適當的內嵌程式碼，並將其貼到 `<head>` 標籤之前。 如需使用內嵌程式碼安裝標籤程式庫的詳細資訊，請參閱 [環境UI指南](./environments.md#installation).

## 後續步驟

本指南說明如何為標籤實作啟用和安裝Experience Platform標籤（中國）功能。 如需在Web和行動屬性上安裝及測試標籤程式庫的詳細資訊，請參閱 [發佈概觀](./overview.md).
