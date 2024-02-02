---
title: 檔案式雲端儲存目的地的IP位址允許清單
type: Documentation
description: 此頁面提供您可新增至允許清單的IP範圍，以便安全地從Experience Platform將資料匯出至雲端儲存空間目的地。
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 1d8ba11b1043fa68bf3c0205e8cecc2de8910234
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 1%

---

# 檔案式雲端儲存目的地的IP位址允許清單 {#ip-address-allow-list-cloud-storage}

>[!IMPORTANT]
>
> * Adobe建議您將此頁面加入書籤，每三個月重新造訪一次，以檢查最新IP位址。 Adobe不提供新IP範圍的通知。
> * 雖然Adobe支援將資料匯出至SFTP伺服器，但建議匯出資料的雲端儲存位置為 [!DNL Amazon S3] 和 [!DNL Azure Blob].

## 適用性 {#applicability}

此頁面上的IP範圍資訊會套用至目的地目錄中的下列檔案型雲端儲存聯結器：

* [[!UICONTROL Amazon S3]](./amazon-s3.md)
* [[!UICONTROL Google雲端儲存空間]](google-cloud-storage.md)
* [SFTP](./sftp.md)

>[!IMPORTANT]
>
>本頁記錄的IP範圍包括 *非* 支援以下檔案式雲端儲存空間目的地： [!UICONTROL Azure Blob]， [!UICONTROL Azure Data Lake Storage Gen2] 和 [!UICONTROL 資料登陸區域].

## 概觀 {#overview}

此頁面提供IP範圍，您可將其新增至允許清單，以安全地從Experience Platform匯出資料至數個雲端儲存空間目的地。

您可以透過網路防火牆定義網路存取控制。 透過指定適當的IP範圍，您可以允許資料傳輸服務的流量。

Adobe建議在使用雲端儲存空間目的地連線之前，將下列IP範圍新增至允許清單。 使用雲端儲存空間目的地連線時，如果無法將您區域專屬的IP範圍新增至允許清單，可能會導致錯誤或效能不佳。

## 所有客戶均需要 {#all-customers}

* `52.247.108.70`

## 美國客戶 {#us-customers}

* `52.252.71.64/29`

## 加拿大客戶 {#canada-customers}

* `20.220.135.16/29`

## EMEA客戶 {#emea-customers}

* `51.137.8.208/29`

## 英國客戶 {#uk-customers}

* `20.26.133.96/29`

## APAC客戶 {#apac-customers}

* `20.53.201.168/29`
