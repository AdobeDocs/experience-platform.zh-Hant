---
title: Adobe Experience Platform Web SDK擴充功能中的動作型別
description: 瞭解Adobe Experience Platform Web SDK標籤擴充功能所提供的各種動作型別。
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 2%

---


# 動作類型

在您設定 [Adobe Experience Platform Web SDK標籤擴充功能](web-sdk-extension-configuration.md)，您必須設定動作型別。

此頁面說明支援的動作型別。 [Adobe Experience Platform Web SDK標籤擴充功能](web-sdk-extension-configuration.md).

## 傳送事件 {#send-event}

傳送事件給Adobe [!DNL Experience Platform] 以便Adobe Experience Platform可以收集您傳送的資料，並對該資訊採取行動。 選取執行個體（如果有多個執行個體）。 任何您想要傳送的資料都可在 **[!UICONTROL XDM資料]** 欄位。 使用符合XDM結構描述的JSON物件。 您可在您的頁面上或透過以下方式建立此物件： **[!UICONTROL 自訂程式碼]** **[!UICONTROL 資料元素]**.

「傳送事件」動作型別中還有其他欄位，根據您的實作而定，這些欄位也可能會相當實用。 請注意，這些欄位都是選用欄位。

- **型別：** 此欄位可讓您指定將記錄在XDM結構描述中的事件型別。 另請參閱 [`type`](/help/web-sdk/commands/sendevent/type.md) 在 `sendEvent` 命令以取得詳細資訊。
- **資料：** 使用此欄位可傳送不符合XDM結構描述的資料。 如果您嘗試更新Adobe Target設定檔或傳送Target Recommendations屬性，此欄位會很有用。 另請參閱 [`data`](/help/web-sdk/commands/sendevent/data.md) 在 `sendEvent` 命令以取得詳細資訊。<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **資料集ID：** 如果您需要傳送資料至資料流中所指定資料集以外的資料集，您可以在此處指定該資料集ID。
- **檔案將解除安裝：** 如果您想要確保事件可到達伺服器，即使使用者導覽離開頁面，請檢查 **[!UICONTROL 檔案將解除安裝]** 核取方塊。 這可讓事件連線至伺服器，但會忽略回應。
- **呈現視覺個人化決定：** 如果您想在頁面上呈現個人化內容，請檢查 **[!UICONTROL 呈現視覺個人化決定]** 核取方塊。 如有需要，您也可以指定決定範圍及/或曲面。 請參閱 [個人化檔案](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) 以取得有關呈現個人化內容的詳細資訊。

## 設定同意 {#set-consent}

在您收到使用者的同意後，必須使用「設定同意」動作型別，將此同意傳達Adobe Experience Platform Web SDK。 目前支援「Adobe」和「IAB TCF」等兩種標準。另請參閱 [支援客戶同意偏好設定](/help/web-sdk/consent/supporting-consent.md). 使用Adobe版本2.0時，僅支援資料元素值。 您將需要建立可解析為同意物件的資料元素。

在此動作中，系統也會提供選填欄位，供您加入身分對應，以便在收到同意後同步身分資料。 同意設為「擱置中」或「退出」時，同步會很有用，因為同意呼叫可能是第一個要觸發的呼叫。

## 更新變數 {#update-variable}

使用此動作來修改作為事件結果的XDM物件。 此動作旨在建立物件，以便稍後從 **[!UICONTROL 傳送事件]** 動作，記錄事件XDM物件。

若要使用此動作型別，您必須定義 [變數](data-element-types.md#variable) 資料元素。 選擇要修改的變數資料元素後，會出現類似編輯器的編輯器 [xdm物件](data-element-types.md#xdm-object) 資料元素。

![](assets/update-variable.png)

用於編輯器的XDM結構描述是在 [!UICONTROL 變數] 資料元素。 您可以按一下左方樹狀結構中的其中一個屬性，然後修改右方的值，來設定物件的一或多個屬性。例如，在下方的熒幕擷圖中， productedBy屬性已設定為資料元素「Producted by data element」。

![](assets/update-variable-set-property.png)

更新變數動作中的編輯器與XDM物件資料元素中的編輯器有一些差異。 首先，更新變數動作具有標示為「xdm」的根層級專案。 如果按一下此專案，您可以指定要用來設定整個物件的資料元素。 其次，更新變數動作有核取方塊可清除xdm物件的資料。 按一下左側的其中一個屬性，然後核取右側的核取方塊以清除值。 這會在設定變數的任何值之前，清除目前的值。

## 後續步驟 {#next-steps}

閱讀本文後，您應該更瞭解如何設定動作。 接下來，閱讀如何 [設定您的資料元素型別](data-element-types.md).
