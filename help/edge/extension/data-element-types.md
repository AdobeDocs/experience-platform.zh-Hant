---
title: Adobe Experience Platform網頁SDK擴充功能中的資料元素類型
description: 瞭解Adobe Experience Platform LaunchAdobe Experience Platform網頁SDK擴充功能提供的不同資料元素類型。
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
translation-type: tm+mt
source-git-commit: 3f7808a08d033c5940d2115006c269b8c4079822
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 47%

---

# 資料元素類型

在[Adobe Experience Platform網頁SDK擴充功能](web-sdk-extension.md)中為[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)設定[動作類型](action-types.md)後，請設定您的資料元素類型。

此頁說明可用的資料元素類型。

## 事件合併 ID

此資料元素能在使用時提供事件合併 ID，而且不需設定。在訪客離開頁面或您使用「重設事件合併 ID」動作類型前，系統提供的資料元素都會保持不變。

## 身分對應

身分對應資料元素可讓您以指定的其他資料元素或其他值建立身分。您建立的所有身分都必須連回相對應的命名空間。此資料元素提供下拉式清單，顯示所有預設名稱空間以及您所建立的任何名稱空間。

![](./assets/identity-map-data-element.png)

## XDM 物件 {#xdm-object}

使用XDM格式將任何資料傳送至Adobe Experience Platform網頁SDK。 使用 XDM 物件資料元素可更輕鬆格式化資料。第一次開啟此資料元素時，請選取正確的 Adobe Experience Platform 沙箱和結構描述。在選取結構後，您會看到結構，您可輕鬆填寫。

![](./assets/XDM-object.png)

請注意，當您開啟結構描述的特定欄位時 (例如「`web.webPageDetails.URL`」)，系統會自動收集部分項目。即使會自動收集數個項目，您也可以視需要覆寫任何項目。 所有值都可手動填寫，也可使用其他資料元素來填寫。

>[!NOTE]
>
>只填寫您有興趣收集的資訊。 當資料傳送至解決方案時，任何未填入的項目都會略過。
