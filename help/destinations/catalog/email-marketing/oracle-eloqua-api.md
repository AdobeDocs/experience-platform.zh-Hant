---
title: (API)OracleEloqua連線
description: (API)OracleEloqua目的地可讓您匯出帳戶資料，並在Eloqua中根據您的業務需求啟動該資料，以符合Oracle的需求。
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---

# [!DNL (API) Oracle Eloqua] 連接

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 可讓行銷人員規劃及執行行銷活動，同時為潛在客戶提供個人化的客戶體驗。 透過整合式銷售機會管理和輕鬆的行銷活動建立，協助行銷人員在購買者歷程的適當時間與適當的對象互動，並優雅地調整規模以跨通路觸及對象，包括電子郵件、顯示搜尋、影片和行動裝置。 銷售團隊可以更快完成更多交易，透過即時分析提高行銷ROI。

此 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 利用 [更新聯繫人](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) 操作 [!DNL Oracle Eloqua] REST API，可讓您將區段內的身分識別更新為 [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] uses [基本驗證](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) 與 [!DNL Oracle Eloqua] REST API。 向您的 [!DNL Oracle Eloqua] 執行個體在下方， [驗證到目標](#authenticate) 區段。

## 使用案例 {#use-cases}

身為行銷人員，您可以根據使用者Adobe Experience Platform設定檔的屬性，為使用者提供個人化體驗。 您可以從離線資料建立區段，並將這些區段傳送至 [!DNL Oracle Eloqua]，可在Adobe Experience Platform中更新區段和設定檔時，立即顯示在使用者的動態消息中。

## 先決條件 {#prerequisites}

### Experience Platform必要條件 {#prerequisites-in-experience-platform}

在將資料啟用至 [!DNL Oracle Eloqua] 目的地，您必須 [綱要](/help/xdm/schema/composition.md), [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)，和 [區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立於 [!DNL Experience Platform].

請參閱Experience Platform檔案，以了解 [區段成員資格詳細資料結構欄位群組](/help/xdm/field-groups/profile/segmentation.md) 如果您需要區段狀態的指引。

### [!DNL Oracle Eloqua] 必要條件 {#prerequisites-destination}

若要將資料從Platform匯出至 [!DNL Oracle Eloqua] 帳戶 [!DNL Oracle Eloqua] 帳戶。

#### 收集 [!DNL Oracle Eloqua] 憑據 {#gather-credentials}

在驗證之前，請記下下列項目 [!DNL Oracle Eloqua] 目的地：

| 憑據 | 說明 |
| --- | --- |
| `Username` | 您的 [!DNL Oracle Eloqua] 帳戶。 |
| `Password` | 您 [!DNL Oracle Eloqua] 帳戶。 |

## 護欄 {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] 自訂連絡欄位會使用在 **[!UICONTROL 選取區段]** 步驟。


* [!DNL Oracle Eloqua] 有250個自訂連絡欄位的上限。
* 匯出新區段之前，請確定Platform區段的數量和 [!DNL Oracle Eloqua] 請勿超過此限制。
* 如果超過此限制，您會在Experience Platform中遇到錯誤。 這是因為 [!DNL Oracle Eloqua] API無法驗證要求，並使用 — 回應 *400:驗證錯誤*  — 說明問題的錯誤訊息。
* 如果您達到上述指定的限制，則需要從目的地移除現有對應，並刪除您 [!DNL Oracle Eloqua] 帳戶才能匯出更多區段。

* 請參閱 [Oracle雄辯建立聯繫欄位](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) 頁面以取得其他限制的相關資訊。

## 支援的身分 {#supported-identities}

[!DNL Oracle Eloqua] 支援下表所述的身分識別更新。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 範例 | 說明 | 必要 |
|---|---|---|---|
| `EloquaId` | `111111` | 聯繫人的唯一標識符。 | 是 |

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

內 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]** 搜尋 [!DNL (API) Oracle Eloqua]. 或者，您也可以在 **[!UICONTROL 電子郵件行銷]** 類別。

### 驗證到目標 {#authenticate}

填寫下方的必填欄位。 請參閱 [收集 [!DNL Oracle Eloqua] 憑據](#gather-credentials) 區段。
* **[!UICONTROL 密碼]**:您 [!DNL Oracle Eloqua] 帳戶。
* **[!UICONTROL 使用者名稱]**:您的 [!DNL Oracle Eloqua] 帳戶。

要驗證到目標，請選擇 **[!UICONTROL 連接到目標]**.
![Platform UI螢幕擷取畫面，顯示如何驗證。](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

如果提供的詳細資料有效，UI會顯示 **[!UICONTROL 已連接]** 狀態（帶綠色複選標籤）。 接著，您可以繼續進行下一個步驟。

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。
![Platform UI螢幕擷取畫面，顯示目的地詳細資訊。](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將您的對象資料從Adobe Experience Platform正確傳送至 [!DNL Oracle Eloqua] 目的地，您必須執行欄位對應步驟。 對應包含在您的Platform帳戶中的Experience Data Model(XDM)結構欄位與目標目的地對應的欄位之間建立連結。

`EloquaID` 必須更新與身分對應的屬性。 此 `emailAddress` 也是必要的，否則API會擲回錯誤，如下所示：

```json
{
   "type":"ObjectValidationError",
   "container":{
      "type":"ObjectKey",
      "objectType":"Contact"
   },
   "property":"emailAddress",
   "requirement":{
      "type":"EmailAddressRequirement"
   },
   "value":"<null>"
}
```

在 **[!UICONTROL 目標欄位]** 名稱應與屬性對應表中所述完全相同，因為這些屬性將形成請求正文。

在 **[!UICONTROL 源欄位]** 不遵守任何此類限制。 您可以視需要對應，但如果資料格式推送至時不正確 [!DNL Oracle Eloqua] 這會導致錯誤。

例如，您可以對應 **[!UICONTROL 源欄位]** 身分命名空間 `contact key`, `ABC ID` 等。 to **[!UICONTROL 目標欄位]** : `EloquaID` 確保ID值符合所接受的格式 [!DNL Oracle Eloqua].

若要正確將XDM欄位對應至 [!DNL Oracle Eloqua] 目標欄位，請遵循下列步驟：

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**. 畫面上會顯示新的對應列。
1. 在 **[!UICONTROL 選擇源欄位]** 窗口，選擇 **[!UICONTROL 選擇屬性]** 類別，然後選取XDM屬性或選擇 **[!UICONTROL 選取身分命名空間]** 並選擇身份。
1. 在 **[!UICONTROL 選擇目標欄位]** 窗口，選擇 **[!UICONTROL 選取身分命名空間]** 並選擇身份或 **[!UICONTROL 選取自訂屬性]** 類別，並視需要選取屬性。
   * 重複這些步驟，新增XDM設定檔架構與 [!DNL Oracle Eloqua] 例項： |源欄位|目標欄位|必填| |—|—|—| |`xdm: personalEmail.address`|`Attribute: emailAddress`|是 | |`IdentityMap: Eid`|`Identity: EloquaId`|是 |

   * 使用這些對應的範例如下所示：
      ![Platform UI螢幕擷取範例及屬性對應。](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

      >[!IMPORTANT]
      >
      >兩者 `emailAddress` 和 `EloquaId` target屬性對應是必填的。

完成為目標連接提供映射時，請選擇 **[!UICONTROL 下一個]**.

>[!NOTE]
>
>在將聯繫人欄位資訊發送到 [!DNL Oracle Eloqua]. 這可確保與區段名稱對應的聯絡人欄位名稱不會重疊。 請參閱 [驗證資料匯出](#exported-data) 部分螢幕截圖示例 [!DNL Oracle Eloqua] 「連絡人詳細資料」頁面，以及使用區段名稱建立的自訂連絡人欄位。

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 選擇 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** 並導覽至目的地清單。
1. 接下來，選取目的地並切換至 **[!UICONTROL 啟動資料]** ，然後選取區段名稱。
   ![Platform UI螢幕擷取範例，顯示「目的地啟動資料」。](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. 監控區段摘要，並確保設定檔的計數與區段內的計數相對應。
   ![Platform UI螢幕擷取範例，顯示「區段」。](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. 登入 [!DNL Oracle Eloqua] 網站，然後導覽至 **[!UICONTROL 聯繫人概覽]** 頁面，檢查區段中的設定檔是否已新增。 若要查看區段狀態，請向下切入 **[!UICONTROL 聯繫人詳細資訊]** 頁面，並檢查是否已建立以所選區段名稱作為首碼的聯絡欄位。

![OracleEloqua UI螢幕截圖顯示「聯繫人詳細資訊」頁面，其中自定義聯繫人欄位以段名稱建立。](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).

## 錯誤和疑難排解 {#errors-and-troubleshooting}

建立目的地時，您可能會收到下列其中一則錯誤訊息： `400: There was a validation error` 或 `400 BAD_REQUEST`. 若超過250個自訂連絡欄位限制，就會發生此情況，如 [護欄](#guardrails) 區段。 若要修正此錯誤，請確定您未超過 [!DNL Oracle Eloqua].
![Platform UI螢幕擷取畫面顯示錯誤。](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

請參閱 [[!DNL Oracle Eloqua] HTTP狀態代碼](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) 和 [[!DNL Oracle Eloqua] 驗證錯誤](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) 頁面，以取得狀態和錯誤碼的完整清單，並提供說明。

## 其他資源 {#additional-resources}

來自 [!DNL Oracle ELoqua] 檔案如下：
* [OracleEloqua行銷自動化](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [REST API for EloquaOracleMarketing Cloud服務](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)