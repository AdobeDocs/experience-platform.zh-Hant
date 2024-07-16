---
keywords: 串流， Qualtrics目的地
title: Qualtrics自動化
description: 同步體驗和營運客戶資料，以大規模解除個人化鎖定。 在Adobe Experience Platform中彙總多個營運資料來源，作為Qualtrics Experience Id中的輸入專案，以更好地瞭解您的客戶，並實現目標式外聯，在瞭解意圖、情緒和體驗驅動因素方面縮小差距。
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 3%

---

# Qualtrics自動化

## 概觀 {#overview}

同步體驗和營運客戶資料，以大規模解除個人化鎖定。

在Adobe Experience Platform中彙總多個營運資料來源，作為Qualtrics Experience Id中的輸入專案，以更好地瞭解您的客戶，並實現目標式外聯，在瞭解意圖、情緒和體驗驅動因素方面縮小差距。

>[!IMPORTANT]
>
>目的地聯結器和檔案頁面是由Qualtrics團隊建立和維護的。 如有任何查詢或更新要求，請登入[客戶成功中心](https://support-portal.qualtrics.com/)，直接連絡他們。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用&#x200B;*Qualtrics自動化*&#x200B;目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 使用案例#1 {#use-case-1}

**案例**：公司想要測量各種數位接觸點（例如其網站和行動應用程式）的客戶滿意度。 他們使用Adobe Experience Platform根據使用者互動來觸發Qualtrics調查，例如完成購買或造訪特定網頁。

**結果**：透過收集即時意見回饋，公司可以改善其客戶體驗，進而提高滿意度和忠誠度。

### 使用案例#2 {#use-case-2}

**案例**：組織希望提升員工上線流程。 他們利用Adobe Experience Platform透過Qualtrics調查收集新聘人員的意見回饋。 在預先定義的入門期間後，調查會自動觸發。

**結果**：持續回饋可讓組織調整並改善上線流程，進而提高新員工的參與度和生產力。

## 先決條件

在Adobe Experience Platform中設定Qualtrics目的地之前，請確定已符合下列必要條件：

* 您有Qualtrics帳戶。
* 您已從Qualtrics取得必要的API權杖。

### 取得API權杖

以下是從Qualtrics取得API權杖的必要步驟。

1. 登入您的Qualtrics帳戶。
2. 移至&#x200B;**帳戶設定**。
3. 選取&#x200B;**Qualtrics ID**。
4. 在此頁面上尋找&#x200B;**API**&#x200B;區段，其中包含&#x200B;**Token**&#x200B;欄位。 這是API Token，在目的地設定期間為必要。

## 支援的身分 {#supported-identities}

*Qualtrics Automations*&#x200B;支援啟用下表所述的身分。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 純文字電子郵件地址 | Qualtrics僅支援純文字電子郵件地址。 |
| external_id | 自訂使用者ID | 當您的來源身分是自訂名稱空間時，請選取此目標身分。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，其中包含&#x200B;*Qualtrics Automations*&#x200B;目的地中使用的識別碼（名稱、電話號碼或其他）。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據區段評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

在驗證過程中，您必須提供&#x200B;**使用者名稱**&#x200B;和&#x200B;**密碼**。 使用者名稱是您的Qualtrics使用者名稱，密碼是您的Qualtrics帳戶的API權杖。 若要擷取API Token，請依照以上&#x200B;**必要條件**&#x200B;一節中的指示操作。

![驗證](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL URL]**：在[JSON事件](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About)中找到的URL會觸發您在Qualtrics](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About)中的[工作流程。 如需範例，請參閱下方的熒幕擷圖。

![URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

閱讀[啟用串流區段匯出目的地的設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md)，以取得啟用此目的地的對象區段的指示。

### 對應屬性和身分 {#map}

此目的地有開啟的結構描述，因此您可以將任何屬性傳送至Qualtrics。

#### 對應屬性

若要將屬性加入對應，只要在新增對應時選取&#x200B;**自訂屬性**&#x200B;即可。 您可以為屬性輸入任何名稱。 Qualtrics鼓勵屬性名稱採用&#x200B;*camelCase*&#x200B;命名慣例（請參閱下面的熒幕擷圖範例）。

![自訂屬性](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

如需可能的屬性對應範例，請參閱下面的熒幕擷圖。

![範例對應](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### 對應身分

必須為此目的地選取身分名稱空間。 目標欄位對應的兩個可能來源欄位為：

| 來源欄位 | 目標欄位 |
|--------------------|-----------------------|
| IdentityMap：電子郵件 | 身分：電子郵件 |
| IdentityMap： ECID | 身分： external_id |

如需範例，請參閱下方的熒幕擷圖。

![身分名稱空間](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

如前所述，此目的地使用開放式結構描述，因此所有屬性皆可傳送至Qualtrics。 儘管如此，傳送至Qualtrics的資料將遵循以下結構：

```json
{
  "person": {
    "name": {
      "firstName": "Dave"
    }
  },
  "mobilePhone": {
    "number": "0123456789"
  },
  "identityMap": {
    "Email": [
      {
        "id": "Email-2Sf6C"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "046456e3b-18e1-48a6-9bda-d68547861283": {
        "lastQualificationTime": "2023-09-05T10:43:55.602687Z",
        "status": "realized"
      },
      "007844dd1-9e5d-4531-a4ee-05470doe759dd": {
        "lastQualificationTime": "2023-09-05T10:43:55.602689Z",
        "status": "realized"
      }
    }
  }
}
```

若要確認已在Qualtrics中擷取資料，請前往包含您的&#x200B;**JSON事件**&#x200B;的工作流程，從那裡，移至&#x200B;**執行歷程記錄**，您應該會在此看到工作流程的執行。 每個工作流程的狀態為&#x200B;**成功**&#x200B;或&#x200B;**失敗**。 選取特定執行會顯示其相關詳細資訊，讓您可在遇到任何問題時進行疑難排解。

如果&#x200B;**執行歷程記錄**&#x200B;中沒有可見的執行，則表示尚未觸發工作流程，表示可能有問題。 請確認工作流程已啟用，且Adobe Experience Platform中的目的地&#x200B;**URL**&#x200B;正確無誤。 工作流程執行並非立即執行，因此您可能會必須等候一段時間才能完成。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。
