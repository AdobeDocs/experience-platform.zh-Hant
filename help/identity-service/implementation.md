---
title: Identity Service實作指南
description: 瞭解提供給Adobe Experience Platform的資料在由Identity Service用於建立身分圖表之前如何進行處理。
exl-id: c961bbf6-6b46-470f-a671-93ff4173876c
source-git-commit: 4ba25ed684ff126ab1c4f1a33e6503f0342e8720
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# Identity Service實作指南

本檔案提供在Identity Service使用提供給Adobe Experience Platform的資料來建立指定客戶的身分圖表之前，如何進行處理的資訊。

## 決定身分欄位

根據您的企業資料收集策略，您標籤為身分的資料欄位將決定哪些資料包含在身分對應中。 若要發揮Experience Platform的最大效益和儘可能完整的客戶身分識別，您應同時上傳線上和離線資料。

* 線上資料是描述線上狀態和行為的資料，例如使用者名稱和電子郵件地址。

* 離線資料是指與線上狀態不直接相關的資料，例如CRM系統的ID。 這類資料可讓您的身分識別更加健全，並支援不同系統間的資料內聚力。

## 建立其他身分名稱空間

雖然Experience Platform提供各種標準名稱空間，但您可能需要建立其他名稱空間以將您的身分正確分類。 如需詳細資訊，請閱讀[為您的組織建立自訂名稱空間](./features/namespaces.md)的指南。

>[!NOTE]
>
>身分名稱空間是身分的限定詞。 因此，建立名稱空間後就無法刪除。

## 在體驗資料模型(XDM)中包含身分資料

Experience Data Model (XDM)是Experience Platform組織客戶資料的標準化架構，可讓Experience Platform和其他與Experience Platform互動的服務彼此共用和瞭解資料。 如需詳細資訊，請閱讀[XDM系統總覽](../xdm/home.md)。

記錄和時間序列結構描述都提供了包含身分資料的方法。 在擷取資料時，如果發現來自不同名稱空間的資料片段共用共同的身分資料，身分圖表會在這些資料片段之間建立新的關係。

## 將XDM欄位標示為身分

在實作記錄或時間序列XDM類別的結構描述中，型別`string`的任何欄位都可以標示為身分欄位。 因此，所有擷取至該欄位的資料都將被視為身分資料。

如果身分欄位共用常見的PII資料，則這些身分欄位也允許連結身分。
例如，透過將電話號碼欄位標示為身分欄位，Identity Service會自動繪製與其他使用相同電話號碼之個人的關係圖。

>[!NOTE]
>
>* 陣列和對應型別欄位不受支援，且無法標籤為身分欄位。
>* 在標籤欄位時，會提供所產生身分的名稱空間。
>* 只要此欄位不在陣列物件下，就可以將欄位標示為身分。

如需詳細資訊，請閱讀[在UI](../xdm/ui/fields/identity.md)中定義身分欄位的指南。

## 設定Identity服務的資料集

在串流擷取程式期間，Identity Service會自動從記錄和時間序列資料中擷取身分資料。 不過，您必須先為Identity Service啟用資料，才能擷取資料。 如需詳細資訊，請參閱有關[使用API為即時客戶設定檔和身分識別服務設定資料集](../profile/tutorials/dataset-configuration.md)的教學課程。

## 將資料內嵌至Identity Service

識別服務會使用[批次擷取](../ingestion/batch-ingestion/overview.md)或[串流擷取](../ingestion/streaming-ingestion/overview.md)傳送給Experience Platform的符合XDM規範的資料。

以下影片旨在協助您瞭解Identity Service。 此影片說明如何將資料欄位標示為身分、擷取身分識別資料，然後驗證資料是否已送入Adobe Experience Platform Identity Service私人圖表。

>[!WARNING]
>
>以下影片中顯示的Experience PlatformUI已過期。 請參閱檔案以瞭解最新的UI熒幕擷取畫面及功能。

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)
