---
title: 標籤擴充功能管理
description: 瞭解如何在Adobe Experience Platform Tags中管理和共用擴充功能套件。
exl-id: 3dfd801a-febc-4461-bd99-5f97682518ce
source-git-commit: 91c8b36ec1b752e288ed8be61f3946eaf8532760
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 0%

---

# 標籤擴充功能管理

Adobe Experience Platform可讓您管理&#x200B;**[!UICONTROL Owned]**&#x200B;擴充功能。 您可以上傳新的擴充功能、部署新版本，並將其發行為私人或公開可用。

## 管理擴充功能  {#manage-extension}

在您在本機準備擴充功能套件之後，請在資料收集UI中使用&#x200B;**[!UICONTROL Extension Management]**&#x200B;上傳該套件、驗證該套件，並透過&#x200B;**開發**、**私人**&#x200B;和&#x200B;**公開**&#x200B;可用性發行版本。 接著，您可以在屬性上安裝擴充功能，並使用它進行測試。

### 上傳擴充功能 {#upload-extension}

若要上傳擴充功能，請導覽至資料收集UI，然後從左側導覽中選取&#x200B;**[!UICONTROL Extension Management]**。 從這裡，選取&#x200B;**[!UICONTROL Owned]**&#x200B;標籤。 此標籤會顯示您或您的組織擁有的任何擴充功能。 這些擴充功能以平台分隔，您可以使用下拉式清單檢視每個平台上的擴充功能（網頁、行動裝置和Edge）。 選擇「**[!UICONTROL Upload New Extension]**」。

![顯示與此組織共用的擴充功能清單的[擁有]索引標籤，醒目顯示下拉式清單，並上傳新的擴充功能。](../images/shared-extensions/upload-extension.png)

在&#x200B;**上傳新的擴充功能**&#x200B;頁面上，選取&#x200B;**[!UICONTROL Select Extension Folder]**，瀏覽至包含您擴充功能的資料夾，選取資料夾，然後選取&#x200B;**[!UICONTROL Upload]**。

在本機資料夾中選取![延伸模組。](../images/shared-extensions/selected-extension.png)

透過選取&#x200B;**[!UICONTROL Upload]**&#x200B;來確認將上傳的檔案數。

將顯示要上傳的檔案數，包括副檔名及版本。 您可以選擇執行&#x200B;**[!UICONTROL Dry Run]**，將zip檔案下載到本機電腦以進行檢查。 選擇「**[!UICONTROL Validate & Upload]**」。

![上傳新的擴充功能套件頁面，顯示要上傳的檔案數目，並醒目提示「驗證和上傳」。](../images/shared-extensions/validate-upload.png)

確認您的擴充功能已成功上傳及處理，並顯示您的&#x200B;**擴充功能套件ID**。 選取「**[!UICONTROL Close]**」以返回顯示您擴充功能的「**[!UICONTROL Owned]**」標籤。

![已確認已上載延伸模組，醒目提示封裝識別碼並關閉。](../images/shared-extensions/confirmation-upload.png)

您會回到顯示已上傳之擴充功能的[!UICONTROL Owned]標籤。

>[!IMPORTANT]
>
>擴充功能會在&#x200B;**開發**&#x200B;可用性中上傳。 在&#x200B;**開發**&#x200B;可用性中的擴充功能發行為&#x200B;**私人**&#x200B;可用性之前，無法共用這些擴充功能。

### 發行擴充功能 {#release-extension}

若要發行擴充功能以供私人使用，請選取您的擴充功能，以在右側顯示資訊面板。 您可以在此處檢視擴充功能的下列詳細資料：

* **版本** — 顯示最新版本及其目前狀態。 您可以使用下拉式選單來檢視擴充功能的版本記錄。
* **動作** — 允許您&#x200B;**[!UICONTROL Upload New Version]**&#x200B;擴充功能和&#x200B;**[!UICONTROL Release To Private]**。
* **擴充功能套件ID** — 顯示在底部。 這將根據所選的版本而變更。

![封裝詳細資料面板，醒目提示版本、動作和封裝ID](../images/shared-extensions/package-details.png)

選取「**[!UICONTROL Release To Private]**」，然後再次選取「**[!UICONTROL Release To Private]**」以確認發行。

一旦擴充功能成功發行至&#x200B;**Private**&#x200B;可用性，即會收到確認。 更新的可用性可在右側面板中看到。

![封裝詳細資料面板，強調版本和私人可用性](../images/shared-extensions/package-details-availability.png)

>[!NOTE]
>
>擴充功能發行至&#x200B;**私人**&#x200B;後，即可與其他組織共用。

若要將擴充功能釋出為&#x200B;**Public**&#x200B;可用性，請從右側面板中選取&#x200B;**[!UICONTROL Request Public Release]**。

