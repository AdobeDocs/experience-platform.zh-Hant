---
title: Amazon Redshift Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Amazon Redshift連線至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: 719f1bca20d5118de14ebe324675bb0aab6161e8
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# [!DNL Amazon Redshift]來源

>[!IMPORTANT]
>
>- [!DNL Amazon Redshift]來源可在來源目錄中提供給已購買Real-Time CDP Ultimate的使用者。
>
>- 您現在可以在Amazon Web Services (AWS)上執行Adobe Experience Platform時使用[!DNL Amazon Redshift]來源。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../landing/multi-cloud.md)。


Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商資料庫擷取資料。 Platform可以連線到不同型別的資料庫，例如關聯式、NoSQL或資料倉儲。 支援的資料庫提供者包括[!DNL Amazon Redshift]。

## 在Azure上設定Experience Platform的[!DNL Amazon Redshift]來源 {#azure}

請依照下列步驟，瞭解如何在Azure上為Experience Platform設定[!DNL Amazon Redshift]帳戶。

### IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 在Amazon Web Services上設定Experience Platform的[!DNL Amazon Redshift]來源 {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../landing/multi-cloud.md)。

### AWS上連線的IP位址允許清單

您必須先將地區特定的IP位址新增至允許清單，才能將您的來源連線到AWS上的Experience Platform。 如需詳細資訊，請參閱[允許清單IP位址以連線至AWS](../../ip-address-allow-list.md)上的Experience Platform的指南。

## 使用API連線[!DNL Amazon Redshift]至平台

- [使用流量服務API連線Amazon Redshift至Experience Platform](../../tutorials/api/create/databases/redshift.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 使用UI連線[!DNL Amazon Redshift]至平台

- [在UI中建立Amazon Redshift來源連線](../../tutorials/ui/create/databases/redshift.md)
- [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)
