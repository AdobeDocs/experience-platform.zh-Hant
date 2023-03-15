---
title: Adobe Experience Platform Web SDK擴充功能中的資料元素類型
description: 了解Adobe Experience Platform Web SDK標籤擴充功能所提供的不同資料元素類型。
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 4caab19e1f58fc5cec5a3c56c43e47786d49c3dc
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 19%

---

# 資料元素類型

在您設定 [動作類型](action-types.md) 在 [Adobe Experience Platform Web SDK標籤擴充功能](web-sdk-extension-configuration.md)，設定您的資料元素類型。

此頁面說明可用的資料元素類型。


## 事件合併 ID

此資料元素能在使用時提供事件合併 ID，而且不需設定。在訪客離開頁面或您使用「重設事件合併 ID」動作類型前，系統提供的資料元素都會保持不變。

## 身分對應

身分對應可讓您為網頁的訪客建立身分。 身分對應包含命名空間，例如 _phone_ 或 _電子郵件_，而每個命名空間都包含一或多個識別碼。 例如，若您網站上的個人已提供兩個電話號碼，您的電話命名空間應包含兩個識別碼。

在 [!UICONTROL 身分對應] 資料元素，您會為每個識別碼提供下列資訊：

* **[!UICONTROL ID]**:識別訪客的值。 例如，如果識別碼屬於 _phone_ 命名空間， [!UICONTROL ID] 可能 _555-555-5555_. 此值通常衍生自JavaScript變數或頁面上的其他資料片段，因此最好建立參考頁面資料的資料元素，然後參考 [!UICONTROL ID] 欄位 [!UICONTROL 身分對應] 資料元素。 如果在您的頁面上執行時，ID值不是填入的字串，則識別碼會自動從身分對應中移除。
* **[!UICONTROL 驗證狀態]**:指出訪客是否已驗證的選取項目。
* **[!UICONTROL 主要]**:指示是否應將標識符用作個人的主要標識符的選擇。 如果未將任何識別碼標示為主要識別碼，系統會將ECID設為主要識別碼。

建立身分對應時，您不應提供ECID。 使用SDK時，系統會自動在伺服器上產生ECID，並包含在身分對應中。

身分對應資料元素通常會與 [[!UICONTROL XDM物件] 資料元素類型](#xdm-object) 和 [[!UICONTROL 設定同意] 動作類型](action-types.md#set-consent).

深入了解 [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hant).

![](./assets/identity-map-data-element.png)

## XDM 物件 {#xdm-object}

使用XDM格式將任何資料傳送至Adobe Experience Platform Web SDK。 使用 XDM 物件資料元素可更輕鬆格式化資料。第一次開啟此資料元素時，請選取正確的 Adobe Experience Platform 沙箱和結構描述。選取架構後，您會看到架構的結構，可輕鬆填寫。

![](./assets/XDM-object.png)

請注意，當您開啟結構的特定欄位時，例如 `web.webPageDetails.URL`，則會自動收集某些項目。 即使自動收集了數個項目，您仍可視需要覆寫任何項目。 所有值都可手動填寫，也可使用其他資料元素來填寫。

>[!NOTE]
>
>只填寫您想要收集的資訊。 資料傳送至解決方案時，會忽略未填入的任何項目。
