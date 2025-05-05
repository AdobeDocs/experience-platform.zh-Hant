---
title: 資料擷取概觀
description: 本檔案主要介紹將資料擷取到Experience Platform的三種方式，並附有各自概述檔案的連結，以取得更詳細的資訊。
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: 0e484dffa38d454561f9d67c6bea92f426d3515d
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 1%

---

# 資料擷取概觀

在Adobe Experience Platform中，資料擷取是將資料從分類來源傳輸到儲存媒體的方式，可供組織存取、使用和分析。 Experience Platform中的資料擷取可以分組為兩個主要類別： **串流擷取**&#x200B;和&#x200B;**批次擷取**。

在串流和批次擷取底下，有多種不同的方法可用來將您的資料擷取至Experience Platform。 這些方法包括使用各種&#x200B;**來源**&#x200B;並連線到這些來源，然後將資料帶入Experience Platform。

閱讀本檔案以概略瞭解可將資料內嵌到Experience Platform中的許多不同方式。

<!-- Adobe Experience Platform brings data from multiple sources together in order to help marketers better understand the behavior of their customers. Adobe Experience Platform Data Ingestion represents the multiple methods by which Experience Platform ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream Experience Platform services. -->

## 串流擷取 {#streaming}

您可以使用串流擷取來即時從使用者端和伺服器端裝置傳送資料至Experience Platform。 Experience Platform支援使用資料輸入來串流傳入的體驗資料，這些資料會儲存在資料湖內已啟用串流的資料集中。 資料輸入可設定為自動驗證其收集的資料，確保資料來自信任的來源。

如需詳細資訊，請閱讀[串流擷取總覽](./streaming-ingestion/overview.md)。

## 批次擷取 {#batch}

在Experience Platform中，批次是指一段時間內收集並作為單一單位處理的一組資料。 資料集是由批次組成。 您可以使用批次內嵌將資料以批次檔案的形式內嵌到Experience Platform中。 擷取後，批次會提供中繼資料，說明成功擷取的記錄數，以及任何失敗的記錄和相關的錯誤訊息。

必須使用此方法來內嵌手動上傳的資料檔，例如一般CSV檔案（對應至XDM結構描述）和Parquet檔案。

如需詳細資訊，請閱讀[批次擷取總覽](./batch-ingestion/overview.md)。

## 來源 {#sources}

您也可以連線至Experience Platform來源以內嵌資料。 Experience Platform維護有各種不同資料來源的目錄，供您連結及擷取資料。 這些來源可以是原生Adobe應用程式，例如Adobe Analytics來源或Marketo Engage來源。 您也可以連線到協力廠商來源，例如[!DNL Amazon S3]來源和[!DNL Google Cloud Storage]來源。

來源會分組到不同的類別中，例如雲端儲存空間、資料庫和CRM系統。 指定的來源可能支援批次或串流擷取。

有了來源，您可以從許多不同的資料來源及不同的使用案例類別擷取資料。 此外，透過來源擷取的資料可讓您針對外部資料來源進行驗證、設定擷取排程並管理擷取輸送量。

如需詳細資訊，請閱讀[來源概觀](../sources/home.md)以取得更多資訊。

### ML輔助結構描述建立 {#ml-assisted-schema-creation}

若要快速整合新資料來源，您現在可以使用機器學習演演算法，從範例資料產生結構描述。 此自動化可簡化建立準確的結構描述、減少錯誤，並加速從資料收集到分析和深入分析的程式。

如需此工作流程的詳細資訊，請參閱[ML輔助結構描述建立指南](../xdm/ui/ml-assisted-schema-creation.md)。

## 資料準備 {#data-prep}

雖然資料準備不是擷取方法，但它是資料擷取流程的重要一環。 在建立資料流以將資料內嵌至Experience Platform之前，請使用資料準備函式對應、轉換及驗證資料與Experience Data Model (XDM)之間的連結。 在資料擷取程式進行期間，「資料準備」會顯示為Experience Platform使用者介面中的「對應」步驟。

如需詳細資訊，請閱讀[資料準備總覽](../data-prep/home.md)。

## 串流擷取方法 {#streaming-ingestion-methods}

