---
title: 'Vorgehensweise: Konfigurieren von WCF-Diensten für die Zusammenarbeit mit WSE3.0-Clients'
ms.date: 03/30/2017
ms.assetid: 0f38c4a0-49a6-437c-bdde-ad1d138d3c4a
ms.openlocfilehash: 0349c9ba76b3f240bf98daa0e095b415bc98a87c
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045934"
---
# <a name="how-to-configure-wcf-services-to-interoperate-with-wse-30-clients"></a>Vorgehensweise: Konfigurieren von WCF-Diensten für die Zusammenarbeit mit WSE3.0-Clients

Windows Communication Foundation (WCF)-Dienste sind auf Wire-Ebene kompatibel mit Webdienst Erweiterungen 3,0 für Microsoft .net (WSE)-Clients, wenn WCF-Dienste für die Verwendung der WS-Adressierungs Spezifikation vom August 2004 konfiguriert sind.

### <a name="to-enable-a-wcf-service-to-interoperate-with-wse-30-clients"></a>So konfigurieren Sie einen WCF-Dienst für die Zusammenarbeit mit WSE3.0-Clients

1. Definieren Sie eine benutzerdefinierte Bindung für den WCF-Dienst.

    Es muss eine benutzerdefinierte Bindung erstellt werden, um anzugeben, dass die Version der WS-Adressierungsspezifikation vom August 2004 für die Nachrichtencodierung verwendet wird.

    1. Fügen Sie [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) [dem Bindungs\<>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) der Konfigurationsdatei des dienstangs einen untergeordneten CustomBinding-> hinzu.

    2. Geben Sie einen Namen für die Bindung an, indem Sie der [ \<CustomBinding->](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) eine [ \<Bindungs >](../../../../docs/framework/misc/binding.md) hinzu `name` fügen und das-Attribut festlegen.

    3. Geben Sie einen Authentifizierungsmodus und die Version der WS-Sicherheitsspezifikationen an, die zum Sichern von Nachrichten verwendet werden, die mit WSE 3,0 kompatibel sind, indem Sie der [ \<Bindungs >](../../../../docs/framework/misc/binding.md)ein [ \<untergeordnetes Sicherheits >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) hinzufügen.

        Um den Authentifizierungsmodus festzulegen, legen `authenticationMode` Sie das-Attribut [ \<der Sicherheits >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)fest. Ein Authentifizierungsmodus ist mit einer sofort verwendbaren WSE 3.0-Sicherheitsassertion vergleichbar. In der folgenden Tabelle sind die Authentifizierungs Modi in WCF den schlüsselfertigen Sicherheits Assertionen in WSE 3,0 zugeordnet.

        |WCF-Authentifizierungsmodus|Sofort verwendbare WSE 3.0-Sicherheitsassertion|
        |-----------------------------|----------------------------------------|
        |<xref:System.ServiceModel.Configuration.AuthenticationMode.AnonymousForCertificate>|`anonymousForCertificateSecurity`|
        |<xref:System.ServiceModel.Configuration.AuthenticationMode.Kerberos>|`kerberosSecurity`|
        |<xref:System.ServiceModel.Configuration.AuthenticationMode.MutualCertificate>|`mutualCertificate10Security`*|
        |<xref:System.ServiceModel.Configuration.AuthenticationMode.MutualCertificate>|`mutualCertificate11Security`*|
        |<xref:System.ServiceModel.Configuration.AuthenticationMode.UserNameOverTransport>|`usernameOverTransportSecurity`|
        |<xref:System.ServiceModel.Configuration.AuthenticationMode.UserNameForCertificate>|`usernameForCertificateSecurity`|

        \*Einer der Hauptunterschiede zwischen der `mutualCertificate10Security` und `mutualCertificate11Security` der sofort einsetzbaren Sicherheits Assertionen ist die Version der WS-Security-Spezifikation, die von WSE zum Sichern der SOAP-Nachrichten verwendet wird. Für `mutualCertificate10Security` wird WS-Security 1.0 verwendet, wohingegen WS-Security 1.1 für `mutualCertificate11Security` verwendet wird. Für WCF wird die Version der WS-Security-Spezifikation im `messageSecurityVersion` -Attribut [ \<des Sicherheits >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)angegeben.

        Um die Version der WS-Security-Spezifikation festzulegen, die zum Sichern von SOAP-Nachrichten `messageSecurityVersion` verwendet wird, legen Sie das-Attribut [ \<der Sicherheits >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)fest. Für die Zusammenarbeit mit WSE 3.0 legen Sie den Wert des `messageSecurityVersion`-Attributs auf <xref:System.ServiceModel.MessageSecurityVersion.WSSecurity11WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11BasicSecurityProfile10%2A> fest.

    4. Geben Sie an, dass die Version vom August 2004 der WS-Adressierungs Spezifikation von WCF verwendet wird, indem Sie eine [ \<textMessageEncoding->](../../../../docs/framework/configure-apps/file-schema/wcf/textmessageencoding.md) hinzu <xref:System.ServiceModel.Channels.MessageVersion.Soap11WSAddressingAugust2004%2A>fügen und den `messageVersion` Wert auf festlegen.

        > [!NOTE]
        > Wenn Sie SOAP 1.2 verwenden, legen Sie das `messageVersion`-Attribut auf <xref:System.ServiceModel.Channels.MessageVersion.Soap12WSAddressingAugust2004%2A> fest.

