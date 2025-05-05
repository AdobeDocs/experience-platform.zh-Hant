---
description: 瞭解如何使用目的地測試API為您的串流目的地產生範例設定檔，以用於目的地測試。
title: 根據來源結構描述產生範例設定檔
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 1%

---


# 根據來源結構描述產生範例設定檔 {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API端點**： `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

此頁面列出並描述您可以使用`/authoring/sample-profiles` API端點執行的所有API作業。

## 為不同的API產生不同的設定檔型別 {#different-profiles-different-apis}

>[!IMPORTANT]
>
>使用此API端點可針對兩個不同的使用案例產生範例設定檔。 您可以：
>* 產生設定檔，以使用&#x200B;*目的地ID*&#x200B;做為查詢引數，在[製作及測試訊息轉換範本](create-template.md)時使用。
>* 如果您的目的地設定正確[&#128279;](streaming-destination-testing-overview.md) — 使用&#x200B;*目的地執行個體識別碼*&#x200B;作為查詢引數，產生呼叫測試時要使用的設定檔。

您可以根據Adobe XDM來源結構描述（用於測試您的目的地）或目的地支援的目標結構描述（用於製作範本）產生範例設定檔。 若要瞭解Adobe XDM來源結構描述與目標結構描述之間的差異，請閱讀[訊息格式](../../functionality/destination-server/message-format.md)文章的概述區段。

請注意，範例設定檔的使用目的不可互換。 根據&#x200B;*目的地識別碼*&#x200B;產生的設定檔只能用來製作您的訊息轉換範本，而根據&#x200B;*目的地執行個體識別碼*&#x200B;產生的設定檔只能用來測試您的目的地端點。

## 範例設定檔產生API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](../../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 根據測試目的地時使用的來源結構描述產生範例設定檔 {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>在[測試您的目的地](streaming-destination-testing-overview.md)時，將此處產生的範例設定檔新增至HTTP呼叫。

您可以根據來源結構描述產生範例設定檔，方法是向`authoring/sample-profiles/`端點發出GET要求，並提供您根據要測試的目的地組態所建立的目的地執行個體識別碼。

若要取得目的地執行個體的ID，您必須先在Experience Platform UI中建立與目的地的連線，才能嘗試測試目的地。 閱讀[啟用目的地教學課程](../../../ui/activation-overview.md)，並參閱下列秘訣，瞭解如何取得目的地執行個體識別碼以用於此API。

>[!IMPORTANT]
>
>* 若要使用此API，您在Experience Platform UI中必須有與目的地的現有連線。 閱讀[連線到目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)以及[啟用設定檔和對象到目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html)以取得詳細資訊。
> * 建立與目的地的連線後，在[瀏覽與目的地的連線時](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html)，取得您應該用於此端點之API呼叫中的目的地執行個體識別碼。
>![UI影像如何取得目的地執行個體識別碼](../../assets/testing-api/get-destination-instance-id.png)

**API格式**

```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| 查詢引數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 要根據目的地執行個體的ID產生範例設定檔。 |
| `{COUNT}` | *選擇性*。 您正在產生的範例設定檔數目。 引數可以取用`1 - 1000`之間的值。 <br>如果未指定count引數，則預設產生的設定檔數目由[目的地伺服器組態](../../authoring-api/destination-server/create-destination-server.md)中的`maxUsersPerRequest`值決定。 如果此屬性未定義，則Adobe將產生一個範例設定檔。 |

{style="table-layout:auto"}


**要求**

下列要求會產生範例設定檔，由`{DESTINATION_INSTANCE_ID}`和`{COUNT}`查詢引數設定。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定數量的範例設定檔，以及與來源XDM結構描述對應的對象成員資格、身分和設定檔屬性。

>[!TIP]
>
> 回應只會傳回目標例項中使用的對象成員資格、身分和設定檔屬性。 即使您的來源結構描述有其他欄位，這些欄位仍會被忽略。

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| 屬性 | 說明 |
| -------- | ----------- |
| `segmentMembership` | 說明個人對象會籍的地圖物件。 如需`segmentMembership`的詳細資訊，請閱讀[對象成員資格詳細資料](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html)。 |
| `lastQualificationTime` | 此設定檔上次符合區段資格的時間戳記。 |
| `xdm:status` | 字串欄位，指出是否已在目前請求中實現對象成員資格。 接受下列值： <ul><li>`realized`：設定檔是區段的一部分。</li><li>`exited`：設定檔正在退出對象，做為目前請求的一部分。</li></ul> |
| `identityMap` | 描述個人各種身分值及其相關名稱空間的對應型別欄位。 如需`identityMap`的詳細資訊，請閱讀[結構描述組合的基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#identityMap)。 |

{style="table-layout:auto"}

## 根據建立訊息轉換範本時使用的目標結構描述產生範例設定檔 {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>在[轉譯範本步驟](render-template-api.md#multiple-profiles-with-body)中，使用製作範本時此處產生的範例設定檔。

您可以根據目標結構描述產生範例設定檔，向`authoring/sample-profiles/`端點發出GET請求，並提供目的地組態的目的地ID （您正在根據此ID建立範本）。

>[!TIP]
>
>* 您應在此使用的目的地ID是與使用`/destinations`端點建立的目的地組態相對應的`instanceId`。 如需詳細資訊，請參閱[擷取目的地組態](../../authoring-api/destination-configuration/retrieve-destination-configuration.md)。

**API格式**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| 查詢引數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 要根據目的地組態的ID產生範例設定檔。 |
| `{COUNT}` | *選擇性*。 您正在產生的範例設定檔數目。 引數可以取用`1 - 1000`之間的值。 <br>如果未指定count引數，則預設產生的設定檔數目由[目的地伺服器組態](../../authoring-api/destination-server/create-destination-server.md)中的`maxUsersPerRequest`值決定。 如果此屬性未定義，則Adobe將產生一個範例設定檔。 |

{style="table-layout:auto"}

**要求**

下列要求會產生範例設定檔，由`{DESTINATION_ID}`和`{COUNT}`查詢引數設定。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定數量的範例設定檔，以及與目標XDM結構描述相對應的對象成員資格、身分和設定檔屬性。

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## API錯誤處理 {#api-error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道如何產生範例設定檔，以便在[測試訊息轉換範本](create-template.md)或[測試目的地是否正確設定](streaming-destination-testing-overview.md)時使用。
