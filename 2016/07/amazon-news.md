# Amazon News – Pacotão de Junho

Como de costume a Amazon não brinca em serviço e constantemente está lançando novas funcionalidades, ou melhorando aquelas que já existem. Neste mês de Junho, diversas melhorias em serviços e no alcance de serviços foram apresentadas. Esse post visa cobrir um pouco do que foi lançado neste mês, como o suporte do Amazon OpsWorks para trabalhar com o Centos 7, a disponibilização do serviço de *Last Accessed Data* do Amazon IAM para a região *South America* e o fantástico anúncio de suporte do Amazon Cognito a SAML.


### OpsWorks e Centos

Agora o OpsWorks passa a dar suporte a instâncias e até mesmo servidores fora da sua stack (on-premises) rodando Centos 7, o suporte inicial prevê somente a versão 7 do sistema operacional e possíveis atualizações nos próximos anos, outra informação importante é que a versão do Chef suportada neste caso é somente a versão 12, então um pouco de cuidado com a versão utilizada atualmente em sua stack.

<p align="center"><img src="https://dl.dropboxusercontent.com/s/6mcg73ayvawnayb/Screen%20Shot%202016-06-28%20at%2010.15.41%20PM.png?dl=0"OpsWorks - Centos"></p>

Para mais informações sobre o suporte a Centos e possíveis atualizações, verifique o [link](https://docs.aws.amazon.com/opsworks/latest/userguide/workinginstances-os-linux.html#workinginstances-os-linux-centos).

### Last Accessed Data para a região South America

Na verdade a Amazon anúnciou na semana passada o suporte da função para duas novas regiões, *South America* (São Paulo) e *Asia Pacific* (Seul) além das oito já suportadas, o mesmo já era esperado, desde que a compania informou o início do rastreio das informações de acesso no final de 2015 e início de 2016. 

O serviço de [__Last Accessed Data__](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_access-advisor.html?icmpid=docs_iam_console) permite obter informações sobre as tentativas de acessos de usuários e roles do IAM aos serviços da AWS. Informações como usuários, grupos e roles acessando recursos são de extrema importãncia para permitir um aprimoramento nas *policies* do seu IAM e manter as boas práticas indicadas pela Amazon baseadas em [menor privilégio](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege).

Agora quando estiver na visualização de um usuário, grupo ou role, você tem a opção de uma nova aba chamada __Access Advisor__ onde são apresentadas todas as tentativas de acesso daquela entidade aos recursos da AWS, indepententemente da forma de conexão, dendo elas provenientes de acesso via console ou chamadas de API. 

<p align="center"><img src="https://dl.dropboxusercontent.com/s/s4otsk5ybalpfg6/Policy-centric-image-1ab.png?dl=0"IAM - Last Accessed Data"></p>

*Imagem retirada do post de Kai Zhao no blog de segurança da AWS, para conferir o post na íntegra, [clique aqui](https://blogs.aws.amazon.com/security/post/Tx280RX2WH6WUD7/Remove-Unnecessary-Permissions-in-Your-IAM-Policies-by-Using-Service-Last-Access).*

