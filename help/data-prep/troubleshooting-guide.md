---
keywords: Experience Platform；首頁；熱門主題；
title: 資料準備疑難排解指南
description: 本檔案提供有關Adobe Experience Platform資料準備常見問題的解答。
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: ff8f660c2b3a04d8b4b9d4f19891816a44069088
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# [!DNL Data Prep]疑難排解指南

本檔案提供有關Adobe Experience Platform [!DNL Data Prep]常見問題的解答，以及常見錯誤的疑難排解指南。 如需Platform API的一般問題和疑難排解資訊，請參閱[Adobe Experience Platform API疑難排解指南](../landing/troubleshooting.md)。

## 常見問題集

以下為關於[!DNL Data Prep]常見問題集及其答案的清單。

### 如何解決轉換錯誤？

[!DNL Data Prep]將所有轉換錯誤當地語系化至其發生的資料行。 因此，該欄會失效，而列的其餘部分會繼續處理。 這些轉換問題記錄為&#x200B;**警告**。 建議您定期檢閱警告，並調整轉換邏輯，以解決轉換問題。 這會提高擷取至Experience Platform的資料品質。

如果標示為&#x200B;**必要**&#x200B;的欄因轉換問題而無效，則不會擷取該列。 啟用部分資料擷取時，您可以設定在整個流程失敗之前此類拒絕的臨界值。 如果取消的屬性並未影響任何結構描述層級的驗證，則會繼續內嵌列。

即使沒有任何轉換錯誤，任何無效列也會被拒絕。 例如，資料擷取流程可能會將傳遞對應（無轉換邏輯）對應到必填欄位，且該屬性沒有傳入值。 將拒絕此列。

### 如何在欄位中逸出特殊字元？

