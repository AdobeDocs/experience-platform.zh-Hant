---
title: Flexible Audience Evaluation Guide
description: 瞭解如何使用彈性的對象評估，以應要求執行批次細分工作。
role: Developer, User
exl-id: b85bf735-be02-4bf7-bd63-8d74ae905e58
source-git-commit: 518afcfaabb9867452dc6ee94bef103ec167da78
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 5%

---

# 彈性的對象評估指南

>[!AVAILABILITY]
>
>彈性的對象評估僅&#x200B;**在**&#x200B;上執行的Experience Platform執行個體上提供[!DNL Microsoft Azure]。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../landing/multi-cloud.md)。
>
>Additionally, flexible audience evaluation is **only** available for use with Real-Time CDP B2C Edition.

Flexible audience evaluation lets you run a batch segmentation job on demand. With flexible audience evaluation, you can run ad-hoc campaign launches, just-in-time communications, or other time-sensitive activities.

## 護欄 {#guardrails}

>[!CONTEXTUALHELP]
>id="platform_segmentation_browse_flexibleaudienceevaluation"
>title="彈性對象評估限制"
>abstract="您可以在單一彈性對象評估執行中評估最多 20 個對象。<br/><br/>此外，雖然評估工作會盡快執行，但可能會出現系統延遲，因為隨選評估<b>無法</b>與另一個隨選或批次評估同時執行。"

當您執行彈性的對象評估時，請記住以下條件：

- 每個沙箱每天只能使用彈性對象評估&#x200B;**兩次**。 此限制會在午夜(UTC)重設。
- 每年&#x200B;**生產**&#x200B;沙箱有&#x200B;**最多**&#x200B;個靈活的受眾評估運行，共50個。
   - 年定義為從Experience Platform合同日期開始的一年，以便靈活評估受眾。 例如，如果您在5月18日開始簽訂合同，則每年5月18日，您的靈活受眾評估運行數將重置。
- 您每&#x200B;**開發**&#x200B;沙箱每年有&#x200B;**最多**&#x200B;次100次彈性對象評估執行。
   - 一年是指從您的Experience Platform合約日期開始的一年，用於彈性對象評估。 例如，如果您從5月18日開始合約，您彈性的對象評估執行次數將會在每年5月18日重設。
- 所有對象&#x200B;**都必須**&#x200B;具有「分段服務」的來源。
- 所有對象&#x200B;**都必須**&#x200B;使用批次細分進行評估。
- 所有對象&#x200B;**都必須**&#x200B;是以人物為基礎的對象。
- You can only select a maximum of 20 audiences per flexible audience evaluation run.

>[!NOTE]
>
>You can purchase additional flexible audience evaluation runs per year. For more information, contact Adobe Customer Care.

## 存取權 {#access}

若要使用彈性的對象評估，您必須具備下列許可權：

- **[!UICONTROL Evaluate Segment to an Audience]**&#x200B;區段下的&#x200B;**[!DNL Profile Management]**。

For more information on role-based access control, please read the [access control overview](../../access-control/home.md).

## Running flexible audience evaluation

You can run flexible audience evaluation by using either the Experience Platform APIs or UI.

>[!BEGINTABS]

>[!TAB Experience Platform APIs]

To run flexible audience evaluation within the Experience Platform APIs, you&#39;ll need to create a segment job that contains the IDs of all the segment definitions (audiences) you want to evaluate.

>[!NOTE]
>
>You can only add a **maximum** of 20 segment definition IDs per segment job API call.

您可以對`/segment/jobs`端點發出POST要求，並在要求內文中包含區段定義的ID，藉此建立新的區段作業。

+++建立新區段作業的範例請求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    },
    {
        "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85"
    }
 ]'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `segmentId` | 要計算的段定義的ID。 這些段定義可以屬於不同的合併策略。 |

+++

成功的回應會傳回HTTP狀態200，其中包含您新建立區段作業的相關資訊。

+++ 建立新區段作業時的範例回應。

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

+++

建立區段作業後，您可以透過向`/segment/jobs`端點發出GET請求來檢查其狀態，在請求路徑中提供您新建立的區段作業的識別碼。

+++擷取區段作業的範例請求

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

成功的回應會傳回HTTP狀態200，其中包含指定區段工作的詳細資訊。


