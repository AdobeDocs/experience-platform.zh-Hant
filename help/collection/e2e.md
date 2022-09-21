---
title: 資料收集端對端概述
description: 概略說明如何使用Adobe Experience Platform的資料收集功能，將事件資料傳送至Adobe Experience Cloud解決方案。
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: da17b273d5464ecd8b00aa37de51425ce3a9a576
workflow-type: tm+mt
source-wordcount: '2619'
ht-degree: 0%

---

# 資料收集端對端概述

Adobe Experience Platform會收集您的資料，並將其傳輸至其他Adobe產品和協力廠商目的地。 若要將事件資料從您的應用程式傳送至Experience Platform邊緣網路，請務必了解這些核心技術，以及如何設定這些技術，以便在您需要時將您的資料傳送至所需的目的地。

本指南提供高階教學課程，說明如何使用Platform的資料收集功能，透過邊緣網路傳送事件。 具體來說，本教學課程會逐步說明在資料收集UI(原稱為Adobe Experience Platform Launch)中安裝和設定Adobe Experience Platform Web SDK標籤擴充功能的步驟。

>[!NOTE]
>
>如果您不想使用標籤，也可以選擇手動安裝及設定SDK，但您仍須依照下列說明完成相關步驟。
>
>所有與資料收集UI相關的步驟也可在Experience PlatformUI中執行。

## 先決條件

