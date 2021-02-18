---
title: Adobe Experience Platform Web SDK Extension中的資料元素類型
description: 瞭解Adobe Experience Platform Launch中Adobe Experience Platform Web SDK擴充功能提供的不同資料元素類型。
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 78%

---


# 資料元素類型

在[Adobe Experience Platform Web SDK擴充功能](web-sdk-extension.md)中為[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)設定[動作類型](action-types.md)後，請設定您的資料元素類型。

此頁說明可用的資料元素類型。

## 事件合併 ID

此資料元素能在使用時提供事件合併 ID，而且不需設定。在訪客離開頁面或您使用「重設事件合併 ID」動作類型前，系統提供的資料元素都會保持不變。

## 身分對應

身分對應資料元素可讓您以指定的其他資料元素或其他值建立身分。您建立的所有身分都必須連回相對應的命名空間。此資料元素的下拉式選單會顯示所有預設的命名空間，以及您建立的所有命名空間。

![](./assets/identity-map-data-element.png)

## XDM 物件

您傳送至 Adobe Experience Platform Web SDK 的所有資料都應採用 XDM 格式。使用 XDM 物件資料元素可更輕鬆格式化資料。第一次開啟此資料元素時，請選取正確的 Adobe Experience Platform 沙箱和結構描述。選取結構描述後，您會看到結構描述的架構，供您輕鬆填寫。

![](./assets/XDM-object.png)

請注意，當您開啟結構描述的特定欄位時 (例如「`web.webPageDetails.URL`」)，系統會自動收集部分項目。即使系統會自動收集多個項目，不過您還是可以視需求選擇覆寫任何項目。所有值都可手動填寫，也可使用其他資料元素來填寫。

>[!NOTE]
>
>您只需填寫想收集的資訊片段。資料傳送至解決方案後，系統會忽略未填寫的項目。
