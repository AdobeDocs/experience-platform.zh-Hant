---
title: 在UI中將Oracle Eloqua (V2)連線至Experience Platform
description: 瞭解如何在UI中將您的Oracle Eloqua帳戶連結至Experience Platform。
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 1%

---

# 在UI中將[!DNL Oracle Eloqua] (V2)連線至Experience Platform

[!DNL Oracle Eloqua (V2)]來源聯結器可讓您將Oracle Eloqua帳戶與Adobe Experience Platform連線，以自動化且可擴充的方式擷取重要的B2B行銷資料，包括連絡人、帳戶、行銷活動和參與活動。

使用此來源聯結器設定安全驗證，選取您需要的確切Eloqua資料實體，並將它們對應至標準化體驗資料模型(XDM)結構描述。 彈性的排程選項可讓您設定初始資料載入和循環的增量同步，確保您的行銷資料保持最新且可行。

[!DNL Oracle Eloqua (V2)]來源聯結器以Adobe的企業擷取架構為基礎，可為行銷活動最佳化、效能測量及跨管道個人化提供可靠、可擴充的基礎。

閱讀本指南，瞭解如何使用Experience Platform使用者介面中的來源工作區將您的[!DNL Oracle Eloqua]帳戶連結至Adobe Experience Platform。

## 開始使用

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

### 收集必要的認證 {#credentials}

閱讀[[!DNL Eloqua] 總覽](../../../../connectors/marketing-automation/eloqua.md)以取得驗證的相關資訊。

## 瀏覽來源目錄 {#catalog}

在Experience Platform UI中，從左側導覽選取「**[!UICONTROL Sources]**」以存取&#x200B;*[!UICONTROL Sources]*&#x200B;工作區。 選擇類別或使用搜尋列來尋找您的來源。

若要連線到[!DNL Eloqua]，請移至&#x200B;*[!UICONTROL Marketing Automation]*&#x200B;類別，選取&#x200B;**[!UICONTROL (V2) Oracle Eloqua]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL Set up]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL Set up]**&#x200B;選項。 建立已驗證的帳戶後，此選項會變更為&#x200B;**[!UICONTROL Add data]**。

![來源目錄中的Eloqua來源卡片，其設定按鈕反白顯示。](../../../../images/tutorials/create/eloqua/catalog.png)

## 使用現有帳戶 {#existing}

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL Existing account]**，然後選取您要使用的[!DNL Eloqua]帳戶。

![在帳戶建立介面中選取的現有帳戶選項。](../../../../images/tutorials/create/eloqua/existing.png)

## 建立新帳戶 {#new}

若要建立新帳戶，請選取&#x200B;**[!UICONTROL New account]**，並在您的[!UICONTROL Source connection details]下提供名稱和說明。 接下來，在[!UICONTROL Account authentication]底下，提供您的&#x200B;**使用者端識別碼**、**使用者端密碼**、**使用者名稱**、**密碼**&#x200B;以及&#x200B;**基底端點**&#x200B;的值。 您可以閱讀[驗證指南](../../../../connectors/marketing-automation/eloqua.md)，瞭解這些認證的詳細資訊。 完成時，請選取&#x200B;**[!UICONTROL Connect to source]**，並等待幾秒鐘讓您的連線建立。

![新帳戶介面，其中包含來源連線詳細資料和驗證認證的欄位。](../../../../images/tutorials/create/eloqua/new.png)

## 選取資料

使用選取資料介面來選取您要擷取至Experience Platform的[!DNL Eloqua]實體。

>[!TIP]
>
>選取資料時，您會注意到，除行銷活動外，其他實體會顯示代表性範例資料。 此方法可確保您可以預覽可用欄位和結構，因為[!DNL Eloqua]個公用API目前僅能擷取行銷活動的實際資料。 對於其餘實體，會提供範例資料以支援您的設定工作流程。

![資料選取介面顯示可用的Eloqua資料實體。](../../../../images/tutorials/create/eloqua/select-data.png)

## 資料集和資料流詳細資料 {#details}

接下來，您必須提供有關資料集和資料流的資訊。 在此步驟中，您可以使用現有的資料集或建立新的資料集。 此外，您可以選擇在此步驟中啟用資料集以擷取至Real-Time Customer Profile。

![資料集和資料流詳細資訊介面，其中包含設定資料集屬性的選項。](../../../../images/tutorials/create/eloqua/details.png)

## 對應 {#mapping}

[!DNL Eloqua]的對映會組織為四種主要實體型別：

