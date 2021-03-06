---
title: "Erstellen von WCF AJAX-Diensten ohne ASP.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba4a7d1b-e277-4978-9f62-37684e6dc934
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Erstellen von WCF AJAX-Diensten ohne ASP.NET
Auf [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] AJAX\-Dienste kann von jeder JavaScript\-aktivierten Webseite zugegriffen werden, ohne dass ASP.NET AJAX erforderlich wäre.  In diesem Thema wird beschrieben, wie ein solcher [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienst erstellt wird.  
  
 Hinweise für das Verwenden von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] mit ASP.NET AJAX finden Sie unter [Erstellen von WCF\-Diensten für ASP.NET AJAX](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md).  
  
 Zur Erstellung eines funktionsfähigen [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] AJAX\-Diensts sind drei Schritte erforderlich:  
  
-   Erstellen eines AJAX\-Endpunkts, auf den vom Browser aus zugegriffen werden kann.  
  
-   Erstellen eines AJAX\-kompatiblen Dienstvertrags.  
  
-   Zugreifen auf den WCF AJAX\-Dienst.  
  
## Erstellen eines AJAX\-Endpunkts  
 Der einfachste Weg, AJAX\-Unterstützunmg in einem [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienst zu aktivieren, besteht darin, in der dem Dienst zugeordneten SVC\-Datei die <xref:System.ServiceModel.Activation.WebServiceHostFactory> zu verwenden, wie im folgenden Beispiel gezeigt.  
  
```  
<%ServiceHost   
    language=c#  
    Debug="true"  
    Service="Microsoft.Ajax.Samples.CityService"  
    Factory=System.ServiceModel.Activation.WebServiceHostFactory  
%>  
```  
  
 Alternativ können Sie auch die Konfiguration verwenden, um einen AJAX\-Endpunkt hinzuzufügen.  Verwenden Sie die <xref:System.ServiceModel.WebHttpBinding> des Dienstendpunkts, und konfigurieren Sie diesen Endpunkt mit dem <xref:System.ServiceModel.Description.WebHttpBehavior>, wie im folgenden Codeausschnitt dargestellt.  
  
```  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="AjaxBehavior">  
          <webHttp/>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <services>  
      <service name="Microsoft.Ajax.Samples.CityService">  
        <endpoint   
          address="ajaxEndpoint"  
          behaviorConfiguration="AjaxBehavior"  
          binding="webHttpBinding"  
          contract="Microsoft.Ajax.Samples.ICityService" />  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
 Ein funktionsfähiges Beispiel finden Sie unter [AJAX\-Dienst mit JSON und XML](../../../../docs/framework/wcf/samples/ajax-service-with-json-and-xml-sample.md).  
  
## Erstellen eines AJAX\-kompatiblen Dienstvertrags  
 Standardmäßig geben die über einem AJAX\-Endpunkt verfügbar gemachten Dienstverträge Daten im XML\-Format zurück.  Ebenso standardmäßig kann auf die Dienstvorgänge über HTTP POST\-Anforderungen mit URLs zugegriffen werden, die die Endpunktadresse gefolgt vom Vorgangsnamen enthalten, wie im folgenden Beispiel gezeigt.  
  
```  
[OperationContract]  
string[] GetCities(string firstLetters);  
```  
  
 Auf diesen Vorgang kann über HTTP POST für `http://serviceaddress/endpointaddress/GetCities` zugegriffen werden. Es wird eine XML\-Nachricht zurückgegeben.  
  
 Sie können das vollständige Webprogrammiermodell verwenden, um diese grundlegenden Aspekte anzupassen.  Sie können beispielsweise die Attribute <xref:System.ServiceModel.Web.WebGetAttribute> oder <xref:System.ServiceModel.Web.WebInvokeAttribute> verwenden, um zu steuern, auf welche HTTP\-Verben der Vorgang reagiert, oder die Eigenschaft `UriTemplate` dieser jeweiligen Attribute verwenden, um benutzerdefinierte URIs anzugeben usw.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] dem folgenden Thema: [WCF\-Web\-HTTP\-Programmiermodell](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md).  
  
 Das JSON\-Datenformat wird oft in AJAX\-Diensten verwendet.  Um einen Vorgang zu erstellen, der JSON statt XML zurückgibt, legen Sie die <xref:System.ServiceModel.Web.WebGetAttribute.ResponseFormat%2A>\-Eigenschaft \(oder die <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A>\-Eigenschaft\) auf <xref:System.ServiceModel.Web.WebMessageFormat> fest.  Im Thema [Eigenständige JSON\-Serialisierung.](../../../../docs/framework/wcf/feature-details/stand-alone-json-serialization.md) wird gezeigt, wie die integrierten .NET\-Typen und Datenvertragstypen JSON zugeordnet werden.  
  
 Normalerweise bestehen JSON\-Anforderungen und \-Antworten aus nur einem Element.  Für den vorangehenden `GetCities`\-Vorgang ähnelt die Anforderung der folgenden Anweisung.  
  
```  
“na”  
```  
  
 Die Antwort auf diese Anforderung ähnelt der folgenden Anweisung.  
  
```  
[“Nairobi”, “Naples”, “Nashville”]  
```  
  
 Wenn der Vorgang einen zusätzlichen Parameter annimmt, muss der Anforderungsstil auf "wrapped" festgelegt werden, damit beide Parameter einem einzigen JSON\-Objekt zugeordnet werden.  Ein Beispiel für eine JSON\-Nachricht in diesem Stil finden Sie im folgenden Beispiel.  
  
```  
{“firstLetters”: “na”, “maxNumber”: 2}  
```  
  
 Der folgende Vertrag akzeptiert diese Nachricht.  
  
```  
[WebInvoke(BodyStyle=WebMessageBodyStyle.WrappedRequest, ResponseFormat=WebMessageFormat.Json)]  
[OperationContract]  
string[] GetCities(string firstLetters, int maxNumber);  
```  
  
## Zugreifen auf AJAX\-Dienste  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]AJAX\-Endpunkte akzeptieren immer sowohl JSON\- als auch XML\-Anforderungen.  
  
 HTTP POST\-Anforderungen mit dem Inhaltstyp "application\/json" werden als JSON behandelt, und jene mit einem XML angebenden Inhaltstyp \(z.&\#160;B. "text\/xml"\) werden als XML behandelt.  
  
 HTTP GET\-Anforderungen enthalten alle Anforderungsparameter in der URL selbst.  
  
 Es obliegt dem Benutzer zu entscheiden, wie die HTTP\-Anforderung für den Endpunkt erstellt wird.  Der Benutzer kann umfassend steuern, wie das den Text der Anforderung bildende JSON erstellt wird.  Ein Beispiel für die Erstellung einer Anforderung mithilfe von JavaScript finden Sie unter [AJAX\-Dienst mit JSON und XML](../../../../docs/framework/wcf/samples/ajax-service-with-json-and-xml-sample.md).