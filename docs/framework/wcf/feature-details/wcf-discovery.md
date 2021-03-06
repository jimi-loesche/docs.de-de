---
title: "WCF-Suche | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Suche [WCF]"
  - "WCF [WCF], Suche"
  - "Windows Communication Foundation [WCF], Suche"
ms.assetid: 462c4913-f388-45a9-9042-28ae96a4e735
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# WCF-Suche
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] beschreibt die Unterstützung dafür, dass Dienste während der Laufzeit auf interoperable Weise erkennbar sind, indem das WS\-Discovery\-Protokoll verwendet wird.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienste können ihre Verfügbarkeit im Netzwerk mit einer Multicastnachricht oder für einen Suchproxyserver ankündigen.Clientanwendungen können ein Netzwerk oder einen Suchproxyserver durchsuchen, um Dienste zu ermitteln, die eine bestimmte Gruppe von Kriterien erfüllen.Die Themen in diesem Abschnitt enthalten eine Übersicht, und das Programmiermodell für diese Funktion wird ausführlich beschrieben.  
  
## In diesem Abschnitt  
 [Übersicht über die WCF\-Suche](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)  
 Bietet eine Übersicht über WS\-Discovery\-Unterstützung, die von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] bereitgestellt wird.  
  
 [Objektmodell der WCF\-Suche](../../../../docs/framework/wcf/feature-details/wcf-discovery-object-model.md)  
 Beschreibt die Klassen im Objektmodell und die Erweiterbarkeit der WS\-Discovery\-Unterstützung.  
  
 [Vorgehensweise: Programmgesteuertes Hinzufügen der Ermittelbarkeit zu einem WCF\-Dienst und \-Client](../../../../docs/framework/wcf/feature-details/how-to-programmatically-add-discoverability-to-a-wcf-service-and-client.md)  
 Beschreibt, wie Sie einen [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\-Dienst erkennbar machen.  
  
 [Implementieren eines Suchproxys](../../../../docs/framework/wcf/feature-details/implementing-a-discovery-proxy.md)  
 Beschreibt die Schritte, die erforderlich sind, um Folgendes zu implementieren: einen Suchproxy, einen erkennbaren Dienst, der sich beim Suchproxy registriert, und einen Client, der den Suchproxy zum Suchen nach dem erkennbaren Dienst verwendet.  
  
 [Versionskontrolle für die Suche](../../../../docs/framework/wcf/feature-details/discovery-versioning.md)  
 Bietet eine kurze Übersicht über eine Prototypimplementierung einiger neuer Suchfunktionen.Enthält außerdem eine Übersicht über die Auswahl der zu verwendenden Suchversion.  
  
 [Konfigurieren der Suche in einer Konfigurationsdatei](../../../../docs/framework/wcf/feature-details/configuring-discovery-in-a-configuration-file.md)  
 Beschreibt, wie Sie die Suche in der Konfiguration konfigurieren.  
  
 [Verwenden des Suchclientchannels](../../../../docs/framework/wcf/feature-details/using-the-discovery-client-channel.md)  
 Beschreibt, wie Sie beim Schreiben einer [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Clientanwendung einen Suchclientkanal verwenden.