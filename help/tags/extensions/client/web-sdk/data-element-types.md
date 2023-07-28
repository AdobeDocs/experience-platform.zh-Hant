---
title: Adobe Experience Platform Web SDK擴充功能中的資料元素型別
description: 瞭解Adobe Experience Platform Web SDK標籤擴充功能所提供的各種資料元素型別。
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 44fac57a30295b476910c0b37314eaebba175157
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 5%

---


# 資料元素類型

在您設定 [動作型別](action-types.md) 在 [Adobe Experience Platform Web SDK標籤擴充功能](web-sdk-extension-configuration.md)，您必須設定資料元素型別。 此頁面說明可用的資料元素型別。

## 身分對應 {#identity-map}

身分對應可讓您建立網頁訪客的身分。 身分對應由名稱空間組成，例如 `CRMID`， `Phone` 或 `Email`，每個名稱空間都包含一或多個識別碼。 例如，如果網站上的個人提供了兩個電話號碼，則您的電話名稱空間應包含兩個識別碼。

在 [!UICONTROL 身分對應] 資料元素中，您會針對每個識別碼提供下列資訊：

* **[!UICONTROL ID]**：識別訪客的值。 例如，如果識別碼屬於 _電話_ 名稱空間， [!UICONTROL ID] 可能是 _555-555-5555_. 此值通常衍生自JavaScript變數或頁面上的其他資料片段，因此最好建立參考頁面資料的資料元素，然後在頁面上的 [!UICONTROL ID] 欄位(在 [!UICONTROL 身分對應] 資料元素。 如果您在頁面上執行時，ID值不是填入的字串，則識別碼會自動從身分對應中移除。
* **[!UICONTROL 已驗證狀態]**：指出訪客是否已驗證的選取範圍。
* **[!UICONTROL 主要]**：指出識別碼是否應作為個人的主要識別碼的選擇。 如果沒有任何識別碼標示為主要，系統會使用ECID作為主要識別碼。

![顯示編輯資料元素畫面的UI影像。](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe建議傳送代表個人的身分，例如 `Luma CRM Id` 作為主要身分。
>
>如果身分對應包含個人識別碼(例如 `Luma CRM Id`)，則人員識別碼會成為主要識別碼。 否則， `ECID` 會成為主要身分。

您不應提供 [!DNL ECID] 建置身分對應時。 使用SDK時， [!DNL ECID] 會在伺服器上自動產生，並包含在身分對應中。

身分對應資料元素通常會與 [[!UICONTROL xdm物件] 資料元素型別](#xdm-object) 和 [[!UICONTROL 設定同意] 動作型別](action-types.md#set-consent).

深入瞭解 [Adobe Experience Platform Identity服務](../../../../identity-service/home.md).

## xdm物件 {#xdm-object}

使用XDM物件資料元素可將資料格式化為XDM較為容易。 第一次開啟此資料元素時，請選取正確的 Adobe Experience Platform 沙箱和結構描述。選取結構描述後，您會看到結構描述的架構，供您輕鬆填寫。

![顯示XDM物件結構的UI影像。](assets/XDM-object.png)

請注意，當您開啟結構描述的特定欄位時，例如 `web.webPageDetails.URL`，則會自動收集某些專案。 即使系統會自動收集多個專案，但您也可以視需要覆寫任何專案。 所有值都可手動填寫，也可使用其他資料元素來填寫。

>[!NOTE]
>
>僅填入您想收集的資訊片段。 資料傳送至解決方案時，系統會忽略未填寫的專案。

## 變數 {#variable}

建立XDM物件的另一種方法是使用 **[!UICONTROL 變數]** 資料元素。 而XDM物件資料元素是在參考時建立的，例如在 `sendEvent` 指令， **[!UICONTROL 變數]** 資料元素可透過以下方式更新： [!UICONTROL 更新變數] 動作。 若要使用資料元素，請選取正確的Adobe Experience Platform沙箱和結構描述。

![顯示「建立資料元素」畫面的UI影像。](assets/variable-data-element.png)

建立此資料元素後，您就可以使用 [更新變數](./action-types.md#update-variable) 動作以修改資料元素。 然後在傳送事件動作中，對XDM選項使用變數資料元素。

## 後續步驟 {#next-steps}

瞭解特定使用案例，例如 [存取ECID](accessing-the-ecid.md).
