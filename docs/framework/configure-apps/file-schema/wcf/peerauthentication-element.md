---
title: "&lt;peerAuthentication&gt;-Element | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 09a8a9ff-e395-42f6-8ceb-9d44bdc1cbe1
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;peerAuthentication&gt;-Element
Gibt die Authentifizierungsoptionen für Peer\-to\-Peer\-Clients an.  
  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)] zur Peer\-to\-Peer\-Programmierung finden Sie unter [Peer\-to\-Peer\-Netzwerke](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md).  
  
## Syntax  
  
```  
  
<peerAuthentication  
customCertificateValidatorType = "namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"  
certificateValidationMode = "ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"  
revocationMode="NoCheck/Online/Offline"  
trustedStoreLocation="CurrentUser/LocalMachine"   
/>  
```  
  
## Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute, untergeordnete Elemente sowie übergeordnete Elemente beschrieben.  
  
### Attribute  
  
|Attribut|Beschreibung|  
|--------------|------------------|  
|`customCertificateValidatorType`|Optionale Zeichenfolge.  Ein Typ und eine Assembly, die zum Überprüfen eines benutzerdefinierten Typs verwendet werden.  Das Attribut muss festgelegt werden, wenn für `certificateValidationMode` der Wert `Custom` festgelegt wurde.|  
|`certifcateValidationMode`|Optionale Enumeration.  Gibt einen der drei für die Überprüfung von Anmeldeinformationen verwendeten Modi an.  Wenn dies auf `Custom` festgelegt wurde, muss auch ein `customCertificateValidator` bereitgestellt werden.  Die Standardeinstellung ist `ChainTrust`.|  
|`revocationMode`|Optionale Enumeration.  Einer der Modi zum Prüfen auf eine Liste gesperrter Zertifikate.  Die Standardeinstellung ist `Online`.|  
|`trustedStoreLocation`|Optionale Enumeration.  Einer der beiden Systemspeicherorte: `LocalMachine` oder `CurrentUser`.  Dieser Wert wird verwendet, wenn ein Dienstzertifikat mit dem Client ausgehandelt wird.  Die Prüfung wird anhand des **Vertrauenswürdige Personen**\-Speichers am angegebenen Speicherort durchgeführt.  Die Standardeinstellung ist `CurrentUser`.|  
  
## customCertificateValidatorType\-Attribut  
  
|Wert|Beschreibung|  
|----------|------------------|  
|Zeichenfolge|Gibt den vollständigen Typnamen und die Assembly sowie weitere Daten zum Suchen des Typs an.  Mindestens ein Namespace und Typname sind erforderlich.  Zu den optionalen Informationen zählen: Assemblyname, Versionsnummer, Kultur und Token des öffentlichen Schlüssels.|  
  
## certificateValidationMode\-Attribut  
  
|Wert|Beschreibung|  
|----------|------------------|  
|Enumeration|Einer der folgenden Werte: `None`, `PeerTrust`, `ChainTrust`, `PeerOrChainTrust`, `Custom`.  Die Standardeinstellung ist `ChainTrust`.<br /><br /> Weitere Informationen finden Sie unter [Verwenden von Zertifikaten](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).|  
  
## revocationMode\-Attribut  
  
|Wert|Beschreibung|  
|----------|------------------|  
|Enumeration|Einer der folgenden Werte: `NoCheck`, `Online`, `Offline`.  Die Standardeinstellung ist `Online`.<br /><br /> Weitere Informationen finden Sie unter [Verwenden von Zertifikaten](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).|  
  
## trustedStoreLocation\-Attribut  
  
|Wert|Beschreibung|  
|----------|------------------|  
|Enumeration|Einer der folgenden Werte: `LocalMachine` oder `CurrentUser`.  Die Standardeinstellung ist `CurrentUser`.  Wenn die Clientanwendung über ein Systemkonto ausgeführt wird, befindet sich das Zertifikat in der Regel in `LocalMachine`.  Wenn die Clientanwendung über ein Benutzerkonto ausgeführt wird, befindet sich das Zertifikat in der Regel in `CurrentUser`.|  
  
### Untergeordnete Elemente  
 Keine  
  
### Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<peer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/peer-of-clientcredentials-element.md)|Gibt Anmeldeinformationen an, die zur Authentifizierung des Clients bei einem Peerdienst verwendet werden.|  
  
## Hinweise  
 Das `<authentication>`\-Element entspricht der <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>\-Klasse.  Mit diesem Element wird ein Validierungssteuerelement angegeben, das bei Nachbar\-zu\-Nachbar\-Authentifizierung im Mesh aufgerufen wird.  Versucht ein neuer Peer, eine Nachbarverbindung herzustellen, übergibt er seine eigenen Anmeldeinformationen an den antwortenden Peer.  Das Validierungssteuerelement des antwortenden Peers wird aufgerufen, um die Anmeldeinformationen der Remotepartei zu überprüfen.  Bei jeder Herstellung einer Peerverbindung im Mesh werden beide Peers gegenseitig authentifziert, das heißt, die Validierungssteuerelemente werden an beiden Enden aufgerufen.  
  
## Beispiel  
 Mit dem folgenden Code wird der Zertifikatprüfmodus auf `PeerOrChainTrust` festgelegt.  
  
```  
<behaviors>  
 <endpointBehaviors>  
  <behavior name="MyEndpointBehavior">  
   <clientCredentials>  
    <peer>  
     <certificate findValue="www.contoso.com"   
                   storeLocation="LocalMachine"  
                   x509FindType="FindByIssuerName" />  
     <peerAuthentication   
          certificateValidationMode="PeerOrChainTrust" />  
     <messageSenderAuthentication certificateValidationMode="None" />  
    </peer>  
   </clientCredentials>  
  </behavior>  
</endpointBehaviors>  
```  
  
## Siehe auch  
 <xref:System.ServiceModel.Configuration.PeerCredentialElement>   
 <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>   
 <xref:System.ServiceModel.Security.PeerCredential.PeerAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.PeerCredentialElement.PeerAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.X509PeerCertificateAuthenticationElement>   
 [Verwenden von Zertifikaten](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Peer\-to\-Peer\-Netzwerke](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)   
 [Peer Channel Message Authentication](http://msdn.microsoft.com/de-de/80e73386-514e-4c30-9e4a-b9ca8c173a95)   
 [Peer Channel Custom Authentication](http://msdn.microsoft.com/de-de/4aa8a82e-41a8-48e2-8621-7e1cbabdca7c)   
 [Sichern von Peerkanalanwendungen](../../../../../docs/framework/wcf/feature-details/securing-peer-channel-applications.md)