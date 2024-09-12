---
title: 身分圖表連結規則的實作指南
description: 瞭解使用身分圖表連結規則設定實作資料時，建議遵循的步驟。
badge: Beta
exl-id: 368f4d4e-9757-4739-aaea-3f200973ef5a
source-git-commit: cfa2cd91f523d80fd42cb6fd2ba17e6eb3eca609
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 2%

---

# 身分圖表連結規則的實作指南

>[!AVAILABILITY]
>
>身分圖表連結規則目前處於Beta版。 如需參與率條件的詳細資訊，請聯絡您的Adobe客戶團隊。 功能和檔案可能會有所變更。

請參閱本檔案，瞭解在使用Adobe Experience Platform Identity Service實作資料時可遵循的逐步指南。

逐步大綱：

1. [建立必要的身分名稱空間](#namespace)
2. [使用圖表模擬工具來熟悉身分最佳化演演算法](#graph-simulation)
3. [使用身分設定工具來指定您專屬的名稱空間，並設定名稱空間的優先順序排名](#identity-settings)
4. [建立體驗資料模型(XDM)結構描述](#schema)
5. [建立資料集](#dataset)
6. [將您的資料內嵌至Experience Platform](#ingest)

## 預先實作必要條件

開始之前，您必須先確定系統中的已驗證事件一律包含人員識別碼。

## 設定許可權 {#set-permissions}

Identity Service實作程式中的第一個步驟，是確保將您的Experience Platform帳戶新增至已布建必要許可權的角色。 您的管理員可以導覽至Adobe Experience Cloud中的許可權UI，設定您帳戶的許可權。 之後，您的帳戶必須新增至具有以下許可權的角色：

* [!UICONTROL 檢視身分設定]：套用此許可權，以便在身分名稱空間瀏覽頁面中檢視唯一的名稱空間和名稱空間優先順序。
* [!UICONTROL 編輯身分設定]：套用此許可權，以便能夠編輯並儲存您的身分設定。

如需許可權的詳細資訊，請閱讀[許可權指南](../../access-control/abac/ui/permissions.md)。

## 建立您的身分識別名稱空間 {#namespace}

如果您的資料需要這些資料，您必須先為組織建立適當的名稱空間。 如需如何建立自訂名稱空間的步驟，請閱讀[在UI](../features/namespaces.md#create-custom-namespaces)中建立自訂名稱空間的指南。

## 使用圖表模擬工具 {#graph-simulation}

接下來，導覽至Identity Service UI工作區中的[圖形模擬工具](./graph-simulation.md)。 您可以使用圖表模擬工具來模擬使用各種不同唯一名稱空間和名稱空間優先順序設定所建立的身分圖表。

透過建立不同的設定，您可以使用圖表模擬工具來學習和更好地瞭解身分最佳化演演算法和特定設定如何影響您的圖表行為。

## 設定身分設定 {#identity-settings}

一旦您知道您想要圖形的行為方式，請瀏覽至Identity Service UI工作區中的[身分設定工具](./identity-settings-ui.md)。

使用身分設定工具來指定您唯一的名稱空間，並依優先順序設定您的名稱空間。 套用完設定後，您必須至少等待六個小時才能繼續內嵌資料，因為新設定至少需要六個小時才能反映在Identity Service中。

## 建立 XDM 結構描述 {#schema}

在建立唯一的名稱空間和名稱空間優先順序後，您現在可以繼續進行必要的設定，以擷取您的資料。 首先，您必須建立XDM結構描述。 根據您的資料，您可能需要為XDM Individual Profile和XDM ExperienceEvent建立結構。

若要將資料內嵌至Real-time Customer Profile，您必須確保您的結構描述至少包含一個已指定為主要身分的欄位。 透過設定主要身分，您可以為設定檔擷取啟用指定的結構描述。

如需如何建立結構描述的指示，請閱讀[在UI](../../xdm/tutorials/create-schema-ui.md)中建立XDM結構描述的指南。

## 建立資料集 {#dataset}

接下來，建立資料集以針對您要擷取的資料提供結構。 資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 資料集與結構描述搭配使用，若要將資料擷取到即時客戶個人檔案，您的資料集必須啟用個人檔案擷取。 為了針對設定檔啟用您的資料集，它必須參考針對設定檔擷取啟用的結構描述。

如需如何建立資料集的說明，請參閱[資料集UI指南](../../catalog/datasets/user-guide.md)。

## 擷取您的資料 {#ingest}

>[!WARNING]
>
>* 在預先實作程式中，您必須確保系統要傳送給Experience Platform的已驗證事件一律包含人員識別碼，例如CRMID。
>* 在實作期間，您必須確保每個設定檔中一律有最高優先順序的唯一名稱空間。 請參閱[附錄](#appendix)以取得圖表案例的範例，其可透過確保每個設定檔都包含具有最高優先順序的唯一名稱空間來解決。
>* 如果您使用[Adobe Analytics來源聯結器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)來內嵌資料，則您必須為ECID指定比AAID更高的優先順序，因為Identity Service會封鎖AAID。 透過優先處理ECID，您可以指示即時客戶設定檔將未驗證事件儲存至ECID而非AAID。

此時，您應該具備下列專案：

* 存取Identity Service功能的必要許可權。
* 資料適用的名稱空間。
* 為名稱空間指定的唯一名稱空間和設定的優先順序。
* 至少一個XDM結構描述。 （根據您的資料和特定使用案例，您可能需要建立設定檔和體驗事件結構。）
* 以您的結構描述為基礎的資料集。

完成上述所有專案後，您就可以開始將資料內嵌至Experience Platform中。 您可以透過數種不同的方式執行資料擷取。 您可以使用下列服務將您的資料帶入Experience Platform：

* [批次和串流擷取](../../ingestion/home.md)
* [Experience Platform中的資料收集](../../collection/home.md)
* [Experience Platform來源](../../sources/home.md)

>[!TIP]
>
>擷取您的資料後，XDM原始資料裝載不會變更。 您仍可在UI中看到主要身分設定。 不過，身分設定將會覆寫這些設定。

如需任何意見，請使用Identity Service UI工作區中的&#x200B;**[!UICONTROL Beta意見]**&#x200B;選項。

## 附錄 {#appendix}

請參閱本節，瞭解實作身分設定和唯一名稱空間時可參考的其他資訊。

### 單一人員名稱空間需求 {#single-person-namespace-requirement}

您必須確保在代表個人的所有設定檔中使用單一名稱空間。 如此一來，Identity Service就能偵測指定圖表中的適當人員識別碼。

>[!BEGINTABS]

>[!TAB 沒有單一人員識別碼名稱空間]

如果沒有能代表您個人識別碼的唯一名稱空間，您最終可能會看到將不同的個人識別碼連結至相同ECID的圖表。 在此範例中，B2BCRM和B2CCRM會同時連結至相同的ECID。 此圖表建議Tom使用其B2C登入帳戶與Summer共用裝置（使用她的B2B登入帳戶）。 但是，系統將識別這是一個設定檔（圖形摺疊）。

![兩個人員識別碼連結至相同ECID的圖表案例。](../images/graph-examples/multi_namespaces.png)

>[!TAB 具有單一人員識別碼名稱空間]

指定唯一的名稱空間（在此案例中是CRMID，而不是兩個完全不同的名稱空間），Identity Service就能夠識別上次與ECID建立關聯的人員識別碼。 在此範例中，由於存在唯一的CRMID，Identity Service能夠識別「共用裝置」情境，其中兩個實體共用相同裝置。

![共用裝置圖表情境，其中兩個人員識別碼連結至相同的ECID，但舊連結被移除。](../images/graph-examples/crmid_only_multi.png)

>[!ENDTABS]

### Danging loginID案例 {#dangling-loginid-scenario}

下圖會模擬「懸浮」登入ID案例。 在此範例中，兩個不同的loginID已繫結至相同的ECID。 但是，`{loginID: ID_C}`未連結至CRMID。 因此，Identity Service無法偵測這兩個loginID代表兩個不同的實體。

>[!BEGINTABS]

>[!TAB 不明確的登入ID]

在此範例中，`{loginID: ID_C}`懸空且未連結至CRMID。 因此，此loginID應關聯的個人實體變得模稜兩可。

![具有「懸浮」登入ID情境的圖表範例。](../images/graph-examples/dangling_example.png)

>[!TAB loginID已連結至CRMID]

在此範例中，`{loginID: ID_C}`連結至`{CRMID: Tom}`。 因此，系統能夠識別此loginID與Tom相關聯。

![LoginID已連結至CRMID。](../images/graph-examples/id_c_tom.png)

>[!TAB loginID已連結至另一個CRMID]

在此範例中，`{loginID: ID_C}`連結至`{CRMID: Summer}`。 因此，系統能夠識別此loginID與另一個個人實體（在此例中為Summer）相關聯。

此範例也顯示Tom和Summer是共用裝置的不同個人實體，以`{ECID: 111}`表示。

![LoginID已連結至另一個CRMID。](../images/graph-examples/id_c_summer.png)

>[!ENDTABS]