+++ A sample response for retrieving a segment job.

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

+++

>[!TAB Experience Platform UI]

若要在Experience Platform UI中執行彈性的對象評估，請在&#x200B;**[!UICONTROL Audiences]**&#x200B;區段中選取&#x200B;**[!UICONTROL Customers]**。

![「客戶」區段內的「對象」按鈕會醒目提示。 顯示客戶設定檔的對象入口網站。](../images/methods/fae/audience-portal.png)

隨即顯示「對象入口網站」，顯示組織內所有人員對象的清單。 在Audience Portal中，您可以選擇要評估的對象並選取&#x200B;**[!UICONTROL Evaluate audience]**。

![您想要使用彈性對象評估的對象已選取。](../images/methods/fae/evaluate-audiences.png)

「**[!UICONTROL Evaluate audiences on demand]**」彈出視窗隨即顯示，顯示將使用隨選區段作業評估的對象清單。 如果對象不符合依需求評估的資格，系統會自動將其從評估工作中移除。 確認列出的對象是您想要評估的對象。

![顯示可以使用彈性對象評估來評估的對象。](../images/methods/fae/evaluate-audiences-modal.png)

在確認列出了正確的受眾後，您可以繼續請求，並開始靈活的受眾評估。 您可以在[評估作業監視視圖](../../dataflows/ui/monitor-audiences.md#evaluation-job-details)中查看此訪問群體評估的狀態。

>[!NOTE]
>
>區段工作的狀態可能會在監視控制面板中報告為「已排入佇列」狀態。 您可以透過向`/segment/jobs`端點發出GET請求，在請求路徑中提供區段作業的ID，來檢視區段作業的最新狀態。 您可以在API標籤中找到有關使用此端點的更多資訊。
>
>如果您執行彈性對象評估，並希望評估將對象啟用到目的地，您必須確保頻率設定為&#x200B;**[!UICONTROL After segment evaluation]**。 針對已設定在區段評估[後啟動](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files)的受眾執行彈性受眾評估，將會在彈性受眾評估工作完成後立即啟動受眾，無論之前是否有任何每日啟動工作。

>[!ENDTABS]

## 影片 {#video}

下列影片示範如何在Experience Platform中存取和使用彈性的對象評估。

>[!VIDEO](https://video.tv.adobe.com/v/3453651?captions=chi_hant&)

## 常見問題 {#faq}

The following section lists frequently asked questions related to flexible audience evaluation.

### How soon can I activate an audience using flexible audience evaluation?

+++ 回答

您可以在對象建立後，立即使用彈性的對象評估來啟用對象。

+++

### How long does flexible audience evaluation take?

+++ 回答

A flexible audience evaluation job can take up to four hours to complete.

+++

### Can I run scheduling with flexible audience evaluation?

+++ 回答

No, scheduling is not available to use with flexible audience evaluation.

+++

### 使用彈性的對象評估時，是否需要執行額外的匯出工作？

+++ 回答

否，匯出作業會在相應的區段作業完成後自動執行。

+++

### 我可以使用靈活的受眾評估評估來評估哪些服務？

+++ 回答

您可以在所有的下游服務（包括目的地和Adobe Journey Optimizer歷程）中使用對象。

+++

### 彈性的對象評估限制何時會重設？

+++ 回答

每日限制會在午夜(UTC)重設。 年度限制會在合約的週年日重設。

+++

### 有彈性的對象評估支援哪些型別的對象？

+++ 回答

Only audiences with the origin of Segmentation Service are supported for flexible audience evaluation. Other audiences, such as compositions, custom upload, or Data Distiller, are not supported for flexible audience evaluation.

+++

### 哪些回合對我的彈性受眾評估回合計數有貢獻？

+++ 回答

使用API或UI建立的彈性受眾評估執行接近上限。 不過，每晚執行的每日批次細分工作不會&#x200B;**對**&#x200B;這個限制有貢獻。

+++

### Do I need to evaluate all dependent audiences when evaluating the main audience with flexible audience evaluation?

+++ 回答

不可以。 Flexible audience evaluation will automatically evaluate all dependent audiences. For example, if Audience A depends on Audience B, you only need to evaluate Audience B. Flexible audience evaluation will automatically evaluate Audience A and then Audience B.

+++