下表概述您可用來將串流資料擷取至Experience Platform的各種方法。

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1123px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:31px; vertical-align:top; width:1123px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">串流來源</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">方法</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:401px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">常見使用案例</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">通訊協定</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:282px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">考量事項</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=zh-Hant" style="color:#0563c1; text-decoration:underline">Adobe Web/Mobile SDK</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">從網站和行動應用程式收集資料。</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">使用者端集合的偏好方法。</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">推播、HTTP、JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">運用單一SDK實作多個Adobe應用程式。</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sources/connectors/streaming/http" style="color:#0563c1; text-decoration:underline">HTTP API聯結器</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">來自串流來源、交易、相關客戶事件和訊號的集合。</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">推播、REST API、JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">原始或XDM資料會直接串流到集線器，不需要即時Edge分段或事件轉送。</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html?lang=zh-Hant" style="color:#0563c1; text-decoration:underline">[!DNL Edge Network] API</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">來自全域分散式[!DNL Edge Network]的串流來源、交易、相關客戶事件和訊號的集合。</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">推播、REST API、JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">資料已透過[!DNL Edge Network]串流處理。 在Edge上支援即時分段和事件轉送。 </span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=zh-Hant" style="color:#0563c1; text-decoration:underline">Adobe應用程式</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">從Adobe Analytics、Marketo Engage、Adobe Campaign Managed Services、Adobe Target、Adobe Audience Manager等應用程式擷取資料</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">推播、Source聯結器和API</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">建議方法是移轉至Web/行動SDK，而非使用傳統應用程式SDK。</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=zh-Hant" style="color:#0563c1; text-decoration:underline">串流來源</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">企業事件串流的擷取，通常用於將企業資料分享至多個下游應用程式。 </span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">推播、REST API、JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">資料會以JSON格式串流，且可以對應至XDM結構描述。</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sources/sdk/streaming-sdk/getting-started" style="color:#0563c1; text-decoration:underline">串流來源SDK</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">使用自助來源串流SDK的自助服務功能，將您自己的資料來源整合到Experience Platform來源目錄。</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">推播、HTTP API、JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">合作夥伴整合的串流來源範例包括：Braze、Pendo和RainFocus。</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>

## 批次擷取方法 {#batch-ingestion-methods}

下表概述您可用來將批次資料擷取至Experience Platform的各種方法。

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1105px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:37px; vertical-align:top; width:1105px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">批次來源</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">方法</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:397px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">常見使用案例</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">通訊協定</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:277px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">考量事項</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-platform/ingestion/batch/overview" style="color:#0563c1; text-decoration:underline">批次擷取API</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">從企業管理的佇列擷取。 如果您的資料需要在擷取前進行準備和格式化，請使用批次擷取。</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">推播、JSON或Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">必須管理要擷取的批次和檔案。</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sources/home" style="color:#0563c1; text-decoration:underline">批次來源</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">從雲端儲存空間、CRM和行銷自動化應用程式擷取資料的常見方法。</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">適合擷取大量歷史資料。</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">提取、CSV、JSON、Parquet</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Source擷取是根據預先設定的排程間隔。</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/cloud-storage/data-landing-zone.html?lang=zh-Hant" style="color:#0563c1; text-decoration:underline">資料登陸區域</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Adobe布建的雲端型檔案儲存。 您有權存取每個沙箱一個資料登陸區域容器。</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">將您的檔案推送至資料登陸區域，以便稍後擷取至Experience Platform。</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">推播、CSV、JSON、Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Experience Platform對上傳至資料登陸區域容器的所有檔案和資料夾強制實施嚴格的七天到期時間。 所有檔案和資料夾都會在七天後刪除。</span></span></span></li>
</ul>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/sdk/overview.html?lang=zh-Hant" style="color:#0563c1; text-decoration:underline">批次來源SDK</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">使用自助來源批次SDK的自助服務功能，將您自己的資料來源整合到Experience Platform來源目錄。</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">最適合使用合作夥伴聯結器，或針對設定企業聯結器提供量身打造的工作流程體驗。</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">提取、REST API、CSV或JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">合作夥伴整合的批次來源的範例包括：Mailchimp、OneTrust、Zendesk</span></span></span></li>
</ul>

<p> </p>
</td>
</tr>
</tbody>
</table>

## 後續步驟和其他資源

本檔案簡要介紹[!DNL Experience Platform]中[!DNL Data Ingestion]的不同方面。 請繼續閱讀每個擷取方法的概觀檔案，以熟悉其不同的功能、使用案例和最佳實務。 您也可以觀看下方的擷取概觀影片，以補充您的學習。 如需[!DNL Experience Platform]如何追蹤所擷取記錄的中繼資料的詳細資訊，請參閱[目錄服務總覽](../catalog/home.md)。

>[!WARNING]
>
>以下影片中使用的「統一設定檔」一詞已過期。 字詞[!DNL "Profile"]或[!DNL "Real-Time Customer Profile"]是[!DNL Experience Platform]檔案中使用的正確字詞。 請參閱檔案以瞭解最新功能。

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
