---
title: Adobe Experience PlatformWeb SDK擴展中的資料元素類型
description: 瞭解Adobe Experience PlatformWeb SDK標籤擴展提供的不同資料元素類型。
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 8%

---


# 資料元素類型

在您 [操作類型](action-types.md) 的 [Adobe Experience PlatformWeb SDK標籤擴展](web-sdk-extension-configuration.md)，必須配置資料元素類型。 此頁描述可用的資料元素類型。

## 事件合併ID {#event-merge-id}

此資料元素能在使用時提供事件合併 ID，而且不需設定。提供的資料元素在訪問者離開頁面或 **[!UICONTROL 重置事件合併ID]** 使用操作類型。

## 身份映射 {#identity-map}

標識映射允許您為網頁訪問者建立標識。 標識映射由命名空間組成，如 _電話_ 或 _電子郵件_，其中每個命名空間包含一個或多個標識符。 例如，如果網站上的個人提供了兩個電話號碼，則您的電話命名空間應包含兩個標識符。

在 [!UICONTROL 身份映射] 資料元素，您將為每個標識符提供以下資訊：

* **[!UICONTROL ID]**:標識訪問者的值。 例如，如果標識符屬於 _電話_ 命名空間， [!UICONTROL ID] 可能 _555-555-555_。 此值通常從JavaScript變數或頁面上的某些其他資料中派生，因此最好建立一個引用頁資料的資料元素，然後在 [!UICONTROL ID] 欄位 [!UICONTROL 身份映射] 資料元素。 如果在您的頁面上運行時，ID值不是填充字串，則標識符將自動從標識映射中刪除。
* **[!UICONTROL 已驗證狀態]**:指示訪問者是否被認證的選擇。
* **[!UICONTROL 主要]**:指示是否應將標識符用作個人的主要標識符的選擇。 如果未將任何標識符標籤為主標識符，則ECID將用作主標識符。

![顯示「編輯資料元素」螢幕的UI影像。](./assets/identity-map-data-element.png)

您不應提供 [!DNL ECID] 生成身份映射時。 使用SDK時， [!DNL ECID] 在伺服器上自動生成並包含在標識映射中。

身份映射資料元常與 [[!UICONTROL XDM對象] 資料元素類型](#xdm-object) 和 [[!UICONTROL 設定同意] 操作類型](action-types.md#set-consent)。

閱讀有關 [Adobe Experience Platform身份服務](../../identity-service/home.md)。

## XDM對象 {#xdm-object}

使用XDM對象資料元素，將資料格式化為XDM更容易。 第一次開啟此資料元素時，請選取正確的 Adobe Experience Platform 沙箱和結構描述。選擇架構後，您將看到架構的結構，您可以輕鬆填寫它。

![顯示XDM對象結構的UI影像。](assets/XDM-object.png)

請注意，當您開啟架構的某些欄位時，例如 `web.webPageDetails.URL`，則會自動收集某些項目。 即使自動收集了多個項目，也可以覆蓋任何項目（如果需要）。 所有值都可手動填寫，也可使用其他資料元素來填寫。

>[!NOTE]
>
>只填寫您感興趣收集的資訊。 資料發送到解決方案時，任何未填入的內容都會被省略。

## (Beta)變數 {#variable}

>[!IMPORTANT]
>
>這是當前的測試版功能，可能會發生更改。 將來的版本可能包含中斷更改。

建立XDM對象的另一種方法是使用 **[!UICONTROL 變數]** 資料元素。 當XDM對象資料元素被引用時建立時，例如在 `sendEvent` 命令 **[!UICONTROL 變數]** 資料元可通過 [!UICONTROL 更新變數] 操作。 要使用資料元素，請選擇正確的Adobe Experience Platform沙盒和架構。

![顯示「建立資料元素」螢幕的UI影像。](assets/variable-data-element.png)

建立此資料元素後，您可以使用 [更新變數](./action-types.md#update-variable) 修改資料元素的操作。 然後，在發送事件操作中使用XDM選項的變數資料元素。

## 後續步驟 {#next-steps}

瞭解特定使用案例，如 [訪問ECID](accessing-the-ecid.md)。
