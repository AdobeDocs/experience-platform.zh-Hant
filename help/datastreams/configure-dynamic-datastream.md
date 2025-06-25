---
title: 建立動態資料流設定
description: 瞭解如何根據規則建立動態資料串流設定，將您的資料路由至各種Experience Cloud服務。
hide: true
hidefromtoc: true
badge: label="Beta" type="Informative"
exl-id: 528ddf89-ad87-4021-b5a6-8e25b4469ac4
source-git-commit: 8ce5b6718861d01731b9aab9f81645f2aeb2970f
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 3%

---

# 建立動態資料流設定

>[!AVAILABILITY]
>
>* 定義動態資料流設定的選專案前在Beta中，可供有限數量的客戶使用。 若要取得此功能的存取權，請聯絡您的Adobe代表。 文件和功能可能會有所變更。

依預設，Experience Platform Edge Network會將到達資料串流的所有事件傳送至您已為資料串流啟用的所有Experience Cloud [服務](configure.md#add-services)。 根據您的使用案例，這可能並不總是適合您的理想工作流程。

動態資料流設定可透過使用者可設定的規則集來解決此問題；您可為為資料流啟用的每個服務定義這些規則集，而這些規則集會規定哪些Experience Cloud解決方案應接收每種型別的資料。

## 先決條件 {#prerequisites}

若要為資料串流建立動態設定，您必須符合兩個條件：

* 您必須已建立至少&#x200B;*個*&#x200B;資料流才能使用。 如需詳細資訊，請參閱有關如何[建立資料流](configure.md)的檔案。
* 您必須將&#x200B;*至少*&#x200B;個Experience Cloud服務新增至資料流。 如需詳細資訊，請參閱有關如何[新增服務](configure.md#add-services)到資料流的檔案。

建立資料串流並新增Experience Cloud服務之後，您可以[建立動態組態](#create-dynamic-configuration)。

## 護欄 {#guardrails}

動態資料流設定具有特定限制和效能限制，可確保最佳系統效能和資料處理效率。 設定動態資料流規則時，以下護欄適用：

| 護欄 | 限制 | 限制型別 |
|---------|------------|------|
| Experience Platform服務的每個資料流的最大動態資料流設定數 | 5 | 效能護欄 |
| 事件轉送的每個資料流的最大動態資料流設定數 | 5 | 效能護欄 |
| Adobe Analytics每個資料流的最大動態資料流設定數 | 5 | 效能護欄 |
| Adobe Target每個資料流的最大動態資料流設定數 | 5 | 效能護欄 |
| Adobe Audience Manager每個資料流的最大動態資料流設定數 | 5 | 效能護欄 |
| 您可以在單一規則中結合的條件（述詞）最大數量 | 100 | 效能護欄 |
| 逾時前評估每個資料流的所有動態資料流設定所允許的最長時間 | 25毫秒 | 系統強制的護欄 |

## 動態資料流設定與資料流設定覆寫 {#dynamic-versus-overrides}

動態資料流設定和[資料流設定覆寫](overrides.md)是互斥功能。

這表示您無法使用動態資料流設定以及資料流設定覆寫。 您必須選擇一個或另一個。

如果您同時啟用動態資料流設定和資料流設定覆寫，設定覆寫將取得優先權，且動態資料流設定規則將被忽略。

## 建立動態資料流設定 {#create-dynamic-configuration}

在您[建立資料流](configure.md)並[新增服務](configure.md#add-services)之後，請依照下列步驟將動態設定新增至服務。

1. 移至&#x200B;**[!UICONTROL 資料收集]** > **[!UICONTROL 資料串流]**&#x200B;頁面，並選取您建立的資料串流。

   ![顯示資料串流清單的資料串流使用者介面影像。](assets/configure-dynamic-datastream/select-datastream.png)

1. 在您要定義動態組態的服務上選取&#x200B;**[!UICONTROL 編輯]**&#x200B;選項。

   ![資料串流使用者介面的影像，顯示新增至資料串流的服務。](assets/configure-dynamic-datastream/select-service.png)

1. 在&#x200B;**[!UICONTROL 設定]**&#x200B;頁面中，選取&#x200B;**[!UICONTROL 儲存並編輯動態設定]**。

   ![顯示資料流設定頁面之資料流使用者介面的影像。](assets/configure-dynamic-datastream/save-and-edit.png)

1. 選取&#x200B;**[!UICONTROL 新增動態組態]**。

   ![資料串流使用者介面的影像，顯示未新增規則的動態設定。](assets/configure-dynamic-datastream/add-dynamic-config.png)

1. 從&#x200B;**[!UICONTROL 資源]**&#x200B;面板，將您想要用來建置規則的專案拖放到視窗右側。 您可以合併多個資源以建置複雜規則。

   使用每個資源的選項，例如&#x200B;**[!UICONTROL 等於]**、**[!UICONTROL 不等於]**、**[!UICONTROL 存在]**&#x200B;等等，以微調規則。

   ![顯示動態設定規則之資料串流使用者介面的影像。](assets/configure-dynamic-datastream/drag-resources.png)

1. 在&#x200B;**[!UICONTROL 組態]**&#x200B;區段中，根據您是否要傳送資料給每個服務，切換您要為每個規則啟用或停用的服務。 如果您關閉切換功能，服務路由會停用，而且不會將任何資料&#x200B;*傳送至上游服務。*

   ![顯示動態設定規則之資料串流使用者介面的影像。](assets/configure-dynamic-datastream/enable-service.png)

1. 設定完規則後，選取[儲存]。**&#x200B;**

## 規則優先順序的考量事項 {#considerations}

您可以為每個動態資料流設定定義多個規則。 但是，如果您的資料符合多個規則的條件，則只會考慮清單中的第一個相符規則，而所有其他相符規則則會被忽略。

若要達到所需的資料路由行為，請留意規則的排列順序。

若要設定規則順序，您可以依照所需的順序拖放規則視窗。

![GIF顯示如何透過拖放來變更規則順序。](assets/configure-dynamic-datastream/move-rules.gif)

## 規則適用性條件 {#eligibility-criteria}

動態資料流設定必須符合特定的資格標準，以確保高效能、可維護性和清晰度。 以下是定義規則的主要需求和最佳實務。

### 支援的資料型別 {#supported-data-types}

動態資料流設定規則可與特定資料型別搭配使用，以確保最佳效能和可靠的資料路由。 瞭解哪些資料型別受到支援，可協助您建立有效規則，以有效處理您的資料。

| 資料類型 | 狀態 | 附註 |
|-----------|--------|-------|
| 字串 | 允許 | - |
| 數字（整數、長、短、位元組） | 允許 | - |
| 列舉 | 允許 | - |
| 布林值 | 允許 | - |
| 日期 | 允許 | - |
| 陣列 | 不允許 | 不支援以陣列為基礎的規則，因為它們可能會降低效能。 |
| 地圖 | 不允許 | 不支援以地圖為基礎的規則，因為它們可能會降低效能。 |

### 支援的運運算元 {#supported-operators}

根據資料型別，規則可以使用以下運運算元：

| 資料類型 | 支援的運運算元 |
|-----------|-------------------|
| **字串** | `equals`、`starts with`、`ends with`、`contains`、`exists`、`does not equal`、`does not start with`、`does not end with`、`does not contain`、`does not exist` |
| **數字（長、整數、短、位元組）** | `equals`，`does not equal`，`greater than`，`less than`，`greater than or equal to`，`less than or equal to`，`exists`，`does not exist` |
| **布林值** | `equals true/false`、`does not equal true/false` |
| **列舉** | `equals`、`does not equal`、`exists`、`does not exist` |
| **日期** | `today`、`yesterday`、`this month`、`this year`、`custom date`、`in last`、`from`、`during`、`within`、`before`、`after`、`rolling range`、`in next`、`exists`、`does not exist` |
| **邏輯** | `INCLUDE`， `ANY/ALL` （相當於AND/OR） |

>[!NOTE]
>
>不直接支援&#x200B;**[!UICONTROL EXCLUDE]**&#x200B;運運算元，但您可以使用&#x200B;**[!UICONTROL INCLUDE]**&#x200B;搭配否定比較運運算元（例如「不等於」）來達到同等邏輯。

### 規則結構 {#rule-structure}

為動態資料流設定建立規則時，瞭解確保最佳效能和系統相容性的結構需求很重要。 規則結構會直接影響系統處理及路由資料的效率。

**僅使用一般運算式**。 您必須將規則定義為平面邏輯運算式。 不支援巢狀邏輯運算式（使用容器或多個層級的AND/OR）。 如果您需要複雜的邏輯，請將其分成多個一般規則。

例如，請考量下圖所示的複雜規則。

![顯示複雜規則的平台UI影像。](assets/configure-dynamic-datastream/complex-rule.png)

您可以將此規則分成下列較簡單的規則：

![顯示複雜規則的平台UI影像。](assets/configure-dynamic-datastream/simple-rule-1.png)

![顯示複雜規則的平台UI影像。](assets/configure-dynamic-datastream/simple-rule-2.png)

**避免複雜的規則**。 更簡單的規則可確保更快的評估和更好的可維護性。

### 最佳作法 {#best-practices}

建立動態資料流設定規則時，遵循最佳實務可確保最佳效能、系統可靠性和可維護的設定。 這些指引可協助您避免常見陷阱，並建立順暢配合平台架構的有效規則。

* **保持規則簡單且平坦。**&#x200B;如果您需要表達複雜的邏輯，請使用多個規則而非巢狀內嵌。
* **僅使用[支援的資料型別](#supported-data-types)和[運運算元](#supported-operators)。**
* **測試您的規則效能。**&#x200B;過於複雜或不支援的規則可能會導致系統拒絕這些規則或影響系統效能。





