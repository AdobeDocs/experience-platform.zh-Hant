---
title: 彈性的對象評估指南
description: 瞭解如何使用彈性的對象評估，以應要求執行批次細分工作。
role: Developer, User
exl-id: b85bf735-be02-4bf7-bd63-8d74ae905e58
source-git-commit: 7a0a98ea035892943a0e9a9a2b059701f6f1f612
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 5%

---

# 彈性的對象評估指南

>[!AVAILABILITY]
>
>彈性的對象評估僅&#x200B;**在[!DNL Microsoft Azure]上執行的Experience Platform執行個體上提供**。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../landing/multi-cloud.md)。
>
>此外，彈性的對象評估僅&#x200B;**可**&#x200B;搭配Real-Time CDP B2C Edition使用。

彈性的對象評估可讓您視需求執行批次細分工作。 透過彈性的對象評估，您可以執行臨機行銷活動啟動、即時通訊或其他時效性活動。

## 護欄 {#guardrails}

>[!CONTEXTUALHELP]
>id="platform_segmentation_browse_flexibleaudienceevaluation"
>title="彈性對象評估限制"
>abstract="您可以在單一彈性對象評估執行中評估最多 20 個對象。<br/><br/>此外，雖然評估工作會盡快執行，但可能會出現系統延遲，因為隨選評估<b>無法</b>與另一個隨選或批次評估同時執行。"

當您執行彈性的對象評估時，請記住以下條件：

- 每個沙箱每天只能使用彈性對象評估&#x200B;**兩次**。 此限制會在午夜(UTC)重設。
- 您每&#x200B;**生產**&#x200B;沙箱每年有&#x200B;**最多**&#x200B;次50次彈性對象評估執行。
- 您每&#x200B;**開發**&#x200B;沙箱每年有&#x200B;**最多**&#x200B;次100次彈性對象評估執行。
- 所有對象&#x200B;**都必須**&#x200B;具有「分段服務」的來源。
- 所有對象&#x200B;**都必須**&#x200B;使用批次細分進行評估。
- 所有對象&#x200B;**都必須**&#x200B;是以人物為基礎的對象。
- 每個彈性受眾評估回合最多只能選取20個受眾。

>[!NOTE]
>
>您可以每年購買額外的彈性受眾評估回合。 如需詳細資訊，請聯絡Adobe客戶服務。

## 存取 {#access}

若要使用彈性的對象評估，您必須具備下列許可權：

- **[!UICONTROL 評估區段給&#x200B;**&#x200B;[!DNL Profile Management]&#x200B;**區段下的對象]**。

如需角色型存取控制的詳細資訊，請閱讀[存取控制總覽](../../access-control/home.md)。

## 執行彈性的對象評估

您可以使用Experience Platform API或UI來執行彈性的對象評估。

>[!BEGINTABS]

>[!TAB Experience Platform API]

若要在Experience Platform API內執行彈性的對象評估，您必須建立區段作業，其中包含您要評估的所有區段定義（對象）的ID。

>[!NOTE]
>
>您只能為每個區段作業API呼叫新增&#x200B;**最多**&#x200B;個20個區段定義ID。

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
| `segmentId` | 您要評估之區段定義的ID。 這些區段定義可屬於不同的合併原則。 |

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


+++ 擷取區段作業的範例回應。

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

若要在Experience Platform UI中執行彈性的對象評估，請在&#x200B;**[!UICONTROL 客戶]**&#x200B;區段中選取&#x200B;**[!UICONTROL 對象]**。

![「客戶」區段內的「對象」按鈕會醒目提示。 顯示客戶設定檔的對象入口網站。](../images/methods/fae/audience-portal.png)

隨即顯示「對象入口網站」，顯示組織內所有人員對象的清單。 在對象入口網站中，您可以選擇要評估的對象，並選取&#x200B;**[!UICONTROL 評估對象]**。

![您想要使用彈性對象評估的對象已選取。](../images/methods/fae/evaluate-audiences.png)

**[!UICONTROL 依需求評估對象]**&#x200B;彈出視窗會出現，顯示將使用依需求區段工作評估的對象清單。 如果對象不符合依需求評估的資格，系統會自動將其從評估工作中移除。 確認列出的對象是您想要評估的對象。

![顯示可以使用彈性對象評估來評估的對象。](../images/methods/fae/evaluate-audiences-modal.png)

確認列出正確的對象後，您可以繼續處理請求，並展開彈性的對象評估。 您可以在[評估工作監視檢視](../../dataflows/ui/monitor-audiences.md#evaluation-job-details)中檢視此對象評估的狀態。

>[!NOTE]
>
>區段工作的狀態可能會在監視控制面板中報告為「已排入佇列」狀態。 您可以透過向`/segment/jobs`端點發出GET請求，在請求路徑中提供區段作業的ID，來檢視區段作業的最新狀態。 您可以在API標籤中找到有關使用此端點的更多資訊。
>
>如果您執行彈性對象評估，並希望評估將對象啟用到目的地，您必須確保頻率設定為&#x200B;**[!UICONTROL 區段評估後]**。 針對已設定在區段評估[&#128279;](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files)後啟動的受眾執行彈性受眾評估，將會在彈性受眾評估工作完成後立即啟動受眾，無論之前是否有任何每日啟動工作。

>[!ENDTABS]

## 影片 {#video}

下列影片示範如何在Experience Platform中存取和使用彈性的對象評估。

>[!VIDEO](https://video.tv.adobe.com/v/3453651?&captions=chi_hant)

## 常見問題 {#faq}

下節列出與彈性對象評估相關的常見問題。

### 我多久才能使用彈性的對象評估來啟用對象？

+++ 回答

您可以在對象建立後，立即使用彈性的對象評估來啟用對象。

+++

### 彈性的對象評估需要多久時間？

+++ 回答

彈性的對象評估工作最多可能需要四個小時才能完成。

+++

### 我是否可透過彈性的對象評估執行排程？

+++ 回答

否，排程不適用於彈性的對象評估。

+++

### 使用彈性的對象評估時，是否需要執行額外的匯出工作？

+++ 回答

否，匯出作業會在相應的區段作業完成後自動執行。

+++

### 我可以使用透過彈性對象評估來評估的對象嗎？

+++ 回答

您可以在所有的下游服務(包括目的地和Adobe Journey Optimizer歷程)中使用對象。

+++

### 彈性的對象評估限制何時會重設？

+++ 回答

每日限制會在午夜(UTC)重設。 年度限制會在合約的週年日重設。

+++

### 有彈性的對象評估支援哪些型別的對象？

+++ 回答

只有具有細分服務來源的受眾才支援進行彈性的受眾評估。 其他對象，例如組合、自訂上傳或資料Distiller，不支援彈性對象評估。

+++

### 哪些回合對我的彈性受眾評估回合計數有貢獻？

+++ 回答

使用API或UI建立的彈性受眾評估執行接近上限。 不過，每晚執行的每日批次細分工作不會&#x200B;**對**&#x200B;這個限制有貢獻。

+++

### 使用彈性的對象評估來評估主要對象時，是否需要評估所有相依對象？

+++ 回答

不可以。 彈性的對象評估會自動評估所有相依對象。 例如，如果對象A相依於對象B，您只需要評估對象B。彈性的對象評估會自動評估對象A，然後評估對象B。

+++
