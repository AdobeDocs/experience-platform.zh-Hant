---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: 體驗平台方針
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 1%

---


# [!DNL Platform] 護欄 [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] 提供個人個人檔案，讓您根據行為見解和客戶屬性，提供個人化的跨通道體驗。 為達到此目標，Adobe Experience Platform中的 [!DNL Profile] 細分引擎使用高度規範化的混合資料模型，提供開發客戶個人檔案的新方式。 使用這種混合資料模型，對於正確建模所收集的資料至關重要。 雖然資 [!DNL Profile] 料存放區維護描述檔資料不是關聯式存放區，但 [!DNL Profile] 允許與小維度實體整合，以便以簡化且直覺的方式建立區段。 此整合稱為多實體分段。

Adobe Experience Platform提供一系列的防護措施，幫助您避免建立無法支援的 [!DNL Real-time Customer Profile] 資料模型。 本檔案概述使用維度實體時的最佳實務和限制，尤其是在批次分段中。

>[!NOTE]
>
>本檔案中概述的護欄和限制正在不斷改進。 請定期回訪以取得更新。

## 快速入門

建議您先閱讀下列Experience Platform服務檔案，再嘗試建立資料模型以供使用 [!DNL Real-time Customer Profile]。 使用資料模型及本檔案中概述的防護措施，需要瞭解管理實體時涉及的各種Experience Platform服 [!DNL Real-time Customer Profile] 務：

* [[!DNL Real-time Customer Profile]](home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [Adobe Experience Platform Identity Service](../identity-service/home.md):支援建立「客戶的單一視圖」，方法是在客戶被納入時，橋接來自不同資料來源的身分識別 [!DNL Platform]。
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):平台組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../xdm/schema/composition.md):介紹Experience Platform中的架構和資料模型。
* [Adobe Experience Platform細分服務](../segmentation/home.md):此分段引擎用 [!DNL Platform] 於根據客戶行為和屬性，從客戶個人檔案建立受眾細分。
   * [多實體分段](../segmentation/multi-entity-segmentation.md):建立將維度圖元與描述檔資料整合的區段的指南。

## 實體類型

儲存 [!DNL Profile] 資料模型由兩種核心實體類型組成：

* **主要實體：** 主要實體或描述檔實體將資料合併在一起，為個人形成「單一真相來源」。 此統一資料使用所謂的「聯合檢視」來表示。 聯合視圖將實施相同類的所有方案的欄位聚合到單個聯合方案中。 的聯合模式是 [!DNL Real-time Customer Profile] 非標準化的混合資料模型，它充當所有配置檔案屬性和行為事件的容器。

   時間無關屬性（也稱為「記錄資料」）是使用建模 [!DNL XDM Individual Profile]，而時間系列資料（亦稱為「事件資料」）是使用建模 [!DNL XDM ExperienceEvent]。 當記錄和時間系列資料在Adobe Experience Platform中擷取時，會觸 [!DNL Real-time Customer Profile] 發開始擷取已啟用使用的資料。 所擷取的互動與詳細資訊越多，個別描述檔就越強穩。

   ![](images/guardrails/profile-entity.png)

* **維實體：** 貴組織也可以定義XDM類別，以說明個人以外的事物，例如商店、產品或屬性。 這些非結構[!DNL XDM Individual Profile] (Non-Schemas)稱為「維實體」，不包含時間序列資料。 維度實體提供查閱資料，協助並簡化多實體區段定義，且必須足夠小，以讓分段引擎將整個資料集載入記憶體，以進行最佳處理（快速點查閱）。

   ![](images/guardrails/profile-and-dimension-entities.png)

## 限制類型

定義您的資料模型時，建議您保留在提供的防護欄內，以確保正確的效能並避免系統錯誤。 本文中提供的護欄包括兩種限制類型：

* **軟限制：** 軟限制提供建議的最大值，以獲得最佳系統效能。 不中斷系統或接收錯誤消息就可以超出軟限制，但超出軟限制將導致效能降低。 建議您保持在軟限制內，以避免整體效能降低。

* **硬限制：** 硬限制為系統提供絕對最大值。 超出硬限制將導致中斷和錯誤，使系統無法如預期般運作。

## 資料模型護欄

在建立要與一起使用的資料模型時，建議遵守以下護欄 [!DNL Real-time Customer Profile]。

### 主要實體護欄

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 建議為聯合模式貢獻的數 [!DNL Profile] 據集數 | 20 | Soft | **建議最多20 [!DNL Profile]個啟用的資料集。** 若要為其他資料集啟 [!DNL Profile]用，應先移除或停用現有資料集。 |
| 建議的多實體關係數 | 5 | Soft | **建議在主實體和維實體之間最多定義5個多實體關係。** 在移除或停用現有關係之前，不應建立其他關係映射。 |
| 用於多實體關係之ID欄位的最大JSON深度 | 4 | Soft | **在多實體關係中使用的ID欄位，建議的JSON深度上限為4。** 這表示在高度巢狀結構中，巢狀內嵌超過4個層級的欄位不應當用作關係中的ID欄位。 |
| 描述檔片段中的陣列基數 | &lt;=500 | Soft | **描述檔片段（與時間無關的資料）中的最佳陣列基數為&lt;=500。** |
| ExperienceEvent中的陣列基數 | &lt;=10 | Soft | **ExperienceEvent（時間系列資料）中最佳的陣列基數為&lt;=10。** |

### 尺寸實體護欄

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 不允許非實體使用時間序列資料[!DNL XDM Individual Profile] | 0 | 硬 | **設定檔服務中的非實體不允許使用[!DNL XDM Individual Profile] 時間系列資料。** 如果時間系列資料集與非[!DNL XDM Individual Profile] ID相關聯，則不應為該資料集啟用 [!DNL Profile]。 |
| 無嵌套關係 | 0 | Soft | **您不應在兩個非結構描述之間建立關[!DNL XDM Individual Profile] 系。** 對於不屬於聯合模式的任何方案，不建議您能夠建立 [!DNL Profile] 關係。 |
| 主要ID欄位的最大JSON深度 | 4 | Soft | **主要ID欄位的建議最大JSON深度為4。** 這表示在高度嵌套的架構中，如果欄位深度超過4個級別，則不應選擇該欄位作為主ID。 位於第4個巢狀層級的欄位可用作主要ID。 |

## 資料大小護欄

以下護欄是指資料大小，建議使用，以確保資料可依預期擷取、儲存和查詢。

>[!NOTE]
>
>擷取時，資料大小會測量為JSON中的解壓縮資料。

### 主要實體護欄

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 每個描述檔片段的最大大小 | 10KB | Soft | **建議的描述檔片段大小上限為10KB。** 接收較大的描述檔片段會影響系統效能。 例如，載入大量CRM資料集（其中部分描述檔片段大小為50kB）會導致系統效能降低。 |
| 每個描述檔片段的絕對最大大小 | 1MB | 硬 | **描述檔片段的絕對最大大小為1MB。** 嘗試上傳大於1MB的描述檔片段時，擷取會失敗。 |

### 尺寸實體護欄

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 所有維圖元的最大總大小 | 5 GB   | Soft | **所有維實體的建議最大總大小為5GB。** 引入大維實體將導致系統效能降低。 例如，不建議嘗試將10GB產品目錄載入為維度實體。 |
| 每維實體模式的資料集 | 5 | Soft | **建議最多5個與每個維實體模式關聯的資料集。** 例如，如果您為「產品」建立模式並新增5個貢獻資料集，則不應建立與產品模式連結的第6個資料集。 |