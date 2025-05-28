---
title: 相互傳輸層安全性(mTLS)概觀
description: 瞭解如何使用mTLS安全地擷取Adobe為事件轉送所發行的公開憑證。
exl-id: e8ee8655-213d-4d2a-93d4-d62824b53b1d
source-git-commit: ab16cc3f70ec54460c7c4834e665c828d75d4d9e
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 2%

---

# 相互傳輸層安全性([!DNL mTLS])總覽

繫結[!UICONTROL 環境UI]中的相互傳輸層安全性([!DNL mTLS])憑證，以取得您擴充功能的安全性。 [!DNL mTLS]憑證是數位認證，可證明安全通訊中的伺服器或使用者端身分。 當您使用[!DNL mTLS]服務API時，這些憑證可協助您驗證並加密Adobe Experience Platform事件轉送的互動。 此過程不僅可保護您的資料，還可確保每個連線都來自信任的合作夥伴。

## 在新環境中實作[!DNL mTLS] {#implement-mtls}

設定Event Forwarding環境，確保您的程式庫組建正確部署至Edge網路。 在設定期間，您可以選取最符合部署需求的託管選項。 [!DNL mTLS]憑證也會自動新增至您的新環境，以進行安全通訊。

若要建立新環境，請選取[事件轉送]屬性左側面板中的&#x200B;**[!UICONTROL 環境]**&#x200B;索引標籤，然後選取&#x200B;**[!UICONTROL 新增環境]**。

![顯示現有環境的事件轉送屬性，醒目提示[!UICONTROL 新增環境]。](../../../images/extensions/server/cloud-connector/add-environment.png)

在下一個頁面，選取要用於此設定的環境。 提供三種環境：

>[!NOTE]
>
>屬性僅限於一個開發、一個測試和一個生產環境。

| 環境 | 說明 |
| --- | --- |
| 開發 | 開發環境可供團隊成員測試事件轉送中的程式庫或變更。 |
| 預備 | 測試環境為選用環境，可讓已核准的團隊成員在程式庫發佈前測試和核准。 |
| 生產 | 生產環境用於即時生產資料。 |

![環境選取畫面，反白顯示[!UICONTROL 為開發選取]。](../../../images/extensions/server/cloud-connector/select-environment.png)

在&#x200B;**[!UICONTROL 建立環境]**&#x200B;頁面上，輸入&#x200B;**[!UICONTROL 名稱]**，然後從&#x200B;**[!UICONTROL 選取主機]**&#x200B;下拉式選單中選取&#x200B;***Adobe Managed***。 **[!UICONTROL 憑證]**&#x200B;是&#x200B;***自動新增***。 最後，選取&#x200B;**[!UICONTROL 儲存]**。

![建立開發環境頁面，醒目提示[!UICONTROL 名稱]、[!UICONTROL 選取主機]和[!UICONTROL 儲存]。](../../../images/extensions/server/cloud-connector/create-environment.png)

環境已成功建立，並且您返回到&#x200B;**[!UICONTROL 環境]**&#x200B;標籤，該標籤顯示您的新環境。

![ [!UICONTROL 環境]標籤，醒目提示開發環境。](../../../images/extensions/server/cloud-connector/new-environment-created.png)

## 檢視環境憑證詳細資訊 {#view-certificate}

若要檢視環境的憑證詳細資訊，請選取「事件轉送」屬性左側面板中的&#x200B;**[!UICONTROL 環境]**&#x200B;索引標籤，然後選取環境以檢視詳細資訊。

將顯示以下憑證詳細資料：

| 欄位名稱 | 說明 |
| --- | --- |
| 憑證 | 憑證的詳細資訊，包括：<ul><li>**名稱**：憑證的名稱。</li><li>**建立日期**：憑證建立的日期。</li><li>**狀態**：憑證的目前狀態：<ul><li>**目前**：憑證正在使用中。</li><li>**已過時**：憑證不在使用中，但尚未過期。 您仍可選取它來使用。</li><li>**已過期**：憑證已過期、變成灰色，且不再可供使用。</li></ul></ul> |
| 過期 | 憑證到期的日期。 |
| Variable Name | 憑證的變數名稱。 |
| 狀態 | 憑證的目前狀態：<ul><li>**已解壓縮**：憑證已成功部署且作用中。</li><li>**正在部署**：正在部署憑證。</li><li>**需要部署**：當選取過時的憑證時，會出現此狀態。</li></ul> |

![編輯開發環境頁面，醒目提示[!UICONTROL 憑證]詳細資料。](../../../images/extensions/server/cloud-connector/certificate-details.png)

### 選取並部署過時的憑證 {#deploy-obsolete-certificate}

若要使用過時的憑證，請導覽至「事件轉送」屬性左側面板中的「**[!UICONTROL 環境]**」標籤，然後選取環境以檢視其詳細資料。

![ [!UICONTROL 環境]標籤，醒目提示開發環境。](../../../images/extensions/server/cloud-connector/new-environment-created.png)

從&#x200B;**[!UICONTROL 憑證]**&#x200B;下拉式清單中，選取過時的憑證，然後選取&#x200B;**[!UICONTROL 儲存]**。

![編輯開發環境頁面，醒目提示[!UICONTROL 憑證]下拉式清單，其中含有過時的憑證並醒目提示「儲存」。](../../../images/extensions/server/cloud-connector/obsolete-certificate.png)

若要部署憑證，請在&#x200B;**[!UICONTROL 部署憑證]**&#x200B;對話方塊中選取&#x200B;**[!UICONTROL 儲存並部署]**。

![部署憑證對話方塊，並反白顯示[儲存並部署]。](../../../images/extensions/server/cloud-connector/obsolete-certificate-deploy.png)


## 後續步驟 {#next-steps}

本檔案示範如何為事件轉送屬性建立環境、新增憑證及使用過時的憑證。 如需[!DNL mTLS]憑證的詳細資訊，請參閱[[!DNL mTLS] 服務API總覽](../../../../data-governance/mtls-api/overview.md)

若要瞭解如何在事件轉送規則中使用[!DNL mTLS]憑證，請參閱[雲端聯結器擴充功能概觀](../cloud-connector/overview.md/#mtls-rules)。
