---
keywords: RTCDP; CDP;B2B Edition；即時客戶資料平台；即時客戶資料平台；即時CDP;b2b; CDP；客戶AI
title: Real-time CDP B2B Edition概述
seo-title: Real-time Customer Data Platform B2B Edition overview
description: 即時客戶資料平台B2B版本帳戶概觀
seo-description: Overview of Real-time Customer Data Platform B2B Edition Account
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: e54bd747a332e37920e24ce07602470f8ad74231
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 1%

---

# 即時客戶資料平台B2B版本概觀

>[!IMPORTANT]
>
>Real-time CDP B2B Edition目前處於測試版。 文件和功能可能會有所變更。

Real-time CDP B2B Edition以Real-time Customer Data Platform(Real-time CDP)為基礎，專門為以業務對業務服務模式運營的營銷人員而構建。 它匯集了來自多個來源的資料，並將其結合為人員和帳戶設定檔的單一檢視。 此統一的資料可讓行銷人員精確鎖定特定對象，並參與所有可用管道中的這些對象。

對各種Adobe Experience Platform功能進行了改進，將即時CDP B2B Edition與其B2C對應版本區分開來。 其中包括針對B2B使用案例改善Experience Data Model(XDM)、升級為身分解析和設定檔分段，以及自訂的[!DNL Marketo Engage]連接器和目的地。 [!DNL Marketo]連接器可讓B2B品牌將其業界領先的B2B參與資料與行為資訊連結，以培育銷售機會並增強以帳戶為基礎的行銷操作。

使用Real-time CDP B2B Edition，您可以：

* 將從多個來源收集的資料合併成單一檢視，以建立整體的人員和帳戶設定檔。
* 從統一帳戶設定檔的集中存放區，擴充、劃分及匯出所有跨來源資料。
* 使用集中化流程每個步驟都提供的資料管理工具來管理您的資料，以確保您的資料符合法律法規和業務策略。

有關為即時CDP B2B Edition所做改進的更全面的詳細資訊，分為以下幾節。

## XDM

Real-time CDP B2B Edition提供數種新的XDM架構類別、欄位群組和關係類型，可專門用於B2B用途擷取和建構您的資料。 如需這些增強功能的細目，請參閱即時CDP B2B版本](./schemas/b2b.md)中的[XDM概觀。

透過使用預先設定的B2B結構，您可以將資料匯入標準化、可操作的結構。 許多新結構類幾乎直接對應至主流CRM中遇到的結構類別，例如[!DNL Salesforce]、[!DNL Microsoft Dynamics]、[!DNL Marketo]和其他B2B資料來源。 使用即時CDP B2B Edition，您可以以簡單明瞭的方式將B2B來源的資料帶入Platform，並取得易於稽核的結果。

這些XDM增強功能可讓您透過B2B為中心的來源和目的地，以更佳的方式擷取和啟動資料，並針對更多種化、更靈活的使用案例，改善資料統一和呈現方式。

## 身分解析

定義結構並擷取符合這些結構的資料後，即時CDP B2B Edition會透過功能強大的即時身分解析系統，識別代表真實人員和企業的來源記錄。

身份解析系統提供下列功能：

* B2B和B2C人員記錄組合
* 多級帳戶階層
* 多對多、人員對帳戶的關係
* 人員和帳戶身分可即時解析

已擴大身份解決系統，以支援更多層面的人員分類。 該系統允許將人員識別為商機中的銷售機會以及客戶。

由來源CRM同步並透過系統內多個路徑連接的帳戶記錄，會由Platform合併在一起。 該系統將那些與業務機會相關的人和那些記錄為客戶的人聚集在一起，但如果他們是可識別的，他們之間的區別也能夠保留。

匹配的標識符用於連結在一起並合併來自多個系統的帳戶記錄。 在整個過程中會保留帳戶層次結構。 使用獨特點會仔細檢查某人是否與某個帳戶相關聯，並在需要時提供將其與帳戶分開的能力。

## 設定檔與區段

一旦即時CDP B2B Edition擷取了與人員、公司、屬性和行為相關的資料和已解析的身分識別，該資料就會用來建立設定檔。 然後，這些設定檔可以分段為可瀏覽的對象，然後可以啟動至各種目的地。

正確實作時，系統會使用唯一的主要識別碼來追蹤使用者，而非可能變更的屬性，例如電子郵件地址。 這表示當有人變更工作時，系統仍會依循這些工作。 該人員仍是同一實體，但會連結至新帳戶。 此原生功能提供擴展至新帳戶的絕佳向量，因為系統會以個人身分跟隨這些人，包括其所有屬性和行為。

## B2B來源

Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 [!DNL Marketo]來源可讓您將B2B資料串流至Platform，並使用與平台連接的應用程式讓此資料保持最新。 它支援任何數量的[!DNL Marketo]例項（對具有多個例項的大型公司有利），並提取至合併資料的單一IMS組織。

>[!NOTE]
>
>[!DNL Marketo]源為&#x200B;**不**，需要此源才能使用即時CDP B2B版本。

如需Marketo和將B2B資料匯入Platform的詳細資訊，請參閱即時CDP B2B版檔案中的來源。

<!-- PLACEHOLDER [sources in Real-time CDP B2B Edition](./sources/b2b) -->

## B2B目的地

所有Experience Platform目的地（如[!DNL Google]、[!DNL Linkedin]或[!DNL Facebook]）均可供即時CDP B2B Edition使用，且完全受支援。 此外也有一個[!DNL Marketo Engage]目的地，可從[!DNL Marketo]或從Platform流出資料，並以受眾形式提供資料。

[!DNL Marketo]目的地提供順暢且快速的方式，可將資訊從Experience Platform提取至[!DNL Marketo]。 目的地可讓行銷人員將Adobe Experience Platform中建立的區段推送至[!DNL Marketo]。 在[!DNL Marketo]中，這些對象隨後可作為靜態清單使用。

對於擁有多個CRM的公司，即時CDP B2B Edition提供選項，可設定目標連接器，以區隔[!DNL Marketo]或CRM的例項。 如有需要，您可以設定每個例項的目的地連接器，並個別傳送對象至每個CRM例項。

## 後續步驟

現在您更清楚了解即時CDP B2B Edition為行銷人員提供的優點，以及它與即時CDP之間的差異，便能了解如何將這些功能套用至您自己的IMS組織。

<!-- PLACEHOLDER [example use case for Real-time CDP B2B Edition]() -->

要了解Real-time CDP B2B Edition如何使您的企業對企業服務模型受益，請參見Real-time CDP B2B Edition的示例使用案例。 或者，您也可以參閱即時客戶資料平台B2B版本](./schemas/b2b.md)中的[結構檔案，以取得有關建立結構和定義基本B2B資料實體關係的更具體指引。
