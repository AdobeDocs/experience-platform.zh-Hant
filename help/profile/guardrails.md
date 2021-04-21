---
keywords: Experience Platform；描述檔；即時客戶描述檔；疑難排解；護欄；指導方針；限制；實體；主實體；維實體；
title: 即時客戶個人檔案資料的護欄
solution: Experience Platform
product: experience platform
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform公司提供了一系列的防護措施，幫助您避免建立「即時客戶概要檔案」無法支援的資料模型。 本檔案概述在建立描述檔資料模型時要牢記的最佳實務和限制。
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 1%

---

# [!DNL Real-time Customer Profile]資料的護欄

[!DNL Real-time Customer Profile] 提供個人個人檔案，讓您根據行為見解和客戶屬性，提供個人化的跨通道體驗。為達到此目標，[!DNL Profile]和Adobe Experience Platform的分段引擎使用高度規範化的混合資料模型，為開發客戶個人檔案提供了新的方法。 使用這種混合資料模型，對於正確建模所收集的資料至關重要。 雖然[!DNL Profile]資料存放區維護描述檔資料不是關聯式存放區，但[!DNL Profile]允許與小維度實體整合，以便以簡化且直覺的方式建立區段。 此整合稱為多實體分段。

Adobe Experience Platform提供了一系列防護措施，幫助您避免建立[!DNL Real-time Customer Profile]無法支援的資料模型。 本檔案概述這些護欄，以及使用描述檔資料進行區段時的最佳實務和限制。

>[!NOTE]
>
>本檔案中概述的護欄和限制正在不斷改進。 請定期回訪以取得更新。

## 快速入門

建議您先閱讀下列Experience Platform服務文檔，然後再嘗試建立要用於[!DNL Real-time Customer Profile]的資料模型。 使用資料模型和本文檔中概述的防護措施需要瞭解與管理[!DNL Real-time Customer Profile]實體有關的各種Experience Platform服務：

* [[!DNL Real-time Customer Profile]](home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [Adobe Experience Platform身分服務](../identity-service/home.md):支援建立「客戶的單一視圖」，方法是在客戶被納入時，橋接來自不同資料來源的身分識別 [!DNL Platform]。
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):平台組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../xdm/schema/composition.md):介紹Experience Platform中的方案和資料建模。
* [Adobe Experience Platform區段服務](../segmentation/home.md):內部的分段引擎， [!DNL Platform] 用於根據客戶行為和屬性，從客戶個人檔案建立受眾細分。
   * [多實體分段](../segmentation/multi-entity-segmentation.md):建立將維度圖元與描述檔資料整合的區段的指南。

## 實體類型

[!DNL Profile]儲存資料模型由兩個核心實體類型組成：

* **主要實體：** 主要實體或描述檔實體將資料合併在一起，為個人形成「單一真相來源」。此統一資料使用所謂的「聯合檢視」來表示。 聯合視圖將實施相同類的所有方案的欄位聚合到單個聯合方案中。 [!DNL Real-time Customer Profile]的聯合模式是非規範的混合資料模型，它充當所有配置檔案屬性和行為事件的容器。

   與時間無關的屬性（也稱為「記錄資料」）是使用[!DNL XDM Individual Profile]來建模，而時間系列資料（亦稱為「事件資料」）則是使用[!DNL XDM ExperienceEvent]來模型。 當記錄和時間序列資料在Adobe Experience Platform被吸收時，它會觸發[!DNL Real-time Customer Profile]開始吸收已啟用其使用的資料。 所擷取的互動與詳細資訊越多，個別描述檔就越強穩。

   ![](images/guardrails/profile-entity.png)

* **Dimension實體：** 您的組織也可以定義XDM類別，以說明個人以外的事物，例如商店、產品或屬性。這些非[!DNL XDM Individual Profile]結構稱為「維實體」，不包含時間序列資料。 Dimension實體提供查閱資料，協助並簡化多實體區段定義，且必須足夠小，以讓分段引擎將整個資料集載入記憶體，以進行最佳處理（快速點查閱）。

   ![](images/guardrails/profile-and-dimension-entities.png)

## 限制類型

定義您的資料模型時，建議您保留在提供的防護欄內，以確保正確的效能並避免系統錯誤。 本文中提供的護欄包括兩種限制類型：

* **軟限制：軟** 限制提供建議的最大值，以獲得最佳系統效能。不中斷系統或接收錯誤消息就可以超出軟限制，但超出軟限制將導致效能降低。 建議您保持在軟限制內，以避免整體效能降低。

