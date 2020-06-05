---
keywords: Experience Platform;user guide;attribution ai;popular topics
solution: Experience Platform
title: Attribution AI使用指南
topic: User guide
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---


# Attribution AI使用指南

歸因人工智慧(Attribution AI)是智慧服務的一部分，是多通道的演算法歸因服務，可計算客戶互動對特定結果的影響和增量影響。 借助Attribution AI，行銷人員可以透過瞭解客戶歷程各個階段的每個個別客戶互動的影響，衡量並最佳化行銷和廣告支出。

本檔案可做為在智慧型服務使用者介面中與Attribution AI互動的指南。

## 建立例項

在UI中 [!DNL Adobe Experience Platform] ，按一下左 **側導覽** 中的「服務」。 「服 *務* 」瀏覽器隨即出現，並顯示可用的Adobe智慧服務。 在「歸因AI」的容器中，按一下「 **開啟**」。

![存取您的例項](./images/user-guide/open_Attribution_ai.png)

此時會顯示「歸因AI」服務頁面。 本頁列出Attribution AI的服務例項，並顯示其相關資訊，包括例項名稱、轉換事件、執行例項的頻率，以及上次更新的狀態。 按一 **下「建立例項** 」以開始。

![建立例項](./images/user-guide/landing_page.png)

接著，Attribution AI的設定頁面隨即出現，您可在此提供基本資訊並指定例項的資料集。

![設定頁面](./images/user-guide/setup_attribution.png)

### 命名例項

在「基 *本資訊*」下，為服務實例提供名稱和可選說明。

![命名實例](./images/user-guide/naming_instance.png)

### 選取資料集

填寫基本資訊後，按一下標示「選取資料集」的下拉式清單， **以選取您的資料集** 。 該資料集用於訓練模型並對其生成的後續資料進行評分。 從下拉式選取器選取資料集時，只會列出與Attribution AI相容且符合Experience Data Model(XDM)架構的資料集。 選擇資料集後，按一 **下右上角的** 「下一步」，以繼續定義事件頁面。

![設定頁面](./images/user-guide/initial_creation_attribution.png)

## 定義事件

用於定義事件的輸入資料有三種類型：

- **轉換事件：** 識別行銷活動（例如電子商務訂單、店內採購和網站造訪）影響的業務目標。
- **回顧視窗：** 提供一個時間範圍，指出應包含多少天前的轉換事件觸點。
- **觸點：** 收件者、個人或Cookie層級行銷事件，用來評估轉換的數值或收入型影響。

### 定義轉換事件

若要定義轉換事件，您必須為事件指定名稱，並按一下「輸入欄位名稱」下拉式選單以選 **取事件類型** 。

![是的下拉式清單](./images/user-guide/conversion_event_2.png)

選取事件後，新的下拉式清單會顯示在其右側。 第二個下拉式清單會用來透過使用操作，為您的事件提供進一步的內容。 對於此轉換事件，會使用預 *設操* 作。

>[!NOTE] 當您定義事件時 *，會更新轉換名* 稱下的字串。

![無下拉式清單](./images/user-guide/conversion_event_1.png)

「新 *增事件* 」和「新 ** 增群組」按鈕可用來進一步定義轉換。 視您所定義的轉換而定，您可能需要使用「新增事 *件* 」和「新 ** 增群組」按鈕來提供更多內容。

![新增事件](./images/user-guide/add_event.png)

按一 **下「新增事件** 」會建立其他欄位，這些欄位可使用與上述相同的方法填入。 這樣做會在轉 *換名稱下方的字串定義中新增* AND **&#x200B;陳述式。 按一下 **x** ，移除已新增的事件。

![新增事件功能表](./images/user-guide/add_event_result.png)

按一 **下「新增群組** 」(Add Group)，提供建立與原始欄位不同之其他欄位的選項。 新增群組後，會顯示藍 *色的* 「And」按鈕。 按一 **下** 「And」（和）提供選項，將參數變更為包含「Or」。 「Or」用於定義多個成功的轉換路徑。 「And」延伸轉換路徑，加入其他條件。

![使用和或](./images/user-guide/and_or.png)

如果您需要多個轉換，請按一下「 **新增轉換** 」以建立新的轉換卡。 您可以重複上述程式來定義多個轉換。

![新增轉換](./images/user-guide/add_conversion.png)

### 定義回顧視窗

定義完轉換後，您需要確認回顧視窗。 使用方向鍵或按一下預設值(56)，指定您要包含觸點的轉換事件前幾天。 接觸點在下一步驟中定義。

![回顧](./images/user-guide/lookback_window.png)

### 定義接觸點

