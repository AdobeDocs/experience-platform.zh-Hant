---
title: Adobe Experience Platform Web SDK擴充功能中的資料元素型別
description: 瞭解Adobe Experience Platform Web SDK標籤擴充功能所提供的各種資料元素型別。
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 8cb8dcf7217440da98f6856293c530a66d4c3444
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 5%

---

# 資料元素類型

在標籤擴充功能中設定[動作型別](actions/actions-overview.md)之後，您必須設定資料元素型別。 此頁面說明可用的資料元素型別。

## 身分對應 {#identity-map}

身分對應可讓您建立網頁訪客的身分。 身分對應包含`CRMID`、`Phone`或`Email`等名稱空間，每個名稱空間包含一或多個識別碼。 例如，如果網站上的個人提供了兩個電話號碼，則您的電話名稱空間應包含兩個識別碼。

在[!UICONTROL Identity map]資料元素中，您將為每個識別碼提供下列資訊：

* **[!UICONTROL ID]**：識別訪客的值。 例如，如果識別碼屬於&#x200B;_電話_&#x200B;名稱空間，[!UICONTROL ID]可以是&#x200B;_555-555-5555_。 此值通常衍生自頁面上的JavaScript變數或某些其他資料，因此最好建立參照頁面資料的資料元素，然後參照[!UICONTROL ID]資料元素內[!UICONTROL Identity map]欄位中的資料元素。 如果您在頁面上執行時，ID值不是填入的字串，則識別碼會自動從身分對應中移除。
* **[!UICONTROL Authenticated state]**：指出訪客是否已驗證的選取範圍。
* **[!UICONTROL Primary]**：指出識別碼是否應作為個人主要識別碼的選項。 如果沒有任何識別碼標示為主要，系統會使用ECID作為主要識別碼。

![顯示[編輯資料元素]畫面的UI影像。](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe建議將代表個人的身分識別（例如`Luma CRM Id`）傳送為主要身分。
>
>如果身分對應包含人員識別碼（例如`Luma CRM Id`），則人員識別碼將成為主要識別碼。 否則，`ECID`會成為主要身分。

建立身分對應時，您不應該提供[!DNL ECID]。 使用SDK時，伺服器上會自動產生[!DNL ECID]，並包含在身分對應中。

身分對應資料元素通常搭配[[!UICONTROL Variable]](#variable)資料元素和[[!UICONTROL Set consent]](actions/set-consent.md)動作使用。

深入瞭解[Adobe Experience Platform Identity服務](/help/identity-service/home.md)。

## xdm物件 {#xdm-object}

使用XDM物件資料元素可將資料格式化為XDM較為容易。 第一次開啟此資料元素時，請選取正確的 Adobe Experience Platform 沙箱和結構描述。選取結構描述後，您會看到結構描述的架構，供您輕鬆填寫。

顯示XDM物件結構的![UI影像。](assets/XDM-object.png)

請注意，當您開啟結構描述的特定欄位時（例如「`web.webPageDetails.URL`」），系統會自動收集部分專案。 即使系統會自動收集多個專案，但您也可以視需要覆寫任何專案。 所有值都可手動填寫，也可使用其他資料元素來填寫。

>[!NOTE]
>
>僅填入您想收集的資訊片段。 資料傳送至解決方案時，系統會忽略未填寫的專案。

## 變數 {#variable}

您可以使用&#x200B;**[!UICONTROL Variable]**&#x200B;資料元素來建立裝載物件。 同時支援[!UICONTROL XDM]和[!UICONTROL Data]物件。

* 當您選取[!UICONTROL XDM]時，請選取所需的[!UICONTROL Sandbox]和[!UICONTROL Schema]。
* 當您選取[!UICONTROL Data]時，請選取所需的解決方案。 可用的解決方案包括[!UICONTROL Adobe Analytics]和[!UICONTROL Adobe Target]。

![顯示資料元素選項的標籤UI影像。](assets/variable-data-element.png)

建立此資料元素之後，您可以使用[更新變數](actions/update-variable.md)動作來修改它。 準備就緒後，您可以在[傳送事件](actions/send-event.md)動作中包含此資料元素，以將資料傳送至資料流。

## 媒體：體驗品質 {#quality-experience}

將串流媒體事件傳送到Adobe Experience Platform時，**[!UICONTROL Quality of Experience]**&#x200B;資料元素會很有幫助。 您可在建立媒體工作階段時新增此元素，而下列媒體事件將包含更新的體驗品質資料。

![顯示[建立體驗資料元素品質]畫面的UI影像。](assets/qoe-data-element.png)

## 後續步驟 {#next-steps}

瞭解特定使用案例，例如[存取ECID](accessing-the-ecid.md)。