本教學課程使用資料收集UI來建立結構、設定資料流和安裝Web SDK。 若要在UI中執行這些動作，您必須獲得至少一個Web屬性的存取權，以及下列項目 [屬性權利](../tags/ui/administration/user-permissions.md#property-rights):

* 開發
* 管理擴充功能

請參閱 [管理資料收集的權限](./permissions.md) 了解如何授予屬性和屬性權限的存取權。

若要使用本指南中提及的各種資料收集產品，您還必須擁有資料流的存取權，以及建立和管理結構的功能。 若您需要存取其中一項功能，請聯絡您的CSM以協助您取得必要的存取權。 請注意，如果您尚未購買Adobe Experience Platform,Adobe會免費提供您使用SDK的必要存取權。

如果您已擁有Platform的存取權，您必須確保擁有 [權限](../access-control/home.md#permissions) 在啟用的下列類別下：

* 資料模型製作
* 身分

請參閱 [存取控制UI概述](../access-control/ui/overview.md) 了解如何將Platform功能的權限授與使用者。

## 流程摘要

為您的網站設定資料收集的程式摘要如下：

1. [建立結構](#schema) 以決定傳送至邊緣網路時的資料結構。
1. [建立資料流](#datastream) 設定您要將資料傳送至哪些目的地。
1. [安裝及配置Web SDK](#sdk) 在網站上發生某些事件時傳送資料至資料流。

將資料傳送至邊緣網路後，您也可以選擇 [設定事件轉送](#event-forwarding) 如果貴組織有授權。

## 建立方案 {#schema}

[Experience Data Model(XDM)](../xdm/home.md) 是開放原始碼規格，以結構形式為資料提供通用結構和定義。 換句話說，XDM是以可由邊緣網路和其他Adobe Experience Cloud應用程式操作的方式，來建構和格式化資料。

設定資料收集作業的第一步，是建立XDM結構以呈現資料。 在本教學課程的稍後步驟中，您會將您要傳送的資料對應至此結構。

>[!NOTE]
>
>XDM結構可供自訂。 以下概述的步驟並非過於規範，而是特別著重於Web SDK的結構需求。 在這些參數之外，您可以自由定義資料的剩餘結構。

在UI中，選取 **[!UICONTROL 結構]** 的下一頁。 從這裡，您可以看到先前建立的結構清單，這些結構屬於您的組織。 若要繼續，請選取 **[!UICONTROL 建立結構]**，然後選取 **[!UICONTROL XDM ExperienceEvent]** 從下拉式功能表。

![結構工作區](./images/e2e/schemas.png)

將出現一個對話框，提示您開始向架構添加欄位組。 若要使用Web SDK傳送事件，您必須新增欄位群組 **[!UICONTROL AEP Web SDK ExperienceEvent Mixin]**. 此欄位群組包含Web SDK程式庫自動收集之資料屬性的定義。

使用搜尋列縮小清單，以便更輕鬆地尋找此欄位群組。 找到它後，請先從清單中選取它，然後再選取 **[!UICONTROL 新增欄位群組]**.

![結構工作區](./images/e2e/add-field-group.png)

架構畫布隨即顯示，其中顯示XDM架構的樹狀結構，包括Web SDK欄位群組提供的欄位。

![綱要結構](./images/e2e/schema-structure.png)

在樹中選擇要開啟的根欄位 **[!UICONTROL 架構屬性]** 在右側邊欄中，您可以提供結構的名稱和選用說明。

![為架構命名](./images/e2e/name-schema.png)

如果要將更多欄位新增至結構，可以選取 **[!UICONTROL 新增]** 在 **[!UICONTROL 欄位群組]** 區段。

![新增欄位群組](./images/e2e/add-field-groups.png)

>[!NOTE]
>
>請參閱 [新增欄位群組](../xdm/ui/resources/schemas.md#add-field-groups) 請參閱XDM檔案，了解如何根據您的使用案例搜尋不同欄位群組的詳細步驟。
>
>最佳實務是只新增您計畫透過邊緣網路傳送之資料的欄位。 將欄位新增至架構並儲存後，之後就只能對架構進行加入式變更。 請參閱 [模式演化規則](../xdm/schema/composition.md#evolution) 以取得更多資訊。

新增您需要的欄位後，請選取 **[!UICONTROL 儲存]** 以儲存結構。

![儲存結構](./images/e2e/save-schema.png)

## 建立資料流 {#datastream}

資料流是可告訴邊緣網路您要將資料傳送至何處的設定。 具體而言，資料流會指定您要將資料傳送至哪些Experience Cloud產品，以及您希望在每個產品中處理和儲存資料的方式。

>[!NOTE]
>
>如果您想使用 [事件轉送](../tags/ui/event-forwarding/overview.md) （假設貴組織已獲授權使用功能），您必須以啟用Adobe產品的相同方式，為資料流啟用。 有關此程式的詳細資訊，請參閱 [稍後部分](#event-forwarding).

選擇 **[!UICONTROL 資料流]** 的下一頁。 您可以從此處選取要編輯的現有資料流，或選取 **[!UICONTROL 新資料流]**.

![資料串流](./images/e2e/datastreams.png)

資料流的設定需求取決於您要傳送資料的產品和功能。 有關每個產品的配置選項的詳細資訊，請參閱 [資料流概觀](../edge/datastreams/overview.md).

## 安裝及配置Web SDK {#install}

建立結構和資料流後，下一步是安裝並設定Platform Web SDK，以開始將資料傳送至邊緣網路。

>[!NOTE]
>
>本節使用資料收集UI來設定Web SDK標籤擴充功能，但您也可以改用原始程式碼來安裝及設定。 如需詳細資訊，請參閱下列指南：
>
>* [安裝SDK](../edge/fundamentals/installing-the-sdk.md)
>* [配置SDK](../edge/fundamentals/configuring-the-sdk.md)
>
>另請注意，即使您只想使用事件轉送，您仍須依照說明安裝及設定SDK，才能在 [稍後步驟](#event-forwarding).

該過程可概括如下：

1. [在標籤屬性上安裝Adobe Experience Platform Web SDK](#install-sdk) 以獲得其功能。
1. [建立XDM物件資料元素](#data-element) 將網站上的變數對應至您先前建立之XDM架構的結構。
1. [建立規則](#rule) 告知SDK何時應將資料傳送至邊緣網路。
1. [建置和安裝程式庫](#library) 以在您的網站上實作規則。

### 將SDK安裝在標籤屬性上 {#install-sdk}

選擇 **[!UICONTROL 標籤]** 在左側導覽中，顯示標籤屬性清單。 您可以選擇要編輯的現有屬性，也可以選取 **[!UICONTROL 新屬性]** 。

![屬性](./images/e2e/properties.png)

如果建立新屬性，請提供描述性名稱並設定 [!UICONTROL 平台] to **[!UICONTROL Web]**. 為Web屬性提供完整網域，然後選取 **[!UICONTROL 儲存]**.

![建立屬性](./images/e2e/create-property.png)

屬性的概觀頁面隨即顯示。 從此處，選擇 **[!UICONTROL 擴充功能]** 在左側導覽器中，然後選取 **[!UICONTROL 目錄]**. 尋找Platform Web SDK的清單（選擇性使用搜尋列來縮小結果），然後選取 **[!UICONTROL 安裝]**.

![安裝Web SDK](./images/e2e/install-sdk.png)

此時會出現SDK的設定頁面。 大部分必要值會自動填入預設值，您可以視需要選擇變更。

![配置Web SDK](./images/e2e/configure-sdk.png)

不過，您必須先選取資料流，資料流才能知道要將資料傳送至何處，才能安裝SDK。 在 **[!UICONTROL 資料流]**，請使用下拉式選單，選取您在 [先前步驟](#datastream). 設定資料流後，請選取 **[!UICONTROL 儲存]** 完成將SDK安裝至屬性。

![設定資料流和儲存](./images/e2e/set-datastream.png)

### 建立XDM資料元素 {#data-element}

為了讓SDK將資料傳送至邊緣網路，該資料必須對應至您在 [上一步](#schema). 此對應是透過使用資料元素來完成。

在UI中，選取 **[!UICONTROL 資料元素]**，然後選取 **[!UICONTROL 建立新資料元素]**.

![建立新資料元素](./images/e2e/data-elements.png)

在下一個畫面中，選取 **[!UICONTROL Adobe Experience Platform Web SDK]** 在 [!UICONTROL 擴充功能] 下拉式清單，然後選取 **[!UICONTROL XDM物件]** （適用於資料元素類型）。

![XDM物件類型](./images/e2e/xdm-object.png)

XDM對象類型的配置對話框隨即出現。 對話方塊會自動選取您的Platform沙箱，您可在此處查看該沙箱中建立的所有結構。 從清單中選取您先前建立的XDM架構。

![XDM物件類型](./images/e2e/select-schema.png)

架構的結構隨即出現。 具有星號(**\***)指出在事件引發時自動填入的欄位。 對於所有其他欄位，您可以探索架構的結構，並填寫其餘的資料。

![將資料對應至XDM欄位](./images/e2e/map-schema.png)

>[!NOTE]
>
>上方的螢幕擷取示範如何從網站的用戶端對應可全域存取的變數(`cartAbandonsTotal`)，並參考 [!UICONTROL 值] 欄位，周圍是百分比符號(`%`)。
>
>您也可以使用其他先前建立的資料元素來填入這些欄位。 請參閱 [資料元素](../tags/ui/managing-resources/data-elements.md) ，以取得詳細資訊。

將資料對應到結構後，請先提供資料元素的名稱，再選取 **[!UICONTROL 儲存]**.

![命名並儲存資料元素](./images/e2e/name-and-save.png)

### 建立規則

儲存資料元素後，下一步是建立規則，當網站上發生特定事件時（例如客戶新增產品至購物車時），將其傳送至Edge Network。

您幾乎可以為網站上可能發生的任何事件設定規則。 例如，本節說明如何建立客戶提交表單時觸發的規則。 以下HTML代表具有「加到購物車」表單的簡單網頁，此表單將是規則的主題：

```html
<!DOCTYPE html>
<html>
<body>

  <form id="add-to-cart-form">
    <label for="item">Product:</label><br>
    <input type="text" id="item" name="item"><br>
    <label for="amount">Amount:</label><br>
    <input type="number" id="amount" name="amount" value="1"><br><br>
    <input type="submit" value="Add to Cart">
  </form> 

</body>
</html>
```

在資料收集UI中，選取 **[!UICONTROL 規則]** 在左側導覽器中，然後選取 **[!UICONTROL 建立新規則]**.

![規則](./images/e2e/rules.png)

在下一個畫面中，提供規則的名稱。 接下來的步驟是決定規則的事件（亦即規則將於何時引發）。 選擇 **[!UICONTROL 新增]** 在 [!UICONTROL 事件].

![名稱規則](./images/e2e/name-rule.png)

此時將顯示事件配置頁。 若要設定事件，您必須先選取事件類型。 事件類型由擴充功能提供。 例如，若要設定「表單提交」事件，請選取 **[!UICONTROL 核心]** 擴充功能，然後選取 **[!UICONTROL 提交]** 事件類型 **[!UICONTROL 表單]** 類別。

>[!NOTE]
>
>如需Adobe網頁擴充功能所提供不同事件類型的詳細資訊，包括如何設定這些類型，請參閱 [Adobe擴充功能參考](../tags/extensions/web/overview.md) 在標籤檔案中。

表單提交事件可讓您使用 [CSS選取器](https://www.w3schools.com/css/css_selectors.asp) 以參考要引發規則的特定元素。 在以下範例中，ID `add-to-cart-form` 使用時，此規則只會針對「新增至購物車」表單觸發。 選擇 **[!UICONTROL 保留變更]** 將事件新增至規則。

![事件設定](./images/e2e/event-config.png)

「規則設定」頁面會重新顯示，指出已新增事件。 您可以縮小「[!UICONTROL 若]」，為規則新增更多條件。

否則，下一步是新增規則的動作，以便規則觸發時執行。 選擇 **[!UICONTROL 新增]** 在 **[!UICONTROL 動作]** 繼續。

![新增動作](./images/e2e/add-action.png)

此時將顯示操作配置頁。 若要取得將資料傳送至邊緣網路的規則，請選取 **[!UICONTROL Adobe Experience Platform Web SDK]** ，以及 **[!UICONTROL 傳送事件]** （針對動作類型）。

![動作類型](./images/e2e/action-type.png)

畫面會更新，顯示設定傳送事件動作的其他選項。 在 **[!UICONTROL 類型]**，您可以提供自訂類型值，以填入 `eventType` XDM欄位。 在 **[!UICONTROL XDM資料]**，提供您先前建立之XDM資料類型的名稱（由百分比符號包圍），或選取資料庫圖示(![資料庫表徵圖](./images/e2e/database-symbol.png))從清單中選取。 這些資料最終會傳送至邊緣網路。

選擇 **[!UICONTROL 保留變更]** 完成時。

![動作設定](./images/e2e/action-config.png)

完成規則設定後，請選取 **[!UICONTROL 儲存]** 來完成這個過程。

![儲存規則](./images/e2e/save-rule.png)

### 建置和安裝程式庫 {#library}

設定規則後，您就可以將其新增至標籤程式庫、將該程式庫建置至環境，然後在您的網站上安裝該組建。

>[!NOTE]
>
>如果您尚未在資料收集UI中設定環境，您必須先設定環境，才能建立組建。 請參閱 [為web屬性設定環境](../tags/ui/publishing/environments.md#web-configuration) ，以取得詳細資訊。

若要了解如何建立程式庫、將擴充功能和規則新增至程式庫，以及將該程式庫建置至環境，請參閱 [管理程式庫](../tags/ui/publishing/libraries.md) 在標籤檔案中。 建立程式庫時，請務必加入Platform Web SDK擴充功能及您先前建立的資料收集規則。

建立程式庫並將其組建指派給環境後，您就可以將該環境安裝在網站的用戶端。 請參閱 [安裝環境](../tags/ui/publishing/environments.md#installation) 以取得更多資訊。

在網站上安裝環境後，您可以 [測試您的實作](../tags/ui/publishing/embed-code-testing.md) 使用Adobe Experience Platform Debugger。

## 設定事件轉送（選用） {#event-forwarding}

>[!NOTE]
>
>事件轉送僅適用於已獲得其授權的組織。

一旦您將SDK設定為將資料傳送至邊緣網路，您可以設定事件轉送，告知邊緣網路您要將該資料傳送至何處。

若要使用事件轉送，您必須先建立事件轉送屬性。 選擇 **[!UICONTROL 事件轉送]** 在左側導覽中，然後選取 **[!UICONTROL 新屬性]**. 在選取 **[!UICONTROL 儲存]**.

建立事件轉送屬性後，下一步就是建立規則，以決定應將資料傳送至何處。 事件轉送屬性的規則的建構方式與標籤屬性大致相同，但無法指定任何事件（因為事件轉送僅處理其直接從資料流收到的事件）。 針對規則的動作，您可以使用其中一個可用的事件轉送擴充功能，或使用自訂程式碼來傳送事件。

![事件轉送規則](./images/e2e/event-forwarding-rule.png)

與之前類似，設定規則後，您必須將其新增至程式庫，並將該程式庫建置至環境。

建置完成後，最後一步就是更新您的資料流 [先前已設定](#datastream) 和啟用事件轉送。 若要開始，請導覽至 **[!UICONTROL 資料流]** 並從清單中選取相關的資料流。 從這裡，啟用事件轉送的切換按鈕，並提供您剛設定的屬性和環境名稱。

![事件轉送資料流](./images/e2e/event-forwarding-datastream.png)

## 後續步驟

本指南提供如何使用Platform Web SDK將資料傳送至邊緣網路的高階端對端概述。 請參閱本指南中連結的檔案，以取得有關各個元件和服務的詳細資訊。
