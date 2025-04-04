---
title: Google PubSub Source概觀
description: 瞭解如何使用API或使用者介面將Google PubSub連結至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7c78173d-2639-47cb-8935-77fb7841a121
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# [!DNL Google PubSub]來源

>[!IMPORTANT]
>
>[!DNL Google PubSub]來源可在來源目錄中提供給已購買Real-Time CDP Ultimate的使用者。

Adobe Experience Platform為[!DNL AWS]、[!DNL Google Cloud Platform]和[!DNL Azure]等雲端提供者提供原生連線，可讓您將這些系統的資料帶入Experience Platform，以用於下游服務和目的地。

雲端儲存空間來源可將您的資料帶入Experience Platform，無需下載、格式化或上傳。 內嵌的資料可以格式化為XDM JSON、XDM Parquet或分隔。 流程的每個步驟都會整合到來源工作流程中。 Experience Platform可讓您即時從[!DNL Google PubSub]匯入資料。

## 先決條件 {#prerequisites}

本節概述在將[!DNL Google PubSub]帳戶連線至Experience Platform之前，必須完成的先決條件設定。

### 建立服務帳戶 {#create-service-account}

**服務帳戶**&#x200B;是應用程式或運算工作負載經常使用的帳戶型別，而不是個人。 服務帳戶由其電子郵件地址識別，該地址為該帳戶所獨有。

* 一方面，服務帳戶是&#x200B;**主參與者** — 您可以授與服務帳戶對[!DNL Google Cloud]資源的存取權。 例如，您可以在指定專案上授與服務帳戶運算管理員角色`(roles/compute.admin)`。 如此一來，服務帳戶就能在該特定專案中管理運算引擎資源。
* 另一方面，服務帳戶也是資源 — 您可以授予其他主體存取服務帳戶的許可權。 例如，您可以授與使用者服務帳戶上的服務帳戶使用者角色`(roles/iam.serviceAccountUser)`，讓使用者將該服務帳戶附加至資源。 或者，您可以授與使用者服務帳戶管理員角色`(roles/iam.serviceAccountAdmin)`，讓使用者完成檢視、編輯、停用和刪除服務帳戶等工作。

如需針對使用案例決定正確驗證型別的詳細資訊，請閱讀驗證方法](https://cloud.google.com/docs/authentication)的[[!DNL Google] 指南。

請依照下列步驟建立服務帳戶：

首先，導覽至[!DNL Google Developer Console]的[!DNL IAM]頁面，然後選取&#x200B;**[!DNL Create Service Account]**。

![Google Developer Console中的建立服務帳戶視窗](../../images/tutorials/create/google-pubsub/create-service-account.png)

接下來，輸入服務帳戶的顯示名稱和ID，然後選取&#x200B;**[!DNL Create and Continue]**。

![Google Developer Console中的服務帳戶詳細資料](../../images/tutorials/create/google-pubsub/service-account-details.png)

### 產生服務帳戶金鑰 {#generate-service-account-keys}

若要為服務帳戶產生金鑰，請在服務帳戶頁面中選取金鑰標頭。 從那裡選取&#x200B;**[!DNL Add key]**，然後從下拉式選單中選取&#x200B;**[!DNL Create new key]**。 您也可以使用此面板來上傳現有的金鑰。

![Google Developer Console中的新增金鑰視窗](../../images/tutorials/create/google-pubsub/add-key.png)

成功後，您將會收到一則訊息，指出您的電腦已儲存私密金鑰，且檔案將會下載。 然後，當您在Experience Platform上建立您的[!DNL Google PubSub]帳戶時，可以使用此檔案的內容作為認證。

### 授與主題和訂閱層級的許可權 {#grant-permissions}

若要授與主題和訂閱層級的許可權，請瀏覽至主題主控台頁面，然後選取&#x200B;**[!DNL Show info panel]**。 接著，在[!DNL Permissions]標籤下，選取[!DNL Add Principal]，然後新增服務帳戶主體與許可權。

![Google Developer Console中的快顯視窗，您可以在其中授與主題和訂閱層級的許可權](../../images/tutorials/create/google-pubsub/add-principal.png)

## 最佳[!DNL Google PubSub usage]的組態 {#optimal-configurations}

本節概述建議您在Experience Platform上最佳化[!DNL Google PubSub]來源使用方式的設定。

### 訂閱屬性 {#subscription-properties}

使用[!DNL Google Developer Console]至&#x200B;**增加您的通知期限**。 這可讓[!DNL Google Publisher]根據您設定的時間等待，然後再傳送訊息。 此延遲有助於減少訂閱者層級不必要的負載。

![Google Developer Console中的通知截止日期介面。](../../images/tutorials/create/google-pubsub/acknowledgement-deadline.png)

啟用&#x200B;**[!DNL exactly one delivery]**。 此設定會通知[!DNL Google Publisher]，保證傳送至訂閱的郵件不會在確認截止日期到期前重新傳送。 您可以使用此設定來確保確認訊息不會重新傳送至訂閱。

![Google Developer Console中只有一個傳遞設定頁面。](../../images/tutorials/create/google-pubsub/exactly-one-delivery.png)

您可以啟用&#x200B;**[!DNL Retry after exponential backoff delay]**，以降低伺服器進一步不堪重負的風險。 您可以在[!DNL Google Developer Console]中啟用此設定，以便在嘗試其他連線之前，提供系統更多的時間復原，以更好地緩解暫時性失敗（通常可自行解決的暫時性錯誤）。

![Google Developer Console中的[重試原則]視窗。](../../images/tutorials/create/google-pubsub/retry-policy.png)

您必須&#x200B;**將訂閱訊息保留期間設為24小時以上**，以確保未確認的資料不會在尖峰載入期間遺失。 此外，**啟用無效信件主題**，以確保即使在極少數邊緣案例中也不會發生資料遺失。

>[!IMPORTANT]
>
>每個[!DNL Google PubSub]訂閱只能建立一個來源資料流。 重複使用訂閱，即使在沙箱間重複使用，也會導致資料遺失。

## 將[!DNL Google PubSub]連線至Experience Platform

以下檔案提供如何使用API或使用者介面將[!DNL Google PubSub]連線至Experience Platform的資訊：

### 使用API

* [使用流量服務API建立Google PubSub來源連線](../../tutorials/api/create/cloud-storage/google-pubsub.md)
* [使用流量服務API收集串流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

* [在使用者介面中建立Google PubSub來源連線](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
* [在UI中為雲端儲存空間連線設定資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
