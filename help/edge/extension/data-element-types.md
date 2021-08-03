---
title: Adobe Experience Platform Web SDK擴充功能中的資料元素類型
description: 了解Adobe Experience Platform Web SDK標籤擴充功能所提供的不同資料元素類型。
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 2f9ff95529c907cfc28bc98198eca9fcfc21e9b9
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 43%

---

# 資料元素類型

在您於[Adobe Experience Platform Web SDK標籤擴充功能](web-sdk-extension-configuration.md)中設定[動作類型](action-types.md)後，請設定您的資料元素類型。

此頁面說明可用的資料元素類型。


## 事件合併 ID

此資料元素能在使用時提供事件合併 ID，而且不需設定。在訪客離開頁面或您使用「重設事件合併 ID」動作類型前，系統提供的資料元素都會保持不變。

## 身分對應

身分對應資料元素可讓您以指定的其他資料元素或其他值建立身分。您建立的所有身分都必須連回相對應的命名空間。此資料元素提供下拉式清單，顯示所有預設命名空間以及您建立的任何命名空間。

![](./assets/identity-map-data-element.png)

## XDM 物件 {#xdm-object}

使用XDM格式將任何資料傳送至Adobe Experience Platform Web SDK。 使用 XDM 物件資料元素可更輕鬆格式化資料。第一次開啟此資料元素時，請選取正確的 Adobe Experience Platform 沙箱和結構描述。選取架構後，您會看到架構的結構，可輕鬆填寫。

![](./assets/XDM-object.png)

請注意，當您開啟架構的某些欄位時（例如`web.webPageDetails.URL`），系統會自動收集某些項目。 即使自動收集了數個項目，您仍可視需要覆寫任何項目。 所有值都可手動填寫，也可使用其他資料元素來填寫。

>[!NOTE]
>
>只填寫您想要收集的資訊。 資料傳送至解決方案時，會忽略未填入的任何項目。
