---
keywords: Experience Platform；首頁；熱門主題；資料登陸區；資料登陸區
solution: Experience Platform
title: 使用UI將資料登錄區域連線至平台
topic-legacy: overview
type: Tutorial
description: 了解如何使用Platform使用者介面建立資料著陸區來源連接器。
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: ca7197036283ee15dbf60c113d361a5ea34d65c1
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 使用UI將[!DNL Data Landing Zone]連線至Platform

[!DNL Data Landing Zone] 是雲端資料儲存設施，適用於布建有Adobe Experience Platform的暫存檔案儲存。[!DNL Data Landing Zone] 僅用於資料進出Platform的入口和出口。7天後，資料會從[!DNL Data Landing Zone]中自動刪除。

本教學課程提供使用Platform使用者介面建立[!DNL Data Landing Zone]來源連線的步驟。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

## 將檔案從[!DNL Data Landing Zone]帶入Platform

在平台UI中，從左側導覽中選取&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL 目錄]畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列找到您要使用的特定來源。

在[!UICONTROL 雲儲存]類別下，選擇[!DNL Data Landing Zone]，然後選擇&#x200B;**[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/dlz/catalog.png)

此時會出現[!UICONTROL 新增資料]步驟，提供您選取並預覽您要帶入Platform的資料的介面。

![新增資料](../../../../images/tutorials/create/dlz/add-data.png)

有關如何為雲儲存源建立資料流的詳細逐步指南，請參閱有關建立雲儲存資料流以將資料帶到Platform](../../dataflow/batch/cloud-storage.md)的教程。[

## 檢索並刷新[!DNL Data Landing Zone]憑據

[!DNL Data Landing Zone] 是隨Adobe Experience Platform來源授權提供的現成可用來源。[!DNL Data Landing Zone] 使用基於SAS URI和SAS令牌的身份驗證。您可以從[!UICONTROL 源目錄]頁中檢索和刷新身份驗證憑據。

在[!UICONTROL 源目錄]的[!UICONTROL 雲儲存]類別下，選擇點(**...**)。 ****&#x200B;從出現的下拉菜單中，選擇&#x200B;**[!UICONTROL 查看憑據]**。

![選項](../../../../images/tutorials/create/dlz/options.png)

此時將出現彈出窗口，顯示您的容器名稱、SAS令牌、儲存帳戶名稱和SAS URI。

選擇&#x200B;**[!UICONTROL 刷新憑據]**&#x200B;並允許處理更新的憑據幾秒鐘。

![view-credentials](../../../../images/tutorials/create/dlz/credentials.png)

## 後續步驟

依照本教學課程，您已存取[!DNL Data Landing Zone]容器，並學習如何擷取和重新整理憑證。 您現在可以繼續進行下一個關於[建立資料流的教程，以將資料從雲儲存帶到Platform](../../dataflow/batch/cloud-storage.md)。