定義觸點會遵循類似的工作流程來定 [義轉換](#define-conversion-events)。 一開始，您需要為觸點命名，並從「輸入欄位名稱」下拉式選 *單中選取觸點值* 。 選取後，運算子下拉式清單會出現預設值「存在」。 按一下下拉式清單以顯示運算子清單。

![營運商](./images/user-guide/operators.png)

為此接觸點的目的，請選取「等 **於」**。

![步驟1](./images/user-guide/touchpoint_step1.png)

選取接觸點的運算子後，就 *可使用「輸入欄位值* 」。 「輸入欄位值 ** 」的下拉式值會根據您先前選取的運算元和觸點值填入。 如果值未填入下拉式清單中，您可以手動輸入該值。 按一下下拉式清單，然後選 **取「按一下**」。

>[!NOTE] 運算子&quot;exists&quot;和&quot;not exists&quot;沒有與它們關聯的欄位值。

![接觸點下拉式選單](./images/user-guide/touchpoint_dropdown.png)

「新 *增事件* 」和「新 ** 增群組」按鈕可用來進一步定義您的觸點。 由於觸點周圍的複雜性質，單一觸點有多個事件和群組的情況並不少見。

按一下後， **「新增事件** 」允許新增其他欄位。 按一下 **x** ，移除已新增的事件。

![新增事件](./images/user-guide/touchpoint_add_event.png)

按一 **下「新增群組** 」可讓您選擇建立與原始欄位不同的其他欄位。 新增群組後，會顯示藍 *色的* 「And」按鈕。 按一 **下** 「與」以變更參數，新參數「Or」用於定義多個成功路徑。 此特定觸點只有一條成功路徑，因此不需要「Or」。

![接觸點概述](./images/user-guide/add_group_touchpoint.png)

>[!NOTE] 使用「觸點名 *稱」下方的字串* ，快速概觀您的觸點。 請注意，字串與接觸點的名稱相符。

![](./images/user-guide/touchpoint_string.png)

您可以按一下「新增接觸點」 **並重複上述程式** ，以新增其他接觸點。

![新增觸點](./images/user-guide/add_touchpoint.png)

定義完所有必要的接觸點後，向上捲動並按一下右上角的「 **Next** 」（下一步），繼續最後的步驟。

![完成定義](./images/user-guide/define_event_next.png)

## 進階訓練與計分設定

Attribution AI中的最後一頁是 *Advanced* page，用於設定訓練和計分。

![新增頁面進階](./images/user-guide/advanced_settings.png)

### 排程培訓

使用「 *排程*」，您可以選取要進行計分的一週中的某天和時間。

按一下「計分頻 *率」下方的下拉式清單* ，以選擇每日、每週和每月計分。 接著，選取您要進行計分的一週中的天數。 可選取多天。 按一下一天，再次取消選取。

![排程培訓](./images/user-guide/schedule_training.png)

要更改要進行計分的日期，請按一下時鐘錶徵圖。 在出現的新覆蓋中，輸入您要進行計分的日期。 按一下覆蓋外部以關閉覆蓋。

>[!NOTE] 每個計分程式最多需要24小時才能完成。

![時鐘錶徵圖](./images/user-guide/time_of_day.png)

### 區域型模型（選用）

您客戶的行為可能會因國家／地區和地理區域而大不相同。 對於全球企業而言，使用以國家或地區為基礎的模型可以提高歸因準確度。 每個新增的區域都會建立包含該區域資料的新模型。

要定義新區域，請首先按一下「添加 **區域」**。 在出現的容器中，提供地區名稱。 從「輸入欄位名稱」下拉式清單中只填入一個值(&quot;placeContext.geo.countryCode&quot;) ** 。 選取此值。

![選取地區](./images/user-guide/select_region_att.png)

接著，選取運算子。

![區域算子](./images/user-guide/region_operators.png)

最後，在「輸入欄位值」下拉式清單中 *輸入國家代碼* 。

>[!NOTE] 國家／地區代碼有兩個字元長。 如需完整清單，請 [參閱ISO 3166-1 alpha-2](https://datahub.io/core/country-list)。

![地區](./images/user-guide/region-based.png)

### 培訓窗口

為確保您獲得盡可能精確的模型，請務必使用代表您業務的歷史資料來訓練模型。 根據預設，模型會使用2個季度（6個月）的資料進行訓練。 選擇下拉式清單以變更預設值。 您可以選擇培訓四分之一至四的資料（3-12個月）。

>[!NOTE] 較短的訓練窗口對最近的趨勢更敏感，而較長的訓練窗口則建立更強穩的模型，對最近的趨勢更不敏感。

![訓練窗口](./images/user-guide/training_window.png)

選擇培訓窗口後，按一下右 **上角的** 「完成」。 為資料處理留出一些時間。 完成後，將出現一個快顯對話框，確認實例設定已完成。 單 **擊「確定** 」可重定向到「服務實例 ** 」頁，您可以在該頁看到服務實例。

![設定完成](./images/user-guide/instance_setup_complete.png)

## 後續步驟

遵循本教學課程，您已成功在Attribution AI中建立服務例項。 當例項完成計分（最多允許24小時）後，您就可以發現Attribution AI [見解](./discover-insights.md)。 此外，如果您想要下載計分結果，請造訪下載原始 [分數檔案](./download-scores.md) 。

## 其他資源

以下視訊概述在Attribution AI中建立新例項的端對端工作流程。

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)