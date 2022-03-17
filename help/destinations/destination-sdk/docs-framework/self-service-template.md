---
title: 文檔自助模板//替換為目標名稱
description: 使用此模板可在Adobe Experience Platform目錄中為目標建立公共文檔。//替換為「概述」部分中的段落
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 2%

---

# 您的目標 {#your-destination}

*在完成此模板時，替換或刪除斜體中的所有段落（從此段開始）。*

*首先更新頁面頂部的元資料（標題和說明）。 請忽略此頁上UICONTROL的所有實例。 這是一個標籤，它幫助我們的機器翻譯流程將頁面正確翻譯成我們支援的多種語言。 在您提交文檔後，我們將向其添加標籤。*

## 總覽 {#overview}

*為您的公司提供簡短的概述，包括它為客戶提供的價值。 包括指向產品文檔首頁的連結，以供進一步閱讀。*

>[!IMPORTANT]
>
>此文檔頁面由 *您的目標* 團隊。 如有任何查詢或更新請求，請直接聯繫他們，地址為： *插入連結或電子郵件地址，可以在其中獲取更新*

## 先決條件 {#prerequisites}

*在本節中添加有關客戶在開始在Adobe Experience Platform用戶介面中設定目標之前需要瞭解的任何資訊。 這可以是：*

* *需要添加到允許清單*
* *電子郵件散列要求*
* *任何有關您的帳戶的詳細資訊*
* *如何獲取API密鑰以連接到您的平台*

*如果對客戶有用，您可以連結到相關文檔。*

## 支援的身份 {#supported-identities}

*在本節中添加有關目標支援的標識的資訊。 我們用一些標準值預填了表。 刪除不適用於目標的值和未預填充的任何值。*