2. Geben Sie an, dass der Dienst die benutzerdefinierte Bindung verwendet.

    1. Legen Sie `binding` das-Attribut [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md) des Endpunkts > `customBinding`-Elements auf fest.

    2. Legen Sie `bindingConfiguration` das-Attribut [ \<des Endpunkts >](../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md) - `name` Elements auf den [ \<](../../../../docs/framework/misc/binding.md) Wert fest, der im-Attribut der Bindungs > für die benutzerdefinierte Bindung angegeben ist.

## <a name="example"></a>Beispiel

Das folgende Codebeispiel gibt an, dass `Service.HelloWorldService` eine benutzerdefinierte Bindung zur Zusammenarbeit mit WSE 3.0-Clients verwendet. Die benutzerdefinierte Bindung gibt an, dass die Version der WS-Adressierungsspezifikation vom August 2004 und die Spezifikationen von WS-Security 1.1 zum Codieren der ausgetauschten Nachrichten verwendet werden. Die Nachrichten werden mit dem <xref:System.ServiceModel.Configuration.AuthenticationMode.AnonymousForCertificate>-Authentifizierungsmodus geschützt.

```xml
<configuration>
  <system.serviceModel>
    <services>
      <service
        behaviorConfiguration="ServiceBehavior"
        name="Service.HelloWorldService">
        <endpoint binding="customBinding" address=""
          bindingConfiguration="ServiceBinding"
          contract="Service.IHelloWorld"></endpoint>
      </service>
    </services>

    <bindings>
      <customBinding>
        <binding name="ServiceBinding">
          <security authenticationMode="AnonymousForCertificate"
                  messageProtectionOrder="SignBeforeEncrypt"
                  messageSecurityVersion="WSSecurity11WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11BasicSecurityProfile10"
                  requireDerivedKeys="false">
          </security>
          <textMessageEncoding messageVersion ="Soap11WSAddressingAugust2004"></textMessageEncoding>
          <httpTransport/>
        </binding>
      </customBinding>
    </bindings>
    <behaviors>
      <behavior name="ServiceBehavior" returnUnknownExceptionsAsFaults="true">
        <serviceCredentials>
          <serviceCertificate findValue="CN=WCFQuickstartServer" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectDistinguishedName"/>
        </serviceCredentials>
      </behavior>
    </behaviors>
  </system.serviceModel>
</configuration>
```

## <a name="see-also"></a>Siehe auch

- [Vorgehensweise: Anpassen einer vom System bereitgestellten Bindung](../../../../docs/framework/wcf/extending/how-to-customize-a-system-provided-binding.md)
