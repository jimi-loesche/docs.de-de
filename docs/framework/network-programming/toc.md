# [Netzwerkprogrammierung in .NET Framework](index.md)
## [Themen zur netzwerkprogrammierung](network-programming-how-to-topics.md)
## [Einführung in austauschbare Protokolle](introducing-pluggable-protocols.md)
## [Anfordern von Daten](requesting-data.md)
### [Erstellen von Internetanforderungen](creating-internet-requests.md)
### [Vorgehensweise: Anfordern einer Webseite und Abrufen der Ergebnisse als Stream](how-to-request-a-web-page-and-retrieve-the-results-as-a-stream.md)
### [Vorgehensweise: Anfordern von Daten mithilfe der WebRequest-Klasse](how-to-request-data-using-the-webrequest-class.md)
### [Vorgehensweise: Senden von Daten mithilfe der WebRequest-Klasse](how-to-send-data-using-the-webrequest-class.md)
### [Vorgehensweise: Abrufen eines protokollspezifischen WebResponse, das einem WebRequest entspricht](how-to-retrieve-a-protocol-specific-webresponse-that-matches-a-webrequest.md)
### [Verwenden von Streams im Netzwerk](using-streams-on-the-network.md)
### [Vornehmen von asynchronen Anforderungen](making-asynchronous-requests.md)
### [Behandeln von Fehlern](handling-errors.md)
## [Programmieren austauschbarer Protokolle](programming-pluggable-protocols.md)
### [Vorgehensweise: Registrieren eines benutzerdefinierten Protokolls mit WebRequest](how-to-register-a-custom-protocol-using-webrequest.md)
### [Vorgehensweise: Typumwandlung für ein WebRequest in zugriffsprotokollspezifische Eigenschaften](how-to-typecast-a-webrequest-to-access-protocol-specific-properties.md)
### [Deriving from WebRequest (Ableiten von WebRequest)](deriving-from-webrequest.md)
### [Ableiten von WebResponse](deriving-from-webresponse.md)
## [Verwenden von Anwendungsprotokollen](using-application-protocols.md)
### [HTTP](http.md)
#### [HttpListener](httplistener.md)
### [Vorgehensweise: Zugreifen auf HTTP-spezifische Eigenschaften](how-to-access-http-specific-properties.md)
### [Verwalten von Verbindungen](managing-connections.md)
#### [Connection Grouping (Verbindungsgruppierung)](connection-grouping.md)
#### [Vorgehensweise: Zuweisen von Benutzerinformationen zu Gruppenverbindungen](how-to-assign-user-information-to-group-connections.md)
### [TCP-UDP](tcp-udp.md)
#### [Mithilfe von TCP-Diensten](using-tcp-services.md)
#### [Mithilfe von UDP-Diensten](using-udp-services.md)
### [Sockets](sockets.md)
#### [Vorgehensweise: Erstellen eines Sockets](how-to-create-a-socket.md)
#### [Verwenden von Clientsockets](using-client-sockets.md)
##### [Verwenden eines synchronen Clientsockets](using-a-synchronous-client-socket.md)
##### [Verwenden von asynchronen Clientsockets](using-an-asynchronous-client-socket.md)
#### [Überwachen mit Sockets](listening-with-sockets.md)
##### [Verwenden eines synchronen Serversockets](using-a-synchronous-server-socket.md)
##### [Verwenden eines asynchronen Serversockets](using-an-asynchronous-server-socket.md)
#### [Socketcodebeispiele](socket-code-examples.md)
##### [Synchrone Clientsockets - Beispiel](synchronous-client-socket-example.md)
##### [Synchroner Serversocket, Beispiel](synchronous-server-socket-example.md)
##### [Asynchrone Clientsockets - Beispiel](asynchronous-client-socket-example.md)
##### [Asynchroner Serversocket, Beispiel](asynchronous-server-socket-example.md)
### [FTP](ftp.md)
#### [Vorgehensweise: Herunterladen von Dateien über FTP](how-to-download-files-with-ftp.md)
#### [Vorgehensweise: Hochladen von Dateien über FTP](how-to-upload-files-with-ftp.md)
#### [Vorgehensweise: Auflisten von Verzeichnisinhalt mit FTP](how-to-list-directory-contents-with-ftp.md)
### [Grundlegendes zu WebRequest-Problemen und-Ausnahmen](understanding-webrequest-problems-and-exceptions.md)
## [Internetprotokoll Version 6](internet-protocol-version-6.md)
### [IPv6-Adressierung](ipv6-addressing.md)
### [IPv6-Routing](ipv6-routing.md)
### [Automatische IPv6-Konfiguration](ipv6-auto-configuration.md)
### [Aktivieren und Deaktivieren von IPv6](enabling-and-disabling-ipv6.md)
### [Vorgehensweise: Ändern der Computerkonfigurationsdatei zum Aktivieren der IPv6-Unterstützung](how-to-modify-the-computer-configuration-file-to-enable-ipv6-support.md)
## [Konfigurieren von Internetanwendungen](configuring-internet-applications.md)
## [Netzwerkablaufverfolgung in .NET Framework](network-tracing.md)
### [Interpretieren von Netzwerkablaufverfolgung](interpreting-network-tracing.md)
### [Aktivieren der Netzwerkablaufverfolgung](enabling-network-tracing.md)
### [Vorgehensweise: Konfigurieren der Netzwerkablaufverfolgung](how-to-configure-network-tracing.md)
## [Cacheverwaltung für Netzwerkanwendungen](cache-management-for-network-applications.md)
### [Cacherichtlinie](cache-policy.md)
### [Speicherortbasierte Cacherichtlinien](location-based-cache-policies.md)
### [Zeitbasierte Cacherichtlinien](time-based-cache-policies.md)
#### [Cacherichtlinieninteraktion – maximales Alter und maximale Überalterung](cache-policy-interaction-maximum-age-and-maximum-staleness.md)
#### [Cacherichtlinieninteraktion – maximales Alter und minimale Aktualität](cache-policy-interaction-maximum-age-and-minimum-freshness.md)
### [Konfigurieren der Zwischenspeicherung in den Netzwerkanwendungen](configuring-caching-in-network-applications.md)
#### [Vorgehensweise: Festlegen einer speicherortbasierten Cacherichtlinie für eine Anwendung](how-to-set-a-location-based-cache-policy-for-an-application.md)
#### [Vorgehensweise: Festlegen der standardmäßigen zeitbasierten Cacherichtlinie für eine Anwendung](how-to-set-the-default-time-based-cache-policy-for-an-application.md)
#### [Vorgehensweise: Anpassen einer zeitbasierten Cacherichtlinie](how-to-customize-a-time-based-cache-policy.md)
#### [Vorgehensweise: Festlegen einer Cacherichtlinie für eine Anforderung](how-to-set-cache-policy-for-a-request.md)
## [Sicherheit in der Netzwerkprogrammierung](security-in-network-programming.md)
### [Using Secure Sockets Layer (Verwenden von Secure Sockets Layer)](using-secure-sockets-layer.md)
#### [Zertifikatauswahl und -überprüfung](certificate-selection-and-validation.md)
### [Internet Authentication (Internetauthentifizierung)](internet-authentication.md)
#### [Grundlegende und Digestauthentifizierung](basic-and-digest-authentication.md)
#### [NTLM- und Kerberos-Authentifizierung](ntlm-and-kerberos-authentication.md)
### [Web and Socket Permissions (Die Berechtigungen „Web“ und „Socket“)](web-and-socket-permissions.md)
## [Bewährte Methoden für System.Net-Klassen](best-practices-for-system-net-classes.md)
## [Zugreifen auf das Internet über einen Proxy](accessing-the-internet-through-a-proxy.md)
### [Proxykonfiguration](proxy-configuration.md)
### [Automatische Proxyerkennung](automatic-proxy-detection.md)
### [Vorgehensweise: Aktivieren von WebRequest zur Verwendung eines Proxys für die Internetkommunikation](how-to-enable-a-webrequest-to-use-a-proxy-to-communicate-with-the-internet.md)
### [Vorgehensweise: Überschreiben einer globalen Proxyauswahl](how-to-override-a-global-proxy-selection.md)
## [NetworkInformation](networkinformation.md)
### [Vorgehensweise: Erkennen von Netzwerkverfügbarkeit und Adressänderungen](how-to-detect-network-availability-and-address-changes.md)
### [Vorgehensweise: Abrufen von Schnittstellen- und Protokollinformationen](how-to-get-interface-and-protocol-information.md)
### [Vorgehensweise: Pingen eines Hosts](how-to-ping-a-host.md)
## [Änderungen am System.Uri-Namespace in Version 2.0](changes-to-the-system-uri-namespace-in-version-2-0.md)
## [International Resource Identifier-Unterstützung in System.Uri](international-resource-identifier-support-in-system-uri.md)
## [Erweiterungen der Socketleistung in Version 3.5](socket-performance-enhancements-in-version-3-5.md)
## [Peer Name Resolution-Protokoll (PNRP)](peer-name-resolution-protocol.md)
### [Peernamen und PNRP-IDs](peer-names-and-pnrp-ids.md)
### [Peernamenveröffentlichung und-Auflösung](peer-name-publication-and-resolution.md)
### [PNRP-Clouds](pnrp-clouds.md)
### [PNRP-Caches](pnrp-caches.md)
### [PNRP in der Anwendungsentwicklung](pnrp-in-application-development.md)
## [Peer-to-Peer-Zusammenarbeit](peer-to-peer-collaboration.md)
### [About the System.Net.PeerToPeer.Collaboration Namespace (Informationen zum System.NET.PeerToPeer.Kollaborations-Namespace)](about-the-system-net-peertopeer-collaboration-namespace.md)
### [Peer-zu-Peer-Netzwerkszenarien](peer-to-peer-networking-scenarios.md)
## [Änderungen an der NTLM-Authentifizierung für „HttpWebRequest“ in Version 3.5 SP1](changes-to-ntlm-authentication-for-httpwebrequest-in-version-3-5-sp1.md)
## [Integrierte Windows-Authentifizierung mit erweitertem Schutz](integrated-windows-authentication-with-extended-protection.md)
## [NAT-Durchlauf mit IPv6 und Teredo](nat-traversal-using-ipv6-and-teredo.md)
## [Netzwerkisolation für Windows Store-Apps](network-isolation-for-windows-store-apps.md)
## [Beispiele zur Netzwerkprogrammierung](network-programming-samples.md)