* **硬限制：** 硬限制為系統提供絕對最大值。超出硬限制將導致中斷和錯誤，使系統無法如預期般運作。

## 資料模型護欄

在建立要與[!DNL Real-time Customer Profile]一起使用的資料模型時，建議遵守以下護欄。

### 主要實體護欄

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 建議為[!DNL Profile]聯合模式貢獻的資料集數 | 20 | Soft | **建議最多20 [!DNL Profile]個啟用的資料集。** 若要為其他資料集啟 [!DNL Profile]用，應先移除或停用現有資料集。 |
| 建議的多實體關係數 | 5 | Soft | **建議在主實體和維實體之間最多定義5個多實體關係。** 在移除或停用現有關係之前，不應建立其他關係映射。 |
| 用於多實體關係之ID欄位的最大JSON深度 | 4 | Soft | **在多實體關係中使用的ID欄位，建議的JSON深度上限為4。** 這表示在高度巢狀結構中，巢狀內嵌超過4個層級的欄位不應當用作關係中的ID欄位。 |
| 描述檔片段中的陣列基數 | &lt;=500 | Soft | **描述檔片段中的最佳陣列基數（與時間無關的資料）為  &lt;>** |
| ExperienceEvent中的陣列基數 | &lt;=10 | Soft | **ExperienceEvent（時間系列資料）中的最佳陣列基數是  &lt;>** |

### Dimension實體護欄

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 不允許非[!DNL XDM Individual Profile]實體使用時間序列資料 | 0 | 硬 | **設定檔服務中的非實體不允許[!DNL XDM Individual Profile] 使用時間序列資料。** 如果時間系列資料集與非[!DNL XDM Individual Profile] ID相關聯，則不應為該資料集啟用 [!DNL Profile]。 |
| 無嵌套關係 | 0 | Soft | **您不應在兩個非結構描述之間建立[!DNL XDM Individual Profile] 關係。** 對於不屬於聯合模式的任何方案，不建議您能夠建立 [!DNL Profile] 關係。 |
| 主要ID欄位的最大JSON深度 | 4 | Soft | **主要ID欄位的建議最大JSON深度為4。** 這表示在高度嵌套的架構中，如果欄位深度超過4個級別，則不應選擇該欄位作為主ID。位於第4個巢狀層級的欄位可用作主要ID。 |

## 資料大小護欄

以下護欄是指資料大小，建議使用，以確保資料可依預期擷取、儲存和查詢。

>[!NOTE]
>
>擷取時，資料大小會測量為JSON中的解壓縮資料。

### 主要實體護欄

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 每個描述檔片段的最大大小 | 10KB | Soft | **建議的描述檔片段大小上限為10KB。** 接收較大的描述檔片段會影響系統效能。例如，載入大量CRM資料集（其中部分描述檔片段大小為50kB）會導致系統效能降低。 |
| 每個描述檔片段的絕對最大大小 | 1MB | 硬 | **描述檔片段的絕對最大大小為1MB。** 嘗試上傳大於1MB的描述檔片段時，擷取會失敗。 |

### Dimension實體護欄

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 所有維圖元的最大總大小 | 5 GB   | Soft | **所有維實體的建議最大總大小為5GB。** 引入大維實體將導致系統效能降低。例如，不建議嘗試將10GB產品目錄載入為維度實體。 |
| 每維實體模式的資料集 | 5 | Soft | **建議最多5個與每個維實體模式關聯的資料集。** 例如，如果您為「產品」建立模式並新增5個貢獻資料集，則不應建立與產品模式連結的第6個資料集。 |

## 分段護欄

本節中概述的防護欄是指組織在Experience Platform中可建立的區段數和性質，以及將區段對應和啟動至目標。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 每個沙盒的區段數上限 | 10K | Soft | **組織可建立的區段數上限為每個沙盒10K。** 組織總共可擁有超過10K個區段，只要每個沙盒中的區段少於10,000個。嘗試建立其他段會導致系統效能降低。 |
| 每個沙盒的串流區段數上限 | 500 | Soft | **組織可建立的串流區段最多為每個沙盒500個。** 一個組織總共可以有500個以上的串流區段，只要每個沙盒中的串流區段少於500個。嘗試建立額外的串流區段會降低系統效能。 |
| 每個沙盒的最大批次區段數 | 10K | Soft | **組織可建立的批次區段數上限為每個沙盒10K。** 組織總共可擁有超過10K個批次區段，只要每個沙盒中的批次區段少於10,000個。嘗試建立其他批處理段會導致系統效能降低。 |