**[!UICONTROL Release Extension Package]**&#x200B;畫面提供要求表單所需的詳細資料，並提供複製詳細資料的選項。 選擇「**[!UICONTROL Go To Request Form]**」。

![發行擴充功能套件頁面醒目提示完成表單所需的資訊。](../images/shared-extensions/public-request-form.png)

已開啟包含請求表單的新瀏覽器索引標籤。 從&#x200B;**[!UICONTROL Release Extension Package]**&#x200B;畫面複製資訊並貼到相關欄位。 提交完成的表單以供檢閱。 擴充功能公開後，您將會收到通知。

## 與其他組織共用擴充功能套件 {#share-extension}

>[!NOTE]
>
>擴充功能套件必須有私用或公用版本，才能透過[!UICONTROL Usage Authorizations]共用。 標示為開發可用性的版本不符合共用資格，且不會出現在授權下拉式清單中。 即使已共用較舊的版本（例如1.0.0），亦適用。 較新版本（例如1.0.1）必須至少設為私人，接收組織才能授權或安裝這些版本。
>
>如果您稍後選擇將這些套件公開，所有關於共用私人擴充功能套件的指引也適用。 有關可見性、版本設定、安全性、相容性、支援和檔案的相同考量事項，無論套件的可用性狀態為何，都仍然適用。

**[!UICONTROL Usage Authorizations]**&#x200B;是一項強大的功能，您可以使用它來安全地與信任的合作夥伴共用私人擴充套件，而不需在擴充功能目錄中公開提供。 使用此功能在組織之間建立安全的橋樑，讓您能夠運用彼此的自訂擴充功能程式碼，同時維護隱私並控制您的專屬解決方案。

組織通常會根據獨特的業務需求開發專門的擴充功能。 這些擴充功能可能包含不應公開使用的專有邏輯、自訂整合或敏感設定。 使用授權可透過啟用以下功能來解決此挑戰：

* **選擇性共用**：僅與信任的夥伴組織共用私人擴充功能。
* **已維護隱私權**：將機密擴充功能程式碼保留在公用目錄之外。
* **合作開發**：讓信任的合作夥伴從您的自訂解決方案中獲益。
* **控制的存取**：維持對誰可以存取及使用您的私人擴充功能的完整控制。

共用程式涉及兩個主要參與者：

1. **共用組織**：擁有並共用私人擴充功能套件的組織
2. **正在接收組織**：取得共用擴充功能存取權的受信任組織

共用私人版本時，接收組織會獲得該特定版本的存取權，並在兩個組織之間建立直接連線。 如果較新的版本稍後設為私人，接收組織也可以使用該版本，而不需要他們執行任何其他步驟。

### 建立擴充功能套件使用授權 {#package-usage-authorization}

若要共用擴充功能，請導覽至資料收集UI，然後從左側導覽中選取&#x200B;**[!UICONTROL Extension Management]**。 從這裡，選取&#x200B;**[!UICONTROL Usage Authorizations]**&#x200B;標籤。

在這裡，您會看到現有共用授權的清單，這些授權分為兩個類別：

* **與此組織共用**：其他組織與您共用的擴充功能。
* **與其他組織共用**：您與其他組織共用的擴充功能。

選擇「**[!UICONTROL Add Authorization]**」。

![此[!UICONTROL Usage Authorizations]標籤顯示與此組織共用的擴充功能清單，醒目提示[!UICONTROL Add Authorization]](../images/shared-extensions/add-authorization.png)

>[!IMPORTANT]
>
>您必須取得目標組織的&#x200B;**`Organization ID`**&#x200B;組織擁有者。 無法依名稱搜尋組織。

從下拉式清單中選取您要授權擴充功能的&#x200B;**[!UICONTROL Platform]**。 您可以共用&#x200B;**[!UICONTROL Web]**、**[!UICONTROL Mobile]**&#x200B;和&#x200B;**[!UICONTROL Edge]**&#x200B;副檔名。

接下來，在下拉式清單中，從可用擴充功能中選取您要共用的&#x200B;**[!UICONTROL Extension]**。 清單會顯示貴組織擁有的擴充功能及其可用性狀態。 最新版本為&#x200B;**開發**&#x200B;可用性的擴充功能將不會出現在此清單中。

接下來，輸入接收組織的ID，然後選取&#x200B;**[!UICONTROL Save]**。

![顯示所選擴充功能和Adobe組織ID的[!UICONTROL Create extension package usage authorization]頁面已輸入，並醒目提示[!UICONTROL Save]](../images/shared-extensions/save-authorization.png)

您會回到[!UICONTROL Usage Authorizations]標籤，您可以在其中看到&#x200B;**[!UICONTROL Shared with other orgs]**&#x200B;清單中的副檔名。 狀態將顯示&#x200B;**等待核准**，直到接收組織核准授權為止，屆時它將會更新為&#x200B;**已核准**。

![此[!UICONTROL Usage Authorizations]標籤顯示與其他組織共用的擴充功能清單，並醒目提示新授權](../images/shared-extensions/new-authorization.png)

>[!TIP]
>
>您也可以直接從&#x200B;**[!UICONTROL Extension Catalog]**&#x200B;共用擴充功能，方法是選取擴充功能卡上的功能表(⋯)，然後從功能表選取共用選項。

當授權作用中時，共用擴充功能會在目錄中顯示&#x200B;***共用***&#x200B;徽章，表示正在與其他組織共用。

![顯示具有徽章之共用擴充功能的[!UICONTROL Catalog]標籤](../images/shared-extensions/sharing-badge.png)

### 授權及管理共用擴充功能 {#manage-shared-extension}

>[!NOTE]
>
>作為接收組織，您只能核准或拒絕共用擴充功能。 您無法管理或修改授權詳細資料，因為這些詳細資料是由共用組織所控制。

若要授權貴組織的共用擴充功能，請導覽至資料收集UI，並從左側導覽中選取「**[!UICONTROL Extension Management]**」，然後選取「**[!UICONTROL Usage Authorizations]**」標籤。

您可以在&#x200B;**區段中看到共用擴充功能的清單，包括那些**&#x200B;等待核准的&#x200B;**[!UICONTROL Shared with this org]**。 選取您要核准的副檔名，然後選取&#x200B;**[!UICONTROL Approve]**。

![此[!UICONTROL Usage Authorizations]標籤顯示與此組織共用的擴充功能清單，其擴充功能正在等待核准中選取，並醒目顯示[!UICONTROL Approve]](../images/shared-extensions/approve-authorization.png)

>[!NOTE]
>
>如果您的組織不再需要共用擴充功能，您也可以在&#x200B;**[!UICONTROL Usage Authorizations]**&#x200B;標籤內拒絕要求。

在&#x200B;**[!UICONTROL OK]**&#x200B;對話方塊中選取&#x200B;**[!UICONTROL Authorization Usages]**。

![&#x200B; [!UICONTROL Authorization Usages]對話方塊，醒目提示[!UICONTROL OK]](../images/shared-extensions/confirmation.png)

您會回到[!UICONTROL Usage Authorizations]索引標籤，您可以在其中看到擴充功能現在顯示&#x200B;**已核准**&#x200B;狀態。

![此[!UICONTROL Usage Authorizations]標籤會顯示與此組織共用的擴充功能清單，並醒目提示狀態為「已核准」的擴充功能](../images/shared-extensions/approved-authorization.png)

在核准授權後，即可在您的目錄中取得擴充功能，並可像任何其他擴充功能一樣安裝及使用。 共用擴充功能會顯示&#x200B;***接收***&#x200B;徽章，表示它是其他組織與您共用的擴充功能。

![顯示「接收」徽章之共用擴充功能的[!UICONTROL Catalog]標籤](../images/shared-extensions/receiving-badge.png)

### 撤銷授權 {#revoke-authorization}

作為擁有權組織，您可以隨時刪除授權，無論其目前狀態（「等待核准」、「已拒絕」或「已核准」）為何。

**如果您的擴充功能從未公開：**

* 接收組織已安裝的任何私人版本，都會繼續顯示在其已安裝的擴充功能清單中。
* 如果接收組織從未安裝您的擴充功能，該擴充功能就不會再出現在介面中的任何位置。

**如果您的擴充功能已公開：**

* 接收組織安裝的任何私人版本都會顯示在已安裝的擴充功能清單中。
* 如果他們從未安裝您的私人版本，他們仍會在目錄中看到最新的公開版本，並且可以安裝。
* 如有需要，他們也可以將您的私人版本降級為最新的公開版本。

當您撤銷授權時，接收組織會保留某些權利，以保護其現有的實作：

* **繼續使用**：接收組織可以繼續使用他們已安裝的任何私人版本，即使您撤銷存取權之後亦然。
* **組建保護**：如果接收組織已安裝您的私人v1.0.0，而您稍後發行私人v1.0.1，他們將無法看到較新的版本，但可以繼續使用v1.0.0進行建置，而不會中斷。
* **未來升級**：如果您稍後將擴充功能設為公開（例如，公開發佈v2.0.0），接收組織就可以從他們的私人v1.0.0直接升級至新的公開v2.0.0。

>[!IMPORTANT]
>
>撤銷授權不會破壞現有的組建或實作。 接收組織可維護其已安裝的任何私人版本的存取權，以確保業務連續性。

## 後續步驟 {#next-steps}

本文會示範如何使用Experience Platform中的共用擴充功能功能。 如需擴充功能開發的資訊，請參閱[擴充功能開發使用手冊](./getting-started.md)。

如需Experience Platform中擴充功能開發的整體概觀，請參閱[概觀檔案](./overview.md)。
