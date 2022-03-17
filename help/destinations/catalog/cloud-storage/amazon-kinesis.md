---
keywords: AmazonKinesis;kinesis目標；kinesis
title: AmazonKinesis
description: 建立到AmazonKinesis儲存的即時出站連接，以從Adobe Experience Platform流資料。
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 1%

---

# (Beta) [!DNL Amazon Kinesis] 連接

## 總覽 {#overview}

>[!IMPORTANT]
>
>的 [!DNL Amazon Kinesis] 平台中的目標當前處於beta中。 文件和功能可能會有所變更。

的 [!DNL Kinesis Data Streams] 服務 [!DNL Amazon Web Services] 允許您即時收集和處理大量資料記錄。

您可以建立到您的 [!DNL Amazon Kinesis] 儲存以從Adobe Experience Platform傳輸資料。

* 有關 [!DNL Amazon Kinesis]，請參見 [Amazon文檔](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)。
* 連接到 [!DNL Amazon Kinesis] 以寫程式方式，請參見 [流目標API教程](../../api/streaming-destinations.md)。
* 連接到 [!DNL Amazon Kinesis] 使用平台用戶介面，請參閱以下各節。

![AmazonKinesis在用戶介面](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## 使用案例 {#use-cases}

使用流目標，如 [!DNL Amazon Kinesis]，您可以輕鬆地將高價值分段事件和關聯的配置檔案屬性輸入到您選擇的系統中。

例如，潛在客戶下載了一份白皮書，確認他們屬於「高傾向轉換」段。 通過映射目標客戶所在的段 [!DNL Amazon Kinesis] 目標，您將在 [!DNL Amazon Kinesis]。 在這裡，您可以採用自行動手的方法，並在活動之前描述業務邏輯，因為您認為最適合您的企業IT系統。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style=&quot;table-layout:auto&quot;}

## 必需 [!DNL Amazon Kinesis] 權限 {#required-kinesis-permission}

要成功將資料連接和導出到 [!DNL Amazon Kinesis] 流，Experience Platform需要以下操作的權限：

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

這些權限通過 [!DNL Kinesis] 在平台用戶介面中配置Kinesis目標後，平台將檢查控制台。

下面的示例顯示成功將資料導出到 [!DNL Kinesis] 目標。

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `kinesis:ListStreams` | 列出您的AmazonKinesis資料流的操作。 |
| `kinesis:PutRecord` | 將單個資料記錄寫入Kinesis資料流的操作。 |
| `kinesis:PutRecords` | 在單個調用中將多個資料記錄寫入Kinesis資料流的操作。 |

有關控制訪問的詳細資訊 [!DNL Kinesis] 資料流，讀取以下內容 [[!DNL Kinesis] 文檔](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)。

## 連接到目標 {#connect}

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!DNL Amazon Web Services]訪問密鑰和密鑰**:在 [!DNL Amazon Web Services]，生成 `access key - secret access key` 對以授予您的平台訪問權 [!DNL Amazon Kinesis] 帳戶。 在 [Amazon Web Services文檔](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。
* **區域**:指明 [!DNL Amazon Web Services] 要將資料流到的區域。
* **名稱**:提供與 [!DNL Amazon Kinesis]
* **說明**:提供與 [!DNL Amazon Kinesis]。
* **流**:提供您的 [!DNL Amazon Kinesis] 帳戶。 平台會將資料導出到此流。

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 將段激活到此目標 {#activate}

請參閱 [激活受眾資料以流式處理配置檔案導出目標](../../ui/activate-streaming-profile-destinations.md) 有關激活此目標受眾段的說明。

## 配置檔案導出行為 {#profile-export-behavior}

Experience Platform優化配置檔案導出行為 [!DNL Amazon Kinesis] 目標：僅當在段鑑定或其他重要事件之後對配置檔案進行了相關更新時，才將資料導出到目標。 配置式在以下情況下導出到目標：

* 配置檔案更新由映射到目的地的至少一個段的段成員資格的改變確定。 例如，配置檔案已限定映射到目標的段之一或已退出映射到目標的段之一。
* 配置檔案更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md)。 例如，已為映射到目標的段之一限定的配置檔案已在標識映射屬性中添加了新標識。
* 配置檔案更新由映射到目的地的至少一個屬性的屬性的改變確定。 例如，映射步驟中映射到目標的屬性之一被添加到配置檔案。

在上述所有情況下，只將發生相關更新的配置檔案導出到目標。 例如，如果映射到目標流的段有100個成員，並且有5個新配置檔案符合該段的條件，則向目標的導出是增量的，並且只包括5個新配置檔案。

請注意，無論更改位於何處，都會為配置檔案導出所有映射的屬性。 因此，在上面的示例中，即使屬性本身沒有更改，也會導出這五個新配置檔案的所有映射屬性。

### 什麼決定資料導出以及導出中包含的內容 {#what-determines-export-what-is-included}

對於為給定配置檔案導出的資料，瞭解以下兩個不同概念非常重要 *決定將資料導出到 [!DNL Amazon Kinesis] 目標* 和 *資料包含在導出中*。

| 決定目標導出的因素 | 目標導出中包含的內容 |
|---------|----------|
| <ul><li>映射的屬性和段用作目標導出的提示。 這意味著，如果任何映射段更改狀態（從null更改為已實現或從已實現/現有更新為退出）或任何映射屬性被更新，則將啟動目標導出。</li><li>由於標識當前無法映射到 [!DNL Amazon Kinesis] 目標，給定配置檔案上任何身份的更改也會決定目標導出。</li><li>屬性的更改定義為屬性上的任何更新，無論其值是否相同。 這意味著，即使值本身未更改，屬性上的覆蓋也被視為更改。</li></ul> | <ul><li>所有段（具有最新成員身份狀態）都包含在 `segmentMembership` 的雙曲餘切值。</li><li>中的所有標識 `identityMap` 也包括對象(Experience Platform當前不支援在 [!DNL Amazon Kinesis] 目標)。</li><li>目標導出中只包含映射的屬性。</li></ul> |

{style=&quot;table-layout:fixed&quot;

例如，將此資料流視為 [!DNL Amazon Kinesis] 目標，其中在資料流中選擇了三個段，並將四個屬性映射到目標。

![AmazonKinesis目標資料流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

導出到目標的配置檔案可由符合或退出其中一個配置檔案來確定 *三個映射段*。 但是，在資料導出中，在 `segmentMembership` 對象（請參見） [導出的資料](#exported-data) )中，如果特定配置檔案是其成員，則可能會顯示其他未映射的段。 如果配置檔案符合DeLorean Cars分部客戶的資格，但也是受觀看的「回到未來」電影和科幻片迷分部的成員，則另外兩個分部也將出現在 `segmentMembership` 資料導出的對象，即使這些對象未映射到資料流中。

從配置檔案屬性的視點來看，對上述四個屬性的任何更改都將確定目標導出，並且配置檔案上存在的四個映射屬性中的任何一個都將出現在資料導出中。

## 導出的資料 {#exported-data}

已導出 [!DNL Experience Platform] 資料到達 [!DNL Amazon Kinesis] JSON格式的目標。 例如，下面的導出包含符合特定段條件的配置檔案，是另兩個段的成員，並退出另一個段。 導出還包括配置檔案屬性的名字、姓氏、出生日期和個人電子郵件地址。 此配置檔案的標識為ECID和電子郵件。

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

>[!MORELIKETHIS]
>
>* [連接到AmazonKinesis，並使用流服務API激活資料](../../api/streaming-destinations.md)
>* [Azure事件中心目標](./azure-event-hubs.md)
>* [目標類型和類別](../../destination-types.md)

