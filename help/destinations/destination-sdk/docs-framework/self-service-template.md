---
title: 檔案自助服務範本//以目的地名稱取代
description: 使用此範本，在Adobe Experience Platform目錄中為您的目的地建立公開檔案。//將取代為概述區段中的段落
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 1%

---

# 您的目的地 {#your-destination}

*瀏覽此模板時，替換或刪除所有斜體段落（從此模板開始）。*

*首先，請更新頁面頂端的中繼資料（標題和說明）。請忽略此頁上的所有UICONTROL實例。 這個標籤可協助我們的機器翻譯程式將頁面正確翻譯成我們支援的多種語言。 在您提交文檔後，我們將向其添加標籤。*

## 概覽 {#overview}

*提供您公司的簡短概述，包括提供給客戶的價值。包含指向產品文檔首頁的連結，以便進一步閱讀。*

>[!IMPORTANT]
>
>此檔案頁面由&#x200B;*YOURDESTINATION*&#x200B;團隊建立。 有關任何查詢或更新請求，請直接聯繫他們，聯繫地址為&#x200B;*插入連結或電子郵件地址，您可以在此處獲取更新*

## 先決條件 {#prerequisites}

*在本節中新增客戶開始在Adobe Experience Platform使用者介面中設定目的地前，需要注意之事項的相關資訊。這可以是：*

* *需要添加到允許清單*
* *電子郵件雜湊要求*
* *任何你方的賬戶細節*
* *如何取得API金鑰以連線至您的平台*

*如果這對客戶有用，您可以連結至相關檔案。*

## 支援的身分 {#supported-identities}

*在本節中新增目的地所支援身分的相關資訊。我們已預先填入一些標準值。 刪除未應用於目標的值和未預填的值。*

** YOURDESTINATION支援下表所述的身分識別的啟用。深入了解[identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當源標識為GAID命名空間時，選擇GAID目標標識。 |
| IDFA | 廣告商專用的Apple ID | 如果來源識別為IDFA命名空間，請選取IDFA目標識別。 |
| ECID | Experience Cloud ID | 代表ECID的命名空間。 此命名空間也可由下列別名引用：&quot;Adobe Marketing Cloud ID&quot;、&quot;Adobe Experience Cloud ID&quot;、&quot;Adobe Experience Platform ID&quot;。 如需詳細資訊，請參閱以下關於[ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html)的檔案。 |
| phone_sha256 | 使用SHA256演算法雜湊的電話號碼 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼。 當源欄位包含未雜湊屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當源欄位包含未雜湊屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。 |
| extern_id | 自訂使用者ID | 當源標識為自定義命名空間時，選擇此目標標識。 |

{style=&quot;table-layout:auto&quot;}

## 匯出類型 {#export-type}

**區段匯出**  — 您會匯出區段（對象）的所有成員，並匯出YOURDESTINATIONdestination中使用的識別碼(名稱、電話號碼或其 ** 他)。

## 使用案例

為協助您更清楚了解您應如何及何時使用&#x200B;*YOURDESTINATION*&#x200B;目的地，以下是Adobe Experience Platform客戶可借由使用此目的地解決的範例使用案例。


### 使用案例#1

*針對行動訊息平台：*

*一個房屋租賃和銷售平台想要向客戶的Android和iOS設備推播移動通知，讓他們知道，他們之前在尋找租房的地區有100個更新清單。*

### 使用案例#2

*針對社交網路平台：*

*運動服裝品牌想透過其社交媒體帳戶觸及現有客戶。服飾品牌可將其CRM的電子郵件地址內嵌至Adobe Experience Platform、從其離線資料建立區段，並將這些區段傳送至YOURDESTINATION，以在其客戶的社交媒體摘要中顯示廣告。*

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)此目標時，您必須提供下列資訊：

*新增客戶在設定新目的地時必須填入的欄位。這些欄位是目的地專屬欄位，視您在目的地SDK中的設定而定。 目標的欄位可能與下面列出的欄位不同。*

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:您 ** 的DESTINATION帳戶ID。


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

## 啟用此目的地的區段 {#activate}

請參閱[啟動設定檔和區段至串流區段匯出目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) ，以取得啟動受眾區段至此目的地的指示。

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

## 匯出的資料 {#exported-data}

*新增資料如何匯出至目的地的附註。這可協助客戶確定他們已正確與您的目的地整合。 例如，您可以提供範例JSON，如下所示。*

```
{
  "person": {
    "email": "yourstruly@adobe.con"
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

## 資料使用與控管 {#data-usage-governance}

處理資料時，所有[!DNL Adobe Experience Platform]目標都符合資料使用策略。 有關[!DNL Adobe Experience Platform]如何實施資料控管的詳細資訊，請參閱[資料控管概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。

## 其他資源 {#additional-resources}

*您可以提供產品檔案的進一步連結，或您認為對客戶而言重要的任何其他資源，以利其成功。*
