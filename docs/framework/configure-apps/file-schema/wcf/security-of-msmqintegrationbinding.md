---
title: <security> von <msmqIntegrationBinding>
ms.date: 03/30/2017
ms.assetid: ae5c68a8-14a2-4c6e-b9e0-3e94e3e9135e
ms.openlocfilehash: e4f10ab994429c6cbb690caef38114b8340e6839
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399868"
---
# <a name="security-of-msmqintegrationbinding"></a>\<security> of \<msmqIntegrationBinding>
Definiert die Transportsicherheitseinstellungen für den Message Queuing (MSMQ)-Integrationskanal.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System. Service Model->** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<Bindungen >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<MsmqIntegrationBinding->** ](msmqintegrationbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<Bindungs >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<Sicherheits >**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<msmqIntegrationBinding>
  <binding>
    <security mode="None/Transport">
      <transport msmqAuthenticationMode="None/Windows/Certificate"
                 msmqEncryptionAlgorithm="RC4Stream/AES"
                 msmqProtectionLevel="None/Sign/EncryptAndSign"
                 msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />
      <message algorithmSuite="Aes128/Aes192/Aes256/Rsa15Aes128/ Rsa15Aes256/TripleDes"
               clientCredentialType="None/Windows/UserName/Certificate/CardSpace"
               defaultProtectionLevel="None/Sign/EncryptAndSign" />
    </security>
  </binding>
</msmqIntegrationBinding>
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|Modus|Gibt den Sicherheitstyp an, der Integrität, Vertraulichkeit und Authentifizierung mit dem Message Queuing-Integrationskanal steuert. Folgende Werte sind gültig:<br /><br /> Gar Dadurch wird die Sicherheit deaktiviert.<br />Personen Schutz und Authentifizierung werden vom Transport bereitgestellt. Dies bezieht sich auf die Nachrichtensicherheit zwischen beiden Warteschlangen-Managern. Es besteht keine Sicherheit zwischen der Anwendung und dem Warteschlangen-Manager. Vorhandene Msmq-Anwendungen sind mit diesem Typ des Sicherheitsmodus funktional äquivalent.<br /><br /> Der Standardwert ist `Transport`. Dieses Attribut ist vom Typ <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationSecurityMode>.|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<transport>](transport-of-msmqintegrationbinding.md)|Definiert die Sicherheitseinstellungen für Message Queuing-Integration und -Transport. Dieses Element ist vom Typ <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>.|  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|Das Bindungs Element der [ \<MsmqIntegrationBinding->](msmqintegrationbinding.md).|  
  
## <a name="see-also"></a>Siehe auch

- <xref:System.ServiceModel.Configuration.MsmqIntegrationSecurityElement>
- <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding.Security%2A>
- <xref:System.ServiceModel.Configuration.MsmqIntegrationBindingElement.Security%2A>
- <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationSecurity>
- [Warteschlangen in WCF](../../../wcf/feature-details/queues-in-wcf.md)
- [Sichern von Diensten und Clients](../../../wcf/feature-details/securing-services-and-clients.md)
- [Bindungen](../../../wcf/bindings.md)
- [Konfigurieren der vom System bereitgestellten Bindungen](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [Verwenden von Bindungen, um Dienste und Clients zu konfigurieren](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
- [\<msmqIntegrationBinding>](msmqintegrationbinding.md)