*您的目標* 支援激活下表中描述的身份。 瞭解有關 [身份](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當源標識為GAID命名空間時，選擇GAID目標標識。 |
| IDFA | Apple廣告商ID | 當源標識為IDFA命名空間時，選擇IDFA目標標識。 |
| ECID | Experience Cloud ID | 表示ECID的命名空間。 以下別名也可以引用此命名空間：&quot;Adobe Marketing CloudID&quot;,&quot;Adobe Experience CloudID&quot;,&quot;Adobe Experience PlatformID&quot; 請參閱以下文檔 [ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html) 的子菜單。 |
| phone_sha256 | 使用SHA256算法散列的電話號碼 | 純文字檔案和SHA256散列電話號碼都受Adobe Experience Platform支援。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |
| email_lc_sha256 | 使用SHA256算法散列的電子郵件地址 | 純文字檔案和SHA256散列電子郵件地址都受Adobe Experience Platform支援。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |
| 外部ID | 自定義用戶ID | 如果源標識是自定義命名空間，請選擇此目標標識。 |

{style=&quot;table-layout:auto&quot;}

## 導出類型和頻率 {#export-type-frequency}

*在表中，僅保留與目標對應的行。 您應該有一行表示「導出」類型，一行表示「導出」頻率。 刪除不適用於目標的值。*

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中使用的標識符（名稱、電話號碼或其他） *您的目標* 目標。 |
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |
| 導出頻率 | **[!UICONTROL 批]** | 批處理目標將檔案以3、6、8、12或24小時的增量導出到下游平台。 閱讀有關 [基於批檔案的目標](/help/destinations/destination-types.md#file-based)。 |

{style=&quot;table-layout:auto&quot;&quot;

## 使用案例 {#use-cases}

幫助您更好地瞭解您應如何以及何時使用 *您的目標* 目的地，以下是Adobe Experience Platform客戶可通過使用此目的地解決的示例使用案例。

### 用例#1

*對於移動消息平台：*

*一個房屋租賃和銷售平台希望將移動通知推送給客戶的Android和iOS設備，讓他們知道，在他們之前搜索的租房區域，有100個更新的房源。*

### 用例#2

*對於社交網路平台：*

*一個運動服裝品牌希望通過社交媒體賬戶接觸現有客戶。 服裝品牌可以將自己的CRM中的電子郵件地址發送到Adobe Experience Platform，從自己的離線資料構建資料段，並將這些資料段發送到YOURDESTINATION，以在客戶的社交媒體源中顯示廣告。*

## 連接到目標 {#connect}

要連接到此目標，請按照 [目標配置教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)。

### 連接參數 {#parameters}

同時 [設定](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) 此目標，必須提供以下資訊：

*添加配置新目標時客戶必須填寫的欄位。 這些欄位是特定於目標的，取決於您在Destination SDK中的配置。 目標的欄位可能與下面列出的欄位不同。*

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 帳戶ID]**:您 *您的目標* 帳戶ID。


<!--

*Replace YOURDESTINATION with your destination name and TOBEFILLEDIN with the category that your destination belongs to.*

1. In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scroll to the ***TOBEFILLEDIN*** category. Select ***YOURDESTINATION***, then select **[!UICONTROL Configure]**.


    >[!NOTE]
    >
    >If a connection with this destination already exists, you can see an **[!UICONTROL Activate]** button on the destination card. For more information about the difference between **[!UICONTROL Activate]** and **[!UICONTROL Configure]**, refer to the [Catalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destinations-workspace.html#catalog) section of the destination workspace documentation.  

    ![Connect to YOURDESTINATION](./assets/yourdestination1.png)

2. In the **Account** step, if you had previously set up a connection to your *YOURDESTINATION* destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to *YOURDESTINATION*. Select **[!UICONTROL Connect to destination]** to log in and connect Adobe Experience Cloud to your *YOURDESTINATION* account.

    >[!NOTE]
    >
    >Adobe Experience Platform supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your ***YOURDESTINATION*** account. This ensures that you don't complete the workflow with incorrect credentials.

3. Once your credentials are confirmed and Adobe Experience Cloud is connected to your ***YOURDESTINATION*** account, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

4. In the **[!UICONTROL Authentication]** step, enter a **[!UICONTROL Name]** and a **[!UICONTROL Description]** for your activation flow and fill your account ID. <br> Also in this step, you can select any marketing action that should apply to this destination. Marketing actions indicate the intent for which data will be exported to the destination. You can select from Adobe-defined marketing actions or you can create your own marketing action. For more information about marketing actions, see the [Data usage policies overview](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html).

    ![Connect to YOURDESTINATION](./assets/yourdestination2.png)

5. Your destination is now created. You can select **[!UICONTROL Save & Exit]** if you want to activate segments later on or you can select **[!UICONTROL Next]** to continue the workflow and select segments to activate. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow.

-->

## 將段激活到此目標 {#activate}

閱讀 [激活配置檔案和段以流式處理段導出目標](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) 有關激活此目標受眾段的說明。

<!--

To activate segments to *YOURDESTINATION*, follow the steps below: 

1. In **[!UICONTROL Destinations > Browse]**, select the *YOURDESTINATION* destination where you want to activate your segments.

2. Click the name of the destination. This takes you to the Activate flow.
    ![activate-flow](./assets/yourdestination3.png)
    Note that if an activation flow already exists for a destination, you can see the segments that are currently being sent to the destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.
3. Select **[!UICONTROL Activate]**;
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to *YOURDESTINATION*.
    ![segments-to-destination](./assets/activate-segments-google-customer-match.png)
5.  In the **[!UICONTROL Mapping]** step, select which attributes and identities from the source XDM schema to map to the target schema. Select **[!UICONTROL Add new mapping]** and browse your schema, select identity namespaces and map them to the corresponding target identity.  
![identity mapping initial screen](./assets/gcm-identity-mapping.png) <br>&nbsp;
   *Plain text email address as primary identity*: If you have plain text (unhashed) email addresses as primary identity in your schema, select the email field in your **[!UICONTROL Source Attributes]** and map to the Email field in the right column under **[!UICONTROL Target Identities]**, as shown below. Set up a mapping between any other attributes you plan to use.
   ![identity mapping step](./assets/ssd-template-identity.png) <br>&nbsp;
6. On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination.
7. On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

>[!IMPORTANT]
>
>In this step, Adobe Experience Platform checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. For information on how to resolve policy violations, see [Policy enforcement](https://experienceleague.adobe.com/docs/experience-platform/data-governance/enforcement/auto-enforcement.html#enforcement) in the data governance documentation section.
 
![confirm-selection](./assets/data-policy-violation.png)

If no policy violations have been detected, select **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](./assets/gcm-review.png)

-->

## 導出的資料 {#exported-data}

*添加有關如何將資料導出到目標的說明。 這將幫助客戶確保他們已正確整合到您的目標。 例如，您可以提供類似於下面的JSON示例。*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
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

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。

## 其他資源 {#additional-resources}

*您可以提供產品文檔或您認為對客戶成功非常重要的任何其他資源的進一步連結。*
