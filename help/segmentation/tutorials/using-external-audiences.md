---
keywords: Experience Platform;home；熱門主題
solution: Experience Platform
title: 對受眾細分強制執行資料使用規範
topic: 教學課程
translation-type: tm+mt
source-git-commit: 2ca0768c951cf67a775fdfc2c1f9440596d118bf
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---


# 匯入和使用外部觀眾

Adobe Experience Platform支援匯入外部觀眾的能力，這些觀眾隨後可用作新區段定義的元件。 本檔案提供教學課程，以設定Experience Platform以匯入和使用外部觀眾。

## 快速入門

- [區段服務](../home.md):可讓您從即時客戶個人檔案資料建立受眾細分。
- [即時客戶個人檔案](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
- [體驗資料模型(XDM)](../../xdm/home.md):平台組織客戶體驗資料的標準化架構。
- [資料集](../../catalog/datasets/overview.md):Experience Platform中資料永續性的儲存和管理架構。
- [串流擷取](../../ingestion/streaming-ingestion/overview.md):Experience Platform如何即時從用戶端和伺服器端裝置擷取和儲存資料。

## 為外部觀眾建立身分命名空間

使用外部對象的第一步是建立身分名稱空間。 身分名稱空間可讓平台關聯區段的來源。

要建立標識名稱空間，請按照[標識名稱空間指南](../../identity-service/namespaces.md#manage-namespaces)中的說明操作。 在建立身份名稱空間時，將源詳細資訊添加到身份名稱空間，並將其[!UICONTROL Type]標籤為&#x200B;**[!UICONTROL 非人員標識符]**。

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## 建立區段中繼資料的架構

建立身分命名空間後，您需要為要建立的區段建立新架構。

要開始合成方案，請首先在左側導航欄上選擇&#x200B;**[!UICONTROL 方案]**，然後在方案工作區右上角選擇&#x200B;**[!UICONTROL 建立方案]**。 在此處，選擇&#x200B;**[!UICONTROL Browse]**&#x200B;以查看可用方案類型的完整選擇。

![](../images/tutorials/external-audiences/create-schema-browse.png)

由於您要建立段定義（即預定義的類），因此選擇&#x200B;**[!UICONTROL 使用現有類]**。 現在，選擇&#x200B;**[!UICONTROL 段定義]**&#x200B;類，然後選擇&#x200B;**[!UICONTROL 分配類]**。

![](../images/tutorials/external-audiences/assign-class.png)

現在已建立架構，您需要指定將包含區段ID的欄位。 此欄位應標籤為主標識，並指派給以前建立的名稱空間。

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

將`_id`欄位標示為主要身分後，請選取架構的標題，接著選取標示為&#x200B;**[!UICONTROL Profile]**&#x200B;的切換。 選擇&#x200B;**[!UICONTROL 啟用]**&#x200B;以啟用[!DNL Real-time Customer Profile]的模式。

![](../images/tutorials/external-audiences/schema-profile.png)

現在，此架構已針對描述檔啟用，且主要識別碼已指派給您建立的非人員身分名稱空間。 因此，這表示使用此架構匯入至平台的區段中繼資料將會收錄至「描述檔」，而不會與其他人員相關的描述檔資料合併。

## 為模式建立資料集

設定結構後，您需要為區段中繼資料建立資料集。

要建立資料集，請按照[dataset使用手冊](../../catalog/datasets/user-guide.md#create)中的說明操作。 您將希望使用先前建立的模式，遵循&#x200B;**[!UICONTROL 從模式]**&#x200B;建立資料集選項。

![](../images/tutorials/external-audiences/select-schema.png)

建立資料集後，請繼續遵循[dataset使用指南](../../catalog/datasets/user-guide.md#enable-profile)中的指示，為即時客戶個人檔案啟用此資料集。

![](../images/tutorials/external-audiences/dataset-profile.png)

## 設定並匯入觀眾資料

啟用資料集後，資料現在可以透過UI或使用Experience Platform API傳送至平台。 若要將此資料匯入Platform，您需要建立串流連線。

若要建立串流連線，您可依照[API教學課程](../../sources/tutorials/api/create/streaming/http.md)或[UI教學課程](../../sources/tutorials/ui/create/streaming/http.md)中的指示進行。

建立串流連線後，您就可以存取您唯一的串流端點，以便將資料傳送至。 要瞭解如何將資料發送到這些端點，請閱讀有關流記錄資料的[教程](../../ingestion/tutorials/streaming-record-data.md#ingest-data)。

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## 使用匯入的觀眾建立區段

一旦設定匯入的觀眾後，就可以當做區段程式的一部分使用。 若要尋找外部對象，請前往「區段產生器」，並在&#x200B;**[!UICONTROL 欄位]**&#x200B;區段中選取「對象&#x200B;]**」標籤。**[!UICONTROL 

![](../images/tutorials/external-audiences/external-audiences.png)

## 後續步驟

現在您可以在區段中使用外部對象，您可以使用區段產生器來建立區段。 若要瞭解如何建立區段，請閱讀有關建立區段[的教學課程。](./create-a-segment.md)