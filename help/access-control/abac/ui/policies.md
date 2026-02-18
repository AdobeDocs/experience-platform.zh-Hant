---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制；ABAC
title: 管理存取控制原則
description: 透過Adobe Experience Cloud中的許可權介面管理存取控制原則。
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 2a26c8786adc412dc643c8a0c94b966e439e034b
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 8%

---

# 管理存取控制原則

存取控制原則是將屬性集合在一起，以建立允許和不允許動作的陳述式。 Adobe提供預設原則，可立即啟動，或您的組織準備好開始根據[標籤](./labels.md){target="_blank"}控制特定物件的存取時啟動。 預設原則&#x200B;**[!UICONTROL Default-Label-Based-Access-Control-Policy]**&#x200B;會利用套用至資源的標籤來拒絕存取，除非使用者在角色中具有相符的標籤。

>[!IMPORTANT]
>
>存取控制原則不應與資料使用原則混淆，後者控制資料在Adobe Experience Platform中的使用方式。 如需詳細資訊，請參閱建立[資料使用原則](../../../data-governance/policies/create.md){target="_blank"}指南。

## 設定原則的沙箱 {#configure-policy}

原則會套用至沙箱層級，以控制哪些沙箱會強制執行標籤型存取控制。 預設會開啟&#x200B;**[!UICONTROL Auto-include]**&#x200B;功能，這表示所有目前和未來的沙箱都會自動新增到原則中。 當&#x200B;**[!UICONTROL Auto-include]**&#x200B;關閉時，只有您手動新增的沙箱會受原則的存取控制規則的約束。

>[!NOTE]
>
>**[!UICONTROL Default-Label-Based-Access-Control-Policy]**&#x200B;原則是目前唯一可供設定的原則。

若要開始設定原則的沙箱，請在&#x200B;**[!UICONTROL Permissions]** Adobe Experience Cloud[中導覽至](https://experience.adobe.com/){target="_blank"}。 從左側面板中選取&#x200B;**[!UICONTROL Policies]**，然後從清單中選取&#x200B;**[!UICONTROL Default-Label-Based-Access-Control-Policy]**。

![顯示現有原則清單的原則工作區。](../../images/ui/policies/policies-home.png){zoomable="yes"}

原則的詳細資訊工作區隨即顯示。 選取&#x200B;**[!UICONTROL Sandboxes]**&#x200B;標籤以檢視與原則關聯的沙箱清單，並存取沙箱組態選項。

![原則的沙箱工作區顯示關聯沙箱清單。](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### 管理自動加入 {#manage-auto-include}

>[!IMPORTANT]
>
>預設會開啟&#x200B;**[!UICONTROL Auto-include]**，這表示所有目前和未來的沙箱都會自動新增到原則中。

若要控制原則中包含哪些沙箱，您可以開啟或關閉&#x200B;**[!UICONTROL Auto-include]**&#x200B;功能。 當您關閉&#x200B;**[!UICONTROL Auto-include]**&#x200B;時，未來的沙箱將不會自動新增到原則中。 但是，切換功能&#x200B;**將不會**&#x200B;移除原則中已包含的任何沙箱。

![原則的[沙箱]索引標籤中，[自動包含]切換反白顯示，且處於[關閉]狀態。](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

若要重新啟用&#x200B;**[!UICONTROL Auto-include]**，請使用切換開關將其開啟。 **[!UICONTROL Enable Auto-include]**&#x200B;對話方塊會出現，提示您確認您的選擇。 選取&#x200B;**[!UICONTROL Enable]**&#x200B;以完成組態設定。

>[!NOTE]
>
>當您重新啟用&#x200B;**[!UICONTROL Auto-include]**&#x200B;時，先前從原則中移除的任何沙箱都將重新新增。

![反白顯示[啟用選項]的[啟用自動包含]對話方塊。](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### 手動管理沙箱 {#manually-manage-sandboxes}

當&#x200B;**[!UICONTROL Auto-include]**&#x200B;關閉時，您可以從原則中手動新增或移除特定沙箱。 這可讓您精確控制哪些沙箱會執行原則的存取控制規則。

>[!NOTE]
>
>若要手動新增或移除沙箱，**[!UICONTROL Auto-include]**&#x200B;切換&#x200B;**必須**&#x200B;關閉。

**若要新增沙箱：**

從原則的沙箱工作區中選取&#x200B;**[!UICONTROL Add Sandboxes]**。

![原則的工作區中，[新增沙箱]選項已反白顯示。](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

**[!UICONTROL Add Sandboxes]**&#x200B;對話方塊隨即顯示，顯示您的可用沙箱資料庫。 選取您要新增至原則的沙箱，然後選取&#x200B;**[!UICONTROL Save]**。

![已選取沙箱且「儲存」選項反白顯示的「新增沙箱」對話方塊。](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>如果原則中已經包含所有可用的沙箱，您會在對話方塊中看到「資料庫中沒有任何專案」訊息。

**若要移除沙箱：**

尋找您要從清單中移除的沙箱，並選取其名稱旁的&#x200B;**X**&#x200B;圖示。

![原則的「沙箱」清單（反白顯示「x」）以移除沙箱。](../../images/ui/policies/policy-remove-sandbox.png){zoomable="yes"}

確認對話方塊隨即顯示。 選取&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成從原則中移除沙箱。

![沙箱的確認對話方塊中反白顯示[確認]選項。](../../images/ui/policies/policy-remove-sandbox-confirmation.png){zoomable="yes"}

## 啟動原則 {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="什麼是原則？"
>abstract="策略是將屬性組合在一起的陳述式，用於建立允許和不允許的動作。每個組織都有一個預設原則，您必須啟動該原則才能開始根據標籤控制特定物件的存取權。除非使用者被指派的角色擁有相符的標籤，否則資源所套用的標籤將拒絕使用者存取。原則無法編輯或刪除，但可加以啟用或停用。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-platform/access-control/abac/permissions-ui/labels" text="管理標籤"

若要啟用現有原則，請從&#x200B;**[!UICONTROL Policies]**&#x200B;的&#x200B;**[!UICONTROL Permissions]**&#x200B;索引標籤中選取原則。 原則啟用狀態會顯示在&#x200B;**[!UICONTROL Status]**&#x200B;區段下。

![原則的工作區已反白顯示原則的狀態。](../../images/ui/policies/policy-status.png){zoomable="yes"}

將會顯示原則的詳細資料工作區。 選擇「**[!UICONTROL Activate]**」。

![原則詳細工作區的[啟用]選項已反白顯示。](../../images/ui/policies/policy-activate.png){zoomable="yes"}

**[!UICONTROL Activate Policy]**&#x200B;對話方塊隨即顯示。 選取&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成啟用原則。

![反白顯示[確認]選項的[啟動原則]對話方塊。](../../images/ui/policies/policy-activate-confirm.png){zoomable="yes"}

## 後續步驟

啟用原則後，您可以繼續下一步以[管理角色](permissions.md)的許可權。
