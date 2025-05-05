---
title: 串流SDK UI的檔案自助服務範本
description: 瞭解如何使用UI將來源中的串流資料匯入Adobe Experience Platform。
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---

# 使用UI建立來源連線和資料流以串流&#x200B;*YOURSOURCE*&#x200B;資料

*當您瀏覽此範本時，請取代或刪除所有斜體字的段落（從此段落開始）。*

*從更新頁面頂端的中繼資料（標題和說明）開始。 請忽略此頁面上的所有UICONTROL執行個體。 此標籤可協助我們的機器翻譯流程將頁面正確翻譯為我們支援的多種語言。 我們會在您提交檔案後新增標籤。*

本教學課程提供使用Experience Platform使用者介面建立&#x200B;*YOURSOURCE*&#x200B;來源聯結器的步驟。

## 概觀

*提供您公司的簡短概觀，包括它提供給客戶的價值。 加入產品檔案首頁的連結，以便進一步閱讀。*

>[!IMPORTANT]
>
>此來源聯結器和檔案頁面是由&#x200B;*YOURSOURCE*&#x200B;團隊建立並維護的。 若有任何查詢或更新要求，請直接透過&#x200B;*插入連結或電子郵件地址*&#x200B;連絡您以取得更新。

## 先決條件

*在本節中新增客戶在Adobe Experience Platform使用者介面中開始設定來源之前需要注意的任何相關資訊。 這可能約：*

* *需要新增至允許清單*
* *電子郵件雜湊需求*
* *您這邊的任何帳戶細節*
* *如何取得驗證認證，以連線至您的平台*

### 收集必要的認證

若要將&#x200B;*YOURSOURCE*&#x200B;連線至Experience Platform，您必須提供下列連線屬性的值：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| *認證一* | *請在此加入來源驗證認證的簡短說明* | *請在此加入來源驗證認證的範例* |
| *認證二* | *請在此加入來源驗證認證的簡短說明* | *請在此加入來源驗證認證的範例* |
| *認證三* | *請在此加入來源驗證認證的簡短說明* | *請在此加入來源驗證認證的範例* |

如需這些認證的詳細資訊，請參閱&#x200B;*YOURSOURCE*&#x200B;驗證檔案。 *請在此加入您平台驗證檔案的連結*。

### 將&#x200B;*YOURSOURCE*&#x200B;與您的webhook整合

*串流SDK需要您的來源能夠支援webhook，才能與Experience Platform通訊。 在本節中，您必須提供使用者必須遵循的步驟，才能將YOURSOURCE與webhook整合。*

## 連線您的&#x200B;*YOURSOURCE*&#x200B;帳戶

在Experience Platform UI中，從左側導覽列選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;**串流**&#x200B;類別下，選取&#x200B;*YOURSOURCE*，然後選取&#x200B;**[!UICONTROL 新增資料]**。

>[!TIP]
>
>以下使用的熒幕擷取畫面為範例。 建立檔案時，請以實際來源的熒幕擷取畫面取代影像。 您可以使用相同的標示圖樣和顏色，以及相同的檔案名稱。 請確定熒幕擷圖能擷取整個Experience Platform UI畫面。 如需如何上傳熒幕擷取畫面的資訊，請參閱[提交檔案以供稽核](../documentation/github.md)上的指南。

![Experience Platform來源目錄](../assets/streaming/catalog.png)

## 選取資料

**[!UICONTROL 選取資料]**&#x200B;步驟隨即顯示，提供介面供您選取要帶到Experience Platform的資料。

* 介面的左側是瀏覽器，可讓您檢視帳戶內的可用資料流；
* 介面的右側部分可讓您預覽JSON檔案中最多100列的資料。

選取&#x200B;**[!UICONTROL 上傳檔案]**&#x200B;以從您的本機系統上傳JSON檔案。 或者，您也可以將要上傳的JSON檔案拖放至[!UICONTROL 拖放檔案]面板。

![來源工作流程的新增資料步驟。](../assets/streaming/add-data.png)

上傳檔案後，預覽介面會更新，以顯示您上傳的結構描述預覽。 預覽介面可讓您檢查檔案的內容和結構。 您也可以使用[!UICONTROL 搜尋欄位]公用程式來存取結構描述中的特定專案。

完成後，選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的預覽步驟。](../assets/streaming/preview.png)

## 資料流詳細資料

**資料流詳細資料**&#x200B;步驟隨即顯示，為您提供使用現有資料集或建立資料流新資料集的選項，以及提供資料流名稱和說明的機會。 在此步驟中，您還可以配置設定檔擷取、錯誤診斷、部分擷取和警報的設定。

完成後，選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的資料流詳細資料步驟。](../assets/streaming/dataflow-detail.png)

## 對應

[!UICONTROL 對應]步驟出現，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

Experience Platform會根據您選取的目標結構或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以根據自己的需求，選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算或計算的值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱[資料準備UI指南](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html)。

成功對應來源資料後，請選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的對應步驟。](../assets/streaming/mapping.png)

## 審核

**[!UICONTROL 檢閱]**&#x200B;步驟隨即顯示，可讓您在建立新資料流之前先檢閱該資料流。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **[!UICONTROL 指派資料集與對應欄位]**：顯示要將來源資料擷取到哪個資料集，包括資料集所堅持的結構描述。

檢閱您的資料流後，請按一下[完成] **&#x200B;**，並等待一些時間來建立資料流。

![來源工作流程的稽核步驟。](../assets/streaming/review.png)

## 取得您的串流端點URL

建立串流資料流後，您現在可以擷取串流端點URL。 此端點將用於訂閱您的webhook，讓您的串流來源能夠與Experience Platform通訊。

若要擷取您的串流端點，請移至您剛建立之資料流的[!UICONTROL 資料流活動]頁面，並從[!UICONTROL 屬性]面板底部複製端點。

![資料流活動中的串流端點。](../assets/testing/endpoint-test.png)

## 後續步驟

*建立資料流之剩餘步驟的工作流程會模組化。 如果您想要針對來源發出任何特定的號召，請參閱下列其他資源區段。*

依照本教學課程中的指示，您已建立與您的&#x200B;*YOURSOURCE*&#x200B;帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html)。

## 其他資源

*這是選用的章節，您可以在此提供產品檔案的進一步連結，或任何其他您認為對客戶成功很重要的步驟、熒幕擷取畫面和細微差別。 您可以使用此區段來新增有關您來源的整個工作流程的資訊或提示，尤其是如果有一般使用者可能會遇到的特定「疑問」。*