* **帳戶** — 來自[!DNL Eloqua]的公司/組織記錄。
* **活動** — 來自[!DNL Eloqua]的行銷活動和參與事件。
* **行銷活動** — 來自[!DNL Eloqua]的行銷活動記錄。
* **連絡人** — 來自[!DNL Eloqua]的個人記錄。

如果您需要存取預設提供欄位以外的其他欄位，可以使用Experience Platform中的資料準備對應程式新增這些欄位。 如果預設（標準）結構描述不支援某些必填欄位，您可以選擇在Experience Platform中定義自訂結構描述。 使用此功能來建立並對應必要的欄位，以便您可以順暢地將所有相關資料從[!DNL Eloqua]擷取到Experience Platform。

後續步驟摘要：

* 檢閱整合提供的預設對應欄位。
* 在對應步驟期間，包括[!DNL Eloqua]所需的任何其他欄位。
* 如果標準結構描述中未出現新欄位，請在Experience Platform中擴充或建立包含這些欄位的自訂結構描述。
* 完成對應以確保所有所需資料皆已擷取。

為確保您的外部CRM資訊能正確反映，只需在資料準備中使用計算欄位函式，以來源資料欄位中的特定CRM執行個體識別碼來更新`{CRM_INSTANCE_ID}`預留位置。 這可讓您靈活地量身打造整合，以符合貴組織的獨特設定。

若要使用計算欄位編輯器，請選取您要更新的來源欄位。

![含有計算欄位的Eloqua來源欄位。](../../../../images/tutorials/create/eloqua/select-calculated-field.png)

>[!BEGINTABS]

>[!TAB Salesforce]

對於[!DNL Salesforce]使用者，請使用計算欄位編輯器並使用適當的執行個體識別碼更新`{CRM_INSTANCE_ID}`。

![Salesforce的計算欄位。](../../../../images/tutorials/create/eloqua/sf-field.png)

>[!TAB Microsoft Dynamics]

對於[!DNL Microsoft]使用者，請使用計算欄位編輯器並使用適當的執行個體識別碼更新`{CRM_INSTANCE_ID}`。

![Dynamics的計算欄位。](../../../../images/tutorials/create/eloqua/dynamics-field.png)

>[!ENDTABS]

更新完計算欄位後，請選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![顯示Eloqua資料實體欄位對應的對應介面。](../../../../images/tutorials/create/eloqua/mapping.png)

## 排程

>[!NOTE]
>
>以下是內部用於增量資料載入的差異欄位：
>
>* **連絡人：** `C_DateModified`
>* **帳戶：** `M_DateModified`
>* **活動：** `CreatedAt`
>* **自訂物件：** `UpdatedAt`
>* **行銷活動：** `updatedAt`

對應完成後，您現在可以為資料流設定擷取排程。 將您的[!UICONTROL Frequency]設為`Once`以設定單次擷取執行。 對於增量擷取，您可以將[!UICONTROL Frequency]設定為`Hour`、`Day`或`Week`。 使用增量擷取時，您也必須設定[!UICONTROL Interval]以定義擷取執行之間發生的時間量。 例如，擷取頻率設為`Day`，而間隔設為`15`，表示您的資料流已排程每15天擷取一次資料。

[!DNL Eloqua]來源無法使用每分鐘擷取頻率。 您可以選擇的最頻繁排程為每小時。 選取符合您資料新鮮度需求的排程。 請記住，選擇更頻繁的排程會增加運算成本。

![排程介面，其中包含設定擷取頻率和間隔的選項。](../../../../images/tutorials/create/eloqua/scheduling.png)

## 檢閱

設定擷取排程後，請使用[!UICONTROL Review]介面確認資料流的詳細資料。 選取「**[!UICONTROL Finish]**」以完成設定，並留出一些時間讓您的資料流啟動。

![檢閱介面會在完成前顯示資料流組態的摘要。](../../../../images/tutorials/create/eloqua/review.png)

## 監視

選取資料流後，資料流會執行一次性資料回填，並依指定的排程進行後續的增量同步。 您可以導覽至資料流，以監視同步的狀態。 如需詳細資訊，請閱讀UI[中](../../../../../dataflows/ui/monitor-sources.md)監視來源資料流程的指南。

## 後續步驟

您現在已在Experience Platform中完成[!DNL Eloqua]來源的設定和組態。 建立您的資料流後，將會根據您選擇的排程擷取您的[!DNL Eloqua]資料，並對應至標準體驗資料模型(XDM)結構描述。 繼續監控您的資料流，並在Platform中探索您擷取的資料，以獲得深入見解並啟用您的行銷使用案例。 如需進階設定和疑難排解的詳細資訊，請參閱相關檔案或聯絡Adobe支援資源。

如需其他資訊，請閱讀以下檔案：

* [來源概觀](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)
