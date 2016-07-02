# Amazon News – Pacotão de Junho

Passamos para o segundo semestre de 2016 e a Amazon continua a todo vapor, anunciando novas funcionalidades ou melhorias no alcance das que já existem. Neste mês de Junho, diversas novidades foram apresentadas e vou tentar cobrir neste post os principais pontos, como o suporte do _Amazon OpsWorks_ para trabalhar com o CentOS, a disponibilização do serviço de *Last Accessed Data* do Amazon IAM para a região *South America* (Sao Paulo) e anúncio de suporte do Amazon Cognito à SAML providers.
  
### OpsWorks e CentOS

Agora o OpsWorks passa a dar suporte a instâncias e até mesmo servidores fora da sua stack (on-premises) rodando CentOS. O que isso significa na prática é que uma **GRANDE** parcela do mercado (só no mercado de WebServers usando Linux, por exemplo, [CentOS representa mais de 20%](https://w3techs.com/technologies/details/os-linux/all/all)), além de quem utiliza a distribuição para seus servidores, será beneficiada pelo anúncio.

<p align="center"><img src="https://dl.dropboxusercontent.com/s/iyit6uo2dxvkqnv/Screen%20Shot%202016-07-01%20at%208.11.42%20AM.png?dl=0"Market Share - CentOS"></p>

O suporte inicial prevê somente a versão 7 do sistema operacional amigo do SysAdmin e possíveis atualizações nos próximos anos. A previsão é de dois em dois anos. A versão do Chef suportada neste caso é somente a versão 12, então vamos tomar um pouco de cuidado com a versão utilizada atualmente em sua stack.

<p align="center"><img src="https://dl.dropboxusercontent.com/s/6mcg73ayvawnayb/Screen%20Shot%202016-06-28%20at%2010.15.41%20PM.png?dl=0"OpsWorks - Centos"></p>

Para mais informações sobre o suporte a Centos e possíveis atualizações, verifique o [link](https://docs.aws.amazon.com/opsworks/latest/userguide/workinginstances-os-linux.html#workinginstances-os-linux-centos) e usufrua de mais uma AMI preparada para rodar o OpsWorks.

---  
  

### Last Accessed Data para a região South America

A Amazon anunciou na semana passada o suporte da função para duas novas regiões, *South America* (São Paulo) e *Asia Pacific* (Seul), além das oito já suportadas. Isso já era esperado desde que a compania informou o início do rastreio das informações de acesso no final de 2015 e início de 2016. 

O serviço de [__Last Accessed Data__](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_access-advisor.html?icmpid=docs_iam_console) permite obter informações sobre as tentativas de acessos de usuários e roles do IAM aos serviços da AWS. Na prática, informações como usuários, grupos e roles tentando acessar recursos permitem apromorar nas *policies* do seu IAM e manter as boas práticas indicadas pela Amazon baseadas em [menor privilégio](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege).

Agora, quando estiver na visualização de um usuário, grupo ou role, uma nova aba chamada __Access Advisor__ é apresentada à direita, onde são expostas todas as tentativas de acesso daquela entidade aos recursos da AWS, indepententemente da forma de acesso e provenientes de acesso via console ou chamadas de API. 

<p align="center"><img src="https://dl.dropboxusercontent.com/s/s4otsk5ybalpfg6/Policy-centric-image-1ab.png?dl=0"IAM - Last Accessed Data"></p>

*Imagem retirada do post de Kai Zhao no blog de segurança da AWS. Para conferir o post na íntegra, [clique aqui](https://blogs.aws.amazon.com/security/post/Tx280RX2WH6WUD7/Remove-Unnecessary-Permissions-in-Your-IAM-Policies-by-Using-Service-Last-Access).*

--- 
  
### Amazon Cognito e SAML

Como geralmente dizemos...
Por último, mas não menos importante, temos aqui a estrela do nosso post (sim, podem me julgar por ter guardado para o final!). Agora o Amazon Cognito dá suporte a provedores de identificação que usam Security Assertion Markup Language (SAML). O SAML é um padrão aberto baseado em XML que permite a troca de informação de autorização e autenticação. Ele é usado por múltiplos serviços de autenticação, como o ADFS da Microsoft, ou então como padrão por muitos SaaS como [Google](https://developers.google.com/google-apps/sso/saml_reference_implementation), [SAP](https://wiki.scn.sap.com/wiki/display/Security/Single+Sign-On+with+SAML+2.0) e [Salesforce](https://developer.salesforce.com/page/How_to_Implement_Single_Sign-On_with_Force.com).

Agora que o SAML passa a ser suportado diretamente pelo Amazon Cognito e não são mais necessárias "adaptações tecnológicas" usando Secure Token Service (STS) do IAM, o desenvolvimento de aplicações corporativas que se autenticam por meio de domínios fica mais facilitado. Já pensou no seu aplicativo de lançamento de horas autenticando diretamente no AD da Microsoft? 

Na criação de um provedor no IAM e configurações de roles e permissões específicas já é possível verificar a nova aba, conforme imagem abaixo. Depois da configuração do provedor, tornam-se necessários o carregamento da feature no Cognito e desenvolvimento da feature para a sua plataforma de preferência.  

<p align="center"><img src="https://dl.dropboxusercontent.com/s/g5qcq5pkobdrj62/Screen%20Shot%202016-06-29%20at%209.16.29%20AM.png?dl=0"Cognito - SAML"></p>

Para mais informações sobre a utilização do SAML pelo Cognito verifique a [documentação](http://docs.aws.amazon.com/cognito/latest/developerguide/saml-identity-provider.html) ou o [blog da AWS](https://mobile.awsblog.com/post/Tx28TCWLHIRK4GT/Announcing-SAML-Support-for-Amazon-Cognito).

Nas documentações, diversos templates são dados para carregamento do perfil em diversas SDKs. Mas agora, com o suporte habilitado, múltiplas opções surgem no horizonte no ponto de vista de federação de identidades.

 - [Getting Started Guide for Android](https://docs.aws.amazon.com/mobile/sdkforandroid/developerguide/cognito-auth.html)
 - [Getting Started Guide for iOS](https://docs.aws.amazon.com/mobile/sdkforios/developerguide/cognito-auth.html)
 - [API reference](http://aws.amazon.com/documentation/cognito/)  

Ficou alguma dúvida ou tem alguma contribuição? Aproveite os campos abaixo! E se você quer saber um pouco mais sobre os nossos serviços em AWS, [entre em contato com o nosso comercial](http://conteudo.concretesolutions.com.br/concrete-solutions-contato).