您可以使用`${...}`來逸出欄位中的特殊字元。 但是，此機制不支援包含具有句點(`.`)之欄位的JSON檔案。 與階層互動時，如果子屬性有句點(`.`)，您必須使用反斜線(`\`)來逸出特殊字元。 例如，`address`是包含屬性`street.name`的物件，然後可以將其稱為`address.street\.name`而非`address.street.name`。

### 計算欄位的最大長度是多少？

計算欄位的長度上限為4096個字元。

### 由於屬性驗證，我的內嵌失敗，但我在檔案中正確擁有該屬性。 到底有什麼問題嗎？

確保每個欄位的資料型別都和結構描述中定義的型別相符。 此外，必須遵守「必要」、「列舉」和「格式」等限制。

所擷取的資料必須符合Experience Platform中定義的Experience Data Model (XDM)結構。 如果屬性不符合結構描述中指定的預期型別或格式，擷取將會失敗。

如果使用「資料準備」函式，請確定轉換產生正確的屬性。 您可以在來源工作流程的設定過程中檢閱屬性。 在對應步驟中，選取&#x200B;**[!UICONTROL 新增欄位型別]**，然後選取&#x200B;**[!UICONTROL 新增計算欄位]**。 接下來，使用計算欄位介面來預覽每個函式。

### 如何從串流或批次擷取記錄中移除錯誤的資料值？

您可以使用「資料準備」對應介面，僅對映具有所需資料的資料欄，以執行資料欄層級篩選。 您也可以使用計算欄位，使用支援函式來轉換資料。

資料列層級篩選目前僅適用於[Adobe Analytics來源聯結器](../sources/tutorials/ui/create/adobe-applications/analytics.md#row-level-filtering)。

內嵌之後，您可以使用Data Distiller來清除、塑造及使用SQL操控資料。 不過，此程式需要刪除含有不良記錄的批次，並重新擷取根據SQL結果建立的新批次。

>[!IMPORTANT]
>
>* 資料湖：您只能透過刪除並重新內嵌記錄所在的批次來移除已內嵌的記錄。
>
>* 即時客戶設定檔：您可以擷取新記錄來覆寫以屬性為基礎的記錄，但無法移除體驗事件記錄。
>
>* Identity Service：您無法在Identity Service中完全移除記錄。 您將必須刪除整個設定檔，並使用設定檔刪除API重新上傳包含正確記錄的設定檔。

### 在GIF資料中使用計算欄位的最佳實務是什麼？

在來源資料對應至XDM結構的步驟中，您可以使用資料準備對應函式來建立新的計算欄位。

### 當您將Adobe Analytics資料匯入作為來源時，所建立的結構描述是否自動針對設定檔啟用？

設定檔不會自動設定Analytics資料。 設定來源聯結器後，您必須進入資料集和結構描述，並為設定檔擷取啟用它們。

在生產沙箱中建立Analytics來源資料流時，會建立兩個資料流：

* 此資料流會將13個月的歷史報表套裝資料回填至Data Lake。 此資料流會在回填完成時結束。
* 將即時資料傳送至資料湖和設定檔的資料流。 此資料流會持續執行。

### 如何使用資料準備函式，將對應物件中的一個值變成小寫？

您可以使用`map_get_values`函式擷取值，然後使用較低階函式將值變成小寫：

```shell
lower(map_get_values(mapObject, 'keyName'))
```

您可以使用相同的函式將地圖物件轉換為小寫。 不過，您不可以循環瀏覽整個對映，並將每個專案變成小寫。

### 我可以在巢狀方式中使用資料準備函式嗎？

可以，您可以在另一個函式中使用一個「資料準備」函式，以解決資料擷取期間複雜的資料準備功能。

例如，如果您想要根據特定條件將欄位定義為null ，則可以使用「iif」函式來檢查該欄位。 如果函式傳回`true`，則您可以使用&quot;nullify()&quot;，如果它傳回`false`，則您可以使用個別欄位。

如果marketing_type為欄位，則您可以使用「.equals」來檢查marketing_type欄位中的值，此值可巢狀內嵌「iif」函式。 如果它傳回`true`，則您可以使用「nullify()」函式，如下所示：

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

下列範例將說明如何使用iif、等於和空值來巢狀內嵌「資料準備」函式：

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| --- | --- | --- | --- | --- | --- |
| iif | 評估給定的布林運算式，並根據結果傳回指定的值。 | <ul><li>運算式： **必要**&#x200B;正在評估的布林運算式。</li><li>TRUE_VALUE： **必要**&#x200B;如果運算式評估為true，則傳回的值。</li><li>FALSE_VALUE： **必要**&#x200B;運算式評估為false時所傳回的值。</li></ul> | iif（運算式， TRUE_VALUE， FALSE_VALUE） | iif(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;)， &quot;True&quot;， &quot;False&quot;) | &quot;True&quot; |
| 等於 | 比較兩個字串以確認是否相等。 此函式區分大小寫。 | <ul><li>STRING1： **必要**&#x200B;您要比較的第一個字串。</li><li>STRING2： **必要**&#x200B;您要比較的第二個字串。 | STRING1&#x200B;。equals(&#x200B;STRING2) | &quot;string1&quot;。 &#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| 無效 | 將屬性的值設定為null。 當您不想將欄位複製到目標結構描述時，就應該使用此專案。 | | nullify() | nullify() | Null |

{style="table-layout:auto"}

以下是如何巢狀設定函式的範例（假設正在評估的欄位為「marketing_type」）。

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

接下來，假設您有下列三個欄位：

* marketing_type： （電子郵件、phyMail、推播、簡訊、電話）
* total_consents：數字範圍從4000到5500
* 日期：2024年2月至3月

您可以使用並巢狀內嵌上述三個函式，以操控三個欄位：

* iif(marketing_type.equals(&quot;email&quot;)， nullify()， iif(marketing_type.equals(&quot;push&quot;)， &quot;push-notification&quot;， marketing_type))
* iif(marketing_type.equals(&quot;phyMail&quot;)， nullify()， iif(marketing_type.equals(&quot;sms&quot;)， &quot;text-message&quot;， marketing_type))
* iif(total_consents > 5000， iif(marketing_type.equals(&quot;phone&quot;)， nullify()， marketing_type)， &quot;infirst-consents&quot;)
* iif(date.equals(&quot;3/21/24&quot;)， iif(marketing_type.equals(&quot;push&quot;)， nullify()， marketing_type)， &quot;not-March&quot;)
* iif(total_consents &lt; 4500， iif(marketing_type.equals(&quot;sms&quot;)， &quot;low-consent-sms&quot;， marketing_type)， &quot;high-consents&quot;)
* iif(marketing_type.equals(&quot;email&quot;)， iif(total_consents > 5000， nullify()， &quot;email-low-consents&quot;)， marketing_type)
* iif(marketing_type.equals(&quot;push&quot;)， iif(total_consents &lt; 4500， &quot;low-consent-push&quot;， nullify())， marketing_type)
* iif(total_consents >= 5500， iif(marketing_type.equals(&quot;phyMail&quot;)， nullify()， &quot;high-consents&quot;)， marketing_type)