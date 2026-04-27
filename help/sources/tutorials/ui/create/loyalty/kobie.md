---
title: 使用UI將資料從Kobie串流到Experience Platform
description: 瞭解如何使用UI將資料從Kobie串流到Adobe Experience Platform。
hide: true
hidefromtoc: true
exl-id: 4e2e3287-3673-4426-8666-5f2ee284ca3d
source-git-commit: 79527635a61a43e2995f08d8c5981cd2030c5840
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 1%

---

# 使用UI將資料從[!DNL Kobie Streaming Events]串流到Experience Platform

[!DNL Kobie Alchemy Loyalty Cloud (KALC)]是高度可設定、安全且可擴充的MACH平台，可因應您的忠誠度策略，加速實現價值、提高效率，並透過企業級控管保護您的品牌。 透過跨CDP、CRM、CMS等的無縫整合，[!DNL KALC]可讓行銷人員跨每個管道提供即時個人化，同時提供彈性和可追蹤性，以隨著您的品牌忠誠度成長而改進。

閱讀本指南，瞭解如何使用UI中的來源工作區將您的資料從[!DNL Kobie Streaming Events]連線並串流至Adobe Experience Platform。

>[!IMPORTANT]
>
>如需先決條件設定與對應的詳細資訊，請直接連絡您的[!DNL Kobie Client Services]代表。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

## 瀏覽來源目錄

在Experience Platform UI中，從左側導覽選取「**[!UICONTROL Sources]**」以存取&#x200B;*[!UICONTROL Sources]*&#x200B;工作區。 在&#x200B;*[!UICONTROL Categories]*&#x200B;面板中選取適當的類別。 或者，使用搜尋列導覽至您要使用的特定來源。

若要從[!DNL Kobie]串流資料，請選取&#x200B;*[!UICONTROL Loyalty]*&#x200B;下的&#x200B;**[!UICONTROL Kobie Streaming Events]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL Add data]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL Set up]**&#x200B;選項。 建立已驗證的帳戶後，此選項會變更為&#x200B;**[!UICONTROL Add data]**。

![已選取Kobie串流事件卡的UI中的來源目錄。](../../../../images/tutorials/create/kobie/catalog.png)

## 選取資料

接下來，使用&#x200B;*[!UICONTROL Select data]*&#x200B;介面上傳範例JSON檔案來定義您的來源結構描述。 在此步驟中，您可以使用預覽介面來檢視裝載的檔案結構。 完成後，選取&#x200B;**[!UICONTROL Next]**。

![來源工作流程的選取資料步驟](../../../../images/tutorials/create/kobie/select-data.png)

## 資料流詳細資料

接下來，您必須提供有關資料集和資料流的資訊。

### 資料集詳細資料

資料集是資料集合的儲存和管理結構，通常是包含方案（欄/欄位）和記錄（列）的表格。 成功內嵌至Experience Platform的資料會以資料集的形式保留在資料湖中。

在此步驟中，您可以使用現有的資料集或建立新的資料集。

>[!NOTE]
>
>無論您是使用現有資料集還是建立新資料集，都必須確保您的資料集已啟用設定檔&#x200B;**內嵌**。

+++選取以啟用設定檔擷取、錯誤診斷及部分擷取的步驟。

如果您的資料集已啟用即時客戶個人檔案，那麼在此步驟中，您可以切換&#x200B;**[!UICONTROL Profile dataset]**&#x200B;以啟用您的資料以進行個人檔案擷取。 您也可以使用此步驟來啟用&#x200B;**[!UICONTROL Error diagnostics]**&#x200B;和&#x200B;**[!UICONTROL Partial ingestion]**。

* **[!UICONTROL Error diagnostics]**：選取&#x200B;**[!UICONTROL Error diagnostics]**&#x200B;以指示來源產生錯誤診斷，以便您稍後在監視資料集活動和資料流狀態時參考。
* **[!UICONTROL Partial ingestion]**：部分批次擷取是擷取包含錯誤的資料的能力，最多可達特定可設定的臨界值。 此功能可讓您將所有精確資料成功擷取到Experience Platform，同時所有不正確的資料會個別批次處理，並提供無效原因的資訊。

+++

### 資料流詳細資料

設定資料集後，您必須提供資料流的詳細資訊，包括名稱、選用的說明和警報設定。

![資料流詳細資料介面](../../../../images/tutorials/create/kobie/dataflow-details.png)

| 資料流設定 | 說明 |
| --- | --- |
| 資料流名稱 | 資料流的名稱。 依預設，這將使用正在匯入的檔案名稱。 |
| 說明 | （選用）資料流的簡短說明。 |
| 警報 | Experience Platform可產生使用者可訂閱的事件型警報，這些選項可讓執行中的資料流觸發這些警報。  如需詳細資訊，請閱讀[警示概述](../../alerts.md) <ul><li>**來源資料流執行開始**：選取此警示以在您的資料流執行開始時收到通知。</li><li>**來源資料流執行成功**：選取此警示以在您的資料流結束且沒有任何錯誤時接收通知。</li><li>**來源資料流執行失敗**：選取此警示以在您的資料流執行結束時發生任何錯誤時接收通知。</li></ul> |

{style="table-layout:auto"}

## 對應

在將資料擷取至Experience Platform之前，請使用對應介面將來源資料對應至適當的結構描述欄位。 如需詳細資訊，請閱讀UI](../../../../../data-prep/ui/mapping.md)中的[對應指南。

![工作流程的對應步驟](../../../../images/tutorials/create/kobie/mapping.png)

## 檢閱

*[!UICONTROL Review]*&#x200B;步驟隨即顯示，可讓您在建立資料流之前先檢閱其詳細資訊。 詳細資料會分組到以下類別中：

* **[!UICONTROL Connection]**：顯示帳戶名稱、來源平台和來源名稱。
* **[!UICONTROL Assign dataset and map fields]**：顯示目標資料集以及資料集所遵守的結構描述。

確認詳細資料正確之後，請選取&#x200B;**[!UICONTROL Finish]**。

![來源工作流程中的檢閱步驟。](../../../../images/tutorials/create/kobie/review.png)

## 擷取串流端點URL

建立連線後，來源詳細資訊頁面就會顯示。 此頁面顯示您新建立之連線的詳細資料，包括先前執行的資料流、ID和串流端點URL。

![串流端點URL。](../../../../images/tutorials/create/kobie/streaming-endpoint.png)

## 監視資料流

建立資料流後，您可以監視透過該資料流擷取的資料，以檢視擷取率、成功和錯誤的資訊。 如需有關如何監視資料流的詳細資訊，請參閱有關UI](../../monitor-streaming.md)中[監視帳戶和資料流的教學課程。
