### Deploy automatizado  Lambda AWS com Jenkins


Olá pessoas, bem?! A pouco tempo estou trabalhando com AWS e ja me deparei com várias situações aonde precisei de um --help "google.com.br" haha, acho que nao sou o unico né! 
Estamos em um momento, aonde precisamos cada vez mais automatizar oque fazemos. O mais maneiro é que hoje em dia já temos muitas ferramentas (softwares) prontas para usufruir, e o principal adaptar conforme a nossa necessidade, cara isso é muito legal.

Algumas pesquisas que fiz, algumas não encontrei e quando encontrei faltava uma explicação com mais detalhes. Bom, vem comigo não vamos perder tempo, mao na massa. 

Vamos utilizar o Jenkins (uma ferramenta de integração continua), para armazenar o nosso codigo iremos usar o github, por final iremos usar o serviço da amazon Lambda.

Oque é Lambda?

So pode encontrar mais detalhes aqui: https://aws.amazon.com/pt/lambda/details/ mas para resumir, é um serviço da aws, que executa funções de codigo, sem a necessidade de ter uma infraestrutura, só é executado seu codigo quando necessário (Lambda invoca o codigo). Chamamos de "Função do Lambda", quando alguem dizer Lambda invocou o codigo, isso quer dizer que seu codigo foi executado. 

Ta bom, mas quando usar?

De cara já digo, quando você não quer se preocupar com a infraestrutura e escalabilidade. O proprio Lambda identifica a necessidade de escalar quando necessário e faz isso sem voce se preocupar. Voce não tera que se preocupar com os bugs de SO e suas novas features para manter a segurança, nossa serio que nao preciso mais abrir um chamado para operações atualizar os pacotes do SO ou de dependencias, serio não precisa. Uma galera de infra vai gostar, outra não, eu sei bem disso eu nasci em suporte e infra, mas so de pensar que uma atualização de kernel, ou de atualizações de features ou instalação de pacotes pode causar alguns estragos no SO e normalmente esse tipo de rollback não é tão simples, já vi alguns sysadmin instalando pacotes com a opçao -y mal sabe eles que muitas das vezes muitos pacotes são atualizados entre eles pode estar o java um node, isso pode gerar problemas caso o codigo esta travado para executar em determinada versão. Pode demorar um certo tempo para descombrir que foi atualização de um dos respectivos pacotes que casou isso. 
Com o Lambda você faz o deploy de uma nova feature ou corrigir falhas rapidamente, há sem se preocupar com os comentarios anteriores. Isso pode ser de forma automatica, vai vendo rsrs.
Você so precisa determinar a quantidade de memória e a Lambda cuida do resto, CPU, Disco e IO/Disco.
Isso se torna muito interessante quando voce pretende colocar sua infraestrutura na AWS, utilizando S3 para armazenar backup de todos os codigos, caso utilize armazenamento de arquivos em Bucket S3 (talvez no proximo capitulo explico melhor sobre Bucket =D). Também tem o serviço de filas na AWS é SQS (um rabbitmk da vida). Ou até mesmo outros serviços da AWS, RDS (banco), Gateway API

Com o Lambda você faz o deploy de uma nova feature ou corrigir falhas rapidamente, há sem se preocupar com os comentarios anteriore    s. Isso pode ser de forma automatica, vai vendo rsrs.
 19 Você so precisa determinar a quantidade de memória e a Lambda cuida do resto, CPU, Disco e IO/Disco.
  20 É mais ainda interessante quando voce pretende colocar sua infraestrutura na AWS, utilizando S3 para armazenar backup de todos os c    odigos, caso utilize armazenamento de arquivos em Bucket S3 (talvez no proximo capitulo explico melhor sobre Bucket =D). Também tem     o serviço de filas na AWS é SQS (um rabbitmk da vida). Ou até mesmo outros serviços da AWS, RDS (banco), Gateway API, entre outros    .
	 21 Tem mais sim, usando Lambda dentro de uma VPC, será necessário usar security group, garantindo segurança. Mas não acabou por ai, na     AWS temos o serviço de IAM, voce controla quais serviços da sua infraestrutura pode ter acesso ao seu Lambda e quais deles podem i    nvocar o Lambda. Aqui tem uma parte chatinha porém muito necessária, configurar policies e criar role, com os niveis de permissoes,     garantindo ainda mais segurança e deixando uma arquitetura muito mais justa.
	  22 Quer mais?! Você só paga pelo tempo de execução do Lambda, isso é demais. Tem gente que acha caro, mais manter uma infraestrutura 2    4x7x367 sendo que boa parte de um sistema  é utilizado poucas vezes ao dia, um exemplo: faça uma conta de um modulo de um sistema d    e controle de acesso, esse modulo so consulta o banco e verifica o status e libera, o mesmo é executado a cada 30Min quando passa u    ma pessoa pela catraca, essa execução demora 2 segundos, vale a pena montar uma infraestrutura fisica redundante para isso, sem pen    sar nos problemas que teria no arcondicionado para resfriar os equipamentos, haha.
		 23                                                                                        Com o Lambda você faz o deploy de uma nova feature ou corrigir falhas rapidamente, há sem se preocupar com os comentarios anteriore    s. Isso pode ser de forma automatica, vai vendo rsrs.
		  19 Você so precisa determinar a quantidade de memória e a Lambda cuida do resto, CPU, Disco e IO/Disco.
			 20 É mais ainda interessante quando voce pretende colocar sua infraestrutura na AWS, utilizando S3 para armazenar backup de todos os c    odigos, caso utilize armazenamento de arquivos em Bucket S3 (talvez no proximo capitulo explico melhor sobre Bucket =D). Também tem     o serviço de filas na AWS é SQS (um rabbitmk da vida). Ou até mesmo outros serviços da AWS, RDS (banco), Gateway API, entre outros    .
			  21 Tem mais sim, usando Lambda dentro de uma VPC, será necessário usar security group, garantindo segurança. Mas não acabou por ai, na     AWS temos o serviço de IAM, voce controla quais serviços da sua infraestrutura pode ter acesso ao seu Lambda e quais deles podem i    nvocar o Lambda. Aqui tem uma parte chatinha porém muito necessária, configurar policies e criar role, com os niveis de permissoes,     garantindo ainda mais segurança e deixando uma arquitetura muito mais justa.
				 22 Quer mais?! Você só paga pelo tempo de execução do Lambda, isso é demais. Tem gente que acha caro, mais manter uma infraestrutura 2    4x7x367 sendo que boa parte de um sistema  é utilizado poucas vezes ao dia, um exemplo: faça uma conta de um modulo de um sistema d    e controle de acesso, esse modulo so consulta o banco e verifica o status e libera, o mesmo é executado a cada 30Min quando passa u    ma pessoa pela catraca, essa execução demora 2 segundos, vale a pena montar uma infraestrutura fisica redundante para isso, não quero nem pensar nos problemas que teria com arcondicionado, haha. Então não será cobrado com seu codigo não estiver executando.
				 
O Lambda é perfeito ?! Vejamos os pros:

Não, ele não tem suporte para todas linguagens. Veja mais em:
Não esta disponivel em todas regioes da AWS. 




Nos 3 meses como devops me deparei com algumas atividades, entre elas automatizar deploy de uma funçao lambda na aws usando jenkins.


