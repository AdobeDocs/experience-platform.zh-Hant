---
title: 透過UI將您的Salesforce Marketing Cloud (V2)帳戶連線至Experience Platform
description: 瞭解如何透過UI將您的Salesforce Marketing Cloud (V2)帳戶連結至Experience Platform。
source-git-commit: 91bf8bf6e6f7030574d693484ce9797800c2d5dd
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 1%

---

# 將[!DNL Salesforce Marketing Cloud]連線至Experience Platform

閱讀本指南，瞭解如何使用Experience Platform使用者介面中的來源工作區將您的[!DNL Salesforce Marketing Cloud]帳戶連結至Adobe Experience Platform。

## 開始使用

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

### 收集必要的認證

閱讀[[!DNL Salesforce Marketing Cloud] 總覽](../../../../connectors/marketing-automation/sfmc.md#prerequisites)以取得驗證的相關資訊。

## 瀏覽來源目錄

在Experience Platform UI中，從左側導覽選取「**[!UICONTROL Sources]**」以存取&#x200B;*[!UICONTROL Sources]*&#x200B;工作區。 選擇類別或使用搜尋列來尋找您的來源。

若要連線到[!DNL Salesforce Marketing Cloud]，請移至&#x200B;*[!UICONTROL Marketing Automation]*&#x200B;類別，選取&#x200B;**[!UICONTROL (V2) Salesforce Marketing Cloud]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL Set up]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL Set up]**&#x200B;選項。 建立已驗證的帳戶後，此選項會變更為&#x200B;**[!UICONTROL Add data]**。

![已選取Salesforce Marketing Cloud來源的來源目錄。](../../../../images/tutorials/create/sfmc/catalog.png)

## 使用現有帳戶 {#existing}

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL Existing account]**，然後選取您要使用的[!DNL Salesforce Marketing Cloud]帳戶。

![來源工作流程的現有帳戶介面](../../../../images/tutorials/create/sfmc/existing.png)

## 建立新帳戶 {#new}

若要建立新帳戶，請選取&#x200B;**[!UICONTROL New account]**，並在您的[!UICONTROL Source connection details]下提供名稱和說明。 接下來，在[!UICONTROL Account authentication]底下，提供您&#x200B;**使用者端識別碼**、**使用者端密碼**&#x200B;和&#x200B;**基底端點**&#x200B;的值。 您可以閱讀[驗證指南](../../../../connectors/marketing-automation/sfmc.md#gather-required-credentials)，瞭解這些認證的詳細資訊。 完成時，請選取&#x200B;**[!UICONTROL Connect to source]**，並等待幾秒鐘讓您的連線建立。

![來源工作流程的新帳戶介面。](../../../../images/tutorials/create/sfmc/new.png)

## 選取資料

[!DNL Salesforce Marketing Cloud]來源僅支援從[!DNL Salesforce Marketing Cloud]資料延伸擷取資料。

使用[!UICONTROL Select data]介面選取您要從[!DNL Salesforce Marketing Cloud]執行個體擷取的資料延伸模組。 選取資料擴充功能後，您可以使用預覽面板來確認資料集包含預期的欄位，然後再繼續。

![來源工作流程的選取資料步驟](../../../../images/tutorials/create/sfmc/select-data.png)

## 資料集和資料流詳細資料

接下來，您必須提供有關資料集和資料流的資訊。 在此步驟中，您可以使用現有的資料集或建立新的資料集。 此外，您可以選擇在此步驟中啟用資料集以擷取至Real-Time Customer Profile。

![來源工作流程的資料集和資料流詳細資料步驟。](../../../../images/tutorials/create/sfmc/dataset-details.png)

## 對應

在[!DNL Salesforce Marketing Cloud]中，資料延伸不會被視為標準物件。 因此，沒有預先定義或固定的對應欄位至Experience Platform結構描述。 雖然Experience Platform中的「資料準備」會盡力在[!DNL Salesforce Marketing Cloud]的來源欄位和目標體驗資料模型(XDM)結構描述之間保持一致，但在某些情況下，仍需要手動檢閱或調整以解決未對應或錯誤的欄位。

![來源工作流程的對應步驟。](../../../../images/tutorials/create/sfmc/mapping.png)

## 排程資料流

對應完成後，您現在可以為資料流設定擷取排程。 將您的[!UICONTROL Frequency]設為`Once`以設定單次擷取執行。 對於增量擷取，您可以將[!UICONTROL Frequency]設定為`Hour`、`Day`或`Week`。 使用增量擷取時，您也必須設定[!UICONTROL Interval]以定義擷取執行之間發生的時間量。 例如，擷取頻率設為`Day`，而間隔設為`15`，表示您的資料流已排程每15天擷取一次資料。

>[!TIP]
>
> [!DNL Salesforce Marketing Cloud]來源無法使用每分鐘擷取頻率。 您可以選擇的最頻繁排程為每小時。 選取符合您資料新鮮度需求的排程。 請記住，選擇更頻繁的排程會增加運算成本。

您必須在資料集中選取差異（日期/時間）欄位，才能啟用增量同步。 如果您的資料集未包含適當的差異欄位，您將無法建立資料流。

![來源工作流程的排程步驟。](../../../../images/tutorials/create/sfmc/schedule.png)

## 檢閱

設定擷取排程後，請使用[!UICONTROL Review]介面確認資料流的詳細資料。 選取「**[!UICONTROL Finish]**」以完成設定，並留出一些時間讓您的資料流啟動。

![來源工作流程的稽核步驟。](../../../../images/tutorials/create/sfmc/review.png)

## 監視

選取資料流後，資料流會執行一次性資料回填，並依指定的排程進行後續的增量同步。 您可以導覽至資料流，以監視同步的狀態。 如需詳細資訊，請閱讀UI[中](../../../../../dataflows/ui/monitor-sources.md)監視來源資料流程的指南。

## 後續步驟

本教學課程引導您使用使用者介面將[!DNL Salesforce Marketing Cloud] (V2)帳戶連線至Experience Platform。 您已瞭解如何選取或建立來源帳戶、提供所需的認證、選擇要擷取的資料延伸模組、指定資料集和資料流詳細資訊、對應您的資料、設定資料擷取排程，以及監視您的資料流。 按照這些步驟，您已成功將[!DNL Salesforce Marketing Cloud]資料與Experience Platform整合，以進行啟用和分析。

如需其他資訊，請閱讀以下檔案：

* [來源概觀](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)

