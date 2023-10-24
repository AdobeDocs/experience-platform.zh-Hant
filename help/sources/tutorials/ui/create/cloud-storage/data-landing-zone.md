---
keywords: Experience Platform；首頁；熱門主題；資料登陸區域；資料登陸區域
title: 使用UI將資料登陸區域連線至Platform
description: 瞭解如何使用Platform使用者介面建立資料登陸區域來源聯結器。
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: 9cffd508c1bff7ce133f84ca686c414e997343b8
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# 連線 [!DNL Data Landing Zone] 使用UI移至Platform

>[!IMPORTANT]
>
>此頁面是特定的 [!DNL Data Landing Zone] *來源* Experience Platform中的聯結器。 如需有關連線至 [!DNL Data Landing Zone] *目的地* 聯結器，請參閱 [[!DNL Data Landing Zone] 目的地檔案頁面](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] 是安全的雲端檔案儲存設施，可將檔案匯入Adobe Experience Platform。 資料會自動從 [!DNL Data Landing Zone] 七天之後。

本教學課程提供建立 [!DNL Data Landing Zone] 來源連線使用Platform使用者介面。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 從以下位置帶入您的檔案 [!DNL Data Landing Zone] 至平台

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示各種來源，供您建立帳戶。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋列來尋找您要使用的特定來源。

在 [!UICONTROL 雲端儲存空間] 類別，選取 [!DNL Data Landing Zone] 然後選取 **[!UICONTROL 新增資料]**.

![已選取資料登陸區域的來源目錄。](../../../../images/tutorials/create/dlz/catalog.png)

此 [!UICONTROL 新增資料] 步驟隨即顯示，為您提供介面，讓您選取並預覽要帶入Platform的資料。

* 介面的左側是資料夾瀏覽器，為您提供來自容器的檔案清單，您可以將這些檔案帶到Platform。
* 介面的右側部分可讓您預覽相容檔案中最多100列的資料。

選取您要帶入Experience Platform的檔案，並等待片刻，讓正確的介面更新到預覽畫面中。

![來源工作區的新增資料介面。](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform會自動偵測您選取之檔案的屬性資訊，包括檔案資料格式、指定的欄分隔符號和壓縮型別的資訊。

預覽介面可讓您檢查檔案的內容和結構。 依預設，預覽介面會顯示所選資料夾中的第一個檔案。

若要預覽其他檔案，請選取要檢查的檔案名稱旁的預覽圖示。

完成後，選取 **[!UICONTROL 下一個]**.

![來源工作區的資料預覽頁面。](../../../../images/tutorials/create/dlz/file-detection.png)

如需如何為雲端儲存空間來源建立資料流的詳細逐步指南，請參閱以下教學課程： [建立雲端儲存空間資料流以將資料帶到Platform](../../dataflow/batch/cloud-storage.md).

## 擷取並重新整理 [!DNL Data Landing Zone] 認證

[!DNL Data Landing Zone] 是隨Adobe Experience Platform來源授權提供的現成可用來源。 [!DNL Data Landing Zone] 使用SAS URI和SAS權杖型驗證。 您可以從以下位置擷取和重新整理您的驗證認證： [!UICONTROL 來源目錄] 頁面。

在 [!UICONTROL 來源目錄]，位於 [!UICONTROL 雲端儲存空間] 類別，選取省略符號(**...**)從 **[!UICONTROL 資料登陸區域]** 卡片。 從出現的下拉式功能表中，選取 **[!UICONTROL 檢視認證]**.

![資料登陸區域的檢視選項清單。](../../../../images/tutorials/create/dlz/options.png)

此時畫面會顯示彈出視窗，其中顯示您的容器名稱、SAS權杖、儲存體帳戶名稱、SAS URI以及到期日。

選取 **[!UICONTROL 重新整理認證]** 並留出數秒時間，以便處理您更新的認證。

>[!TIP]
>
>您的 [!DNL Data Landing Zone] 認證已設定為90天後自動過期，您必須使用新認證以重新連線 [!DNL Data Landing Zone] 過期之後。 您的Platform資料流不會受到即將到期的認證的影響，而且您仍然可以使用新認證繼續使用新的和現有的資料流。

![與指定資料登陸區域帳戶相關聯的認證。](../../../../images/tutorials/create/dlz/view-credentials.png)

## 後續步驟

依照本教學課程，您已存取 [!DNL Data Landing Zone] 容器，並已瞭解如何擷取和重新整理您的認證。 您現在可以繼續下一個教學課程，於 [建立資料流，將資料從雲端儲存空間帶到Platform](../../dataflow/batch/cloud-storage.md).
