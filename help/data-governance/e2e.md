---
title: 資料控管端對端指南
description: 請依照完整程式，針對Adobe Experience Platform中的欄位和資料集強制執行資料使用限制。
source-git-commit: c8b2dba9b1e305f826830b8341bf1a6dde4e2da2
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 0%

---

# 資料控管端對端指南

若要控制可對Adobe Experience Platform中的特定資料集和欄位執行哪些行銷動作，您必須設定下列項目：

1. [套用標籤](#labels) 限制其使用情形的資料集和欄位。
1. [設定並啟用資料控管原則](#policy) 來判斷哪些類型的標籤資料可用於特定行銷動作。
1. [將行銷動作套用至您的目的地](#destinations) 指出哪些原則適用於傳送至這些目的地的資料。

完成標籤、原則和行銷動作的設定後，您就可以 [測試策略執行](#test) 以確保它正常運作。

本指南會逐步說明在Platform UI中設定及實作資料控管原則的完整程式。 如需本指南所用功能的詳細資訊，請參閱以下主題的概觀檔案：

* [Adobe Experience Platform資料控管](./home.md)
* [資料使用量標籤](./labels/overview.md)
* [資料使用原則](./policies/overview.md)
* [政策執行](./enforcement/overview.md)

## 套用標籤 {#labels}

如果有要強制限制資料使用的特定資料集，您可以 [直接將標籤套用至資料集](#dataset-labels) 或該資料集中的特定欄位。

或者，您也可以 [將標籤應用於方案](#schema-labels) 如此一來，以該結構為基礎的所有資料集都會繼承相同的標籤。

>[!NOTE]
>
>如需不同資料使用標籤及其預期用途的詳細資訊，請參閱 [資料使用標籤參考](./labels/reference.md). 如果可用的核心標籤未涵蓋您所有需要的使用案例，您可以 [定義您自己的自訂標籤](./labels/user-guide.md#manage-custom-labels) 還有。

### 將標籤套用至資料集 {#dataset-labels}

選擇 **[!UICONTROL 資料集]** 在左側導覽列中，選取您要套用標籤的資料集名稱。 您可以選擇使用搜尋欄位來縮小顯示的資料集清單。

![顯示在Platform UI中選取之資料集的影像](./images/e2e/select-dataset.png)

資料集的詳細資訊檢視隨即顯示。 選取 **[!UICONTROL 資料控管]** 索引標籤來檢視資料集欄位清單，以及已套用至這些欄位的標籤。 選取您要新增標籤的欄位旁的核取方塊，然後選取 **[!UICONTROL 編輯控管標籤]** 在右側邊欄。

![顯示為標籤選擇的多個資料集欄位的影像](./images/e2e/dataset-field-label.png)

>[!NOTE]
>
>如果您想要將標籤新增至整個資料集，請選取旁邊的核取方塊 **[!UICONTROL 欄位名稱]** 在選取 **[!UICONTROL 編輯控管標籤]**.
>
>![此影像顯示為資料集突出顯示的所有欄位](./images/e2e/label-whole-dataset.png)

在下一個對話方塊中，選取您要套用至先前所選資料集欄位的標籤。 完成後，請選取 **[!UICONTROL 儲存變更]**.

![此影像顯示為資料集突出顯示的所有欄位](./images/e2e/save-dataset-labels.png)

請繼續依照上述步驟操作，視需要將標籤套用至不同欄位（或不同資料集）。 完成後，您可以繼續 [啟用資料控管原則](#policy).

### 將標籤應用於架構 {#schema-labels}

選擇 **[!UICONTROL 結構]** 在左側導覽器中，從清單中選擇要添加標籤的架構。

>[!TIP]
>
>如果您不確定哪個結構適用於特定資料集，請選取 **[!UICONTROL 資料集]** 在左側導覽中，然後選取 **[!UICONTROL 結構]** 欄。 在彈出式視窗中選取架構名稱，該名稱會在架構編輯器中開啟架構。
>
>![顯示資料集結構之連結的影像](./images/e2e/schema-from-dataset.png)

架構的結構會顯示在架構編輯器中。 從此處，選取 **[!UICONTROL 標籤]** 頁簽，顯示架構欄位和已應用到它們的標籤的清單視圖。 選取您要新增標籤的欄位旁的核取方塊，然後選取 **[!UICONTROL 編輯控管標籤]** 在右側邊欄。

![此影像顯示為控管標籤選取的單一結構欄位](./images/e2e/schema-field-label.png)

>[!NOTE]
>
>如果要將標籤新增至架構中的所有欄位，請選取頂端列的鉛筆圖示。
>
>![顯示從架構標籤檢視中選取的鉛筆圖示的影像](./images/e2e/label-whole-schema.png)

在下一個對話框中，選擇要應用於先前選擇的架構欄位的標籤。 完成後，請選取 **[!UICONTROL 儲存]**.

![影像，顯示要新增至結構欄位的多個標籤](./images/e2e/save-schema-labels.png)

請繼續依照上述步驟操作，視需要將標籤套用至不同欄位（或不同結構）。 完成後，您可以繼續 [啟用資料控管原則](#policy).

## 啟用資料控管原則 {#policy}

將標籤套用至結構和/或資料集後，您可以建立資料控管原則，限制某些標籤可用的行銷動作。

選擇 **[!UICONTROL 原則]** 在左側導覽中，檢視由Adobe定義的核心原則清單，以及您的組織先前建立的任何自訂原則。

每個核心標籤都有一個相關聯的核心原則，一旦啟用，便會對包含該標籤的任何資料強制執行適當的啟用限制。 若要啟用核心原則，請從清單中選取該核心原則，然後選取 **[!UICONTROL 策略狀態]** 切換為 **[!UICONTROL 已啟用]**.

![顯示UI中啟用核心原則的影像](./images/e2e/enable-core-policy.png)

如果可用的核心原則未涵蓋您的所有使用案例（例如您使用在組織下定義的自訂標籤時），則您可以改為定義自訂原則。 從 **[!UICONTROL 原則]** 工作區，選取 **[!UICONTROL 建立原則]**.

![顯示 [!UICONTROL 建立原則] 按鈕](./images/e2e/create-policy.png)

此時會出現彈出窗口，提示您選擇要建立的策略類型。 選擇 **[!UICONTROL 資料控管原則]**，然後選取 **[!UICONTROL 繼續]**.

![顯示 [!UICONTROL 資料控管原則] 選項](./images/e2e/governance-policy.png)

在下一個畫面中，提供 **[!UICONTROL 名稱]** 和選填 **[!UICONTROL 說明]** 對政策。 在下表中，選擇要檢查此策略的標籤。 換言之，這些是策略將阻止用於您在下一個步驟中指定的市場營銷操作的標籤。

如果選擇多個標籤，則可以使用右側邊欄中的選項來確定是否必須存在所有標籤，以便策略強制執行使用限制，或者是否只需要存在其中一個標籤。 完成後，請選取 **[!UICONTROL 下一個]**.

![在UI中顯示策略基本配置的影像](./images/e2e/configure-policy.png)

在下一個畫面中，選取此原則將限制使用先前選取的標籤的行銷動作。 選擇 **[!UICONTROL 下一個]** 繼續。

![在UI中顯示指派給原則的行銷動作的影像](./images/e2e/select-marketing-action.png)

最後螢幕顯示策略詳細資訊的摘要，以及策略將限制哪些標籤的操作。 選擇 **[!UICONTROL 完成]** 來建立策略。

![顯示已在UI中確認的原則設定的影像](./images/e2e/confirm-policy.png)

策略已建立，但設定為 [!UICONTROL 已停用] 依預設。 從清單中選取原則，然後設定 **[!UICONTROL 策略狀態]** 切換為 **[!UICONTROL 已啟用]** 啟用策略。

![顯示在UI中啟用的已建立策略的影像](./images/e2e/enable-created-policy.png)

繼續執行上述步驟，以建立並啟用您所需的原則，然後再繼續執行下一個步驟。

## 管理目的地的行銷動作 {#destinations}

為了讓您啟用的原則能夠準確判斷哪些資料可以啟動至目的地，您必須將特定行銷動作指派給該目的地。

例如，請考慮啟用策略，該策略可防止任何包含 `C2` 標籤，以防止用於行銷動作「[!UICONTROL 匯出至第三方]」。 在將資料啟用至目的地時，原則會檢查目的地上有哪些行銷動作。 如果&quot;[!UICONTROL 匯出至第三方]」，嘗試使用 `C2` 標籤會導致策略違規。 如果&quot;[!UICONTROL 匯出至第三方]「不存在，不會對具有的目標和資料強制執行策略 `C2` 標籤可以自由激活。

當 [在UI中連接目標](../destinations/ui/connect-destination.md), **[!UICONTROL 治理]** 工作流程中的步驟可讓您選取套用至此目的地的行銷動作，最終決定要對目的地強制執行哪些資料控管原則。

![顯示為目的地選取行銷動作的影像](./images/e2e/destination-marketing-actions.png)

## 測試策略實施 {#test}

在您標示資料、啟用資料控管原則，以及將行銷動作指派給目的地後，即可測試原則是否如預期般執行。

如果設定正確，當您嘗試激活受策略限制的資料時，激活將被自動拒絕，並出現策略違規消息，概述有關導致違規的原因的詳細資料處理資訊。

請參閱 [自動策略執行](./enforcement/auto-enforcement.md) 有關如何解釋策略違規消息的詳細資訊。

## 後續步驟

本指南說明在啟動工作流程中設定及執行資料控管原則的必要步驟。 如需本指南中相關資料控管元件的詳細資訊，請參閱下列檔案：

* [資料使用量標籤](./labels/overview.md)
* [資料使用原則](./policies/overview.md)
* [政策執行](./enforcement/overview.md)
