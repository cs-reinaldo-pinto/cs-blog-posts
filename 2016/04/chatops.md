# ChatOps - Um pouco de Passado, a utilização no Presente e a massificação no Futuro.

ChatOps surgiu nos últimos anos como um modelo colaborativo, onde pessoas e ferramentas são conectadas, permitindo uma melhor intereção dos times dentro do ambiente como um todo.

## Sobre passado 

No tempo em que __Cloud Computing__ era um termo muito utilizado mas ninguém sabia pra que seria utilizado mesmo, eu estava lendo um artigo sobre computação distribuída e nele dizia que os conceitos de cloud datavam da década de 70 e isso fazia muito sentido. Já iniciavam-se os trabalhos com máquinas virtuais e já era prevista a utilização de computadores __on-demand__ (pagando mensalmente a conta, assim como fazemos com água e luz). Desde então, parei a observar um pouco melhor os "**novos conceitos**" que surgem.

Nestes exemplos dados, basicamente toda a tecnologia já existia, mas ainda não havia um cenário ideal para que elas fossem aplicadas. Podemos listar na história diversos momentos onde isso aconteceu, vocês lembram dos "terminais burros" conectados aos mainframes da IBM? E dos "novos" conceitos de VDI (Virtual Desktop Infrastructure) da VMware?  

A utilização dos chats e de certa automação neles também tiveram sua tentativa de aplicação outrora, desde o __BBSs__ (Bulletin Board System) na década de 70, até o __mIRC__ e __AOL__ na década de 90, passamos por inúmeras ferramentas que utilizavam de conceitos bem primitivos de comunicação colaborativa e notificação. Inclusive podemos citar o sugimento do primeiro chatbot em 1993, o [Eggdrop](http://www.eggheads.org), utilizado para notificações dentro de canais IRC surgiu como algo revolucionário, mas fora de contexto. Apesar de grande popularidade, no inîcio dos anos 2000 os chats perderam bastante espaço devido aos serviços de mensagem instantâneas e redes sociais, voltando a ter um pouco de espaço mais recentemente em serviços de atendimento ao cliente incorporado a sites de empresas, mas ainda assim sem uma grande aplicação.

## E agora?

Mais um termo que surgiu recentemente e vem causando alvoroço é o tal **DevOps**, mas diferente de outros posts, o meu não tem por intenção discutir o que é ou deixa de ser DevOps. Não quero deixar pessoas emocionalmente abaladas pelo o que escrevo. E já que eu não estou aqui para definir se podemos ou não chamar DevOps de profissão, eu só queria compartilhar que temos alguns pilares comuns aos quem aderem ao tal DevOps. Esses pilares principais ficaram conhecidos como CAMS:

- Culture
	- Onde o principal intuito é diminuir as barreiras entre os times e permitir uma integração maior por meio de processos e sistemas menos burocráticos.
- Automation
	- Automatizar tudo que for possível para permitir um ganho de performance e de produtividade.
- Measurement
	- Levantar dados Buscar dados de tudo que for possível, para se ter maior inteligência em tomada de decisões, e o mais importante, transparência na apresentação destes dados.
- Sharing
	- A chave maior de tudo é compartilhar, compartilhar tudo que for possível. 

Então a comunidade busca formas de se aproximar desses pilares para que os processo fiquem mais ajustados ou mesmo para permitir uma melhor gerência das informações. Mas em um ambiente de medição, automatização, e compartilhamento total alguns problemas surgem:

- Como deixar todos os times (muitas vezes não só os times de produto, como desenvolvimento e operações) atualizados no processo? Como deixar todas as equipes na mesma "página"?
- Como garantir que todos possam fazer de forma ágil as suas atividades e que isso fique visível a todos? Não queremos ter mais heróis que magicamente resolvem um problema sem ninguém mais saber como?
- Como garantir certa uniformidade e processo no acesso as informações?
- Como permitir uma unificação das ferramentas em um ambient só e não ter que fazer a "Dashboard das dashboards", aquela ferramenta que gerencia outras ferramentas?

A resposta é simples, utilizando uma ferramenta interativa onde podemos criar comandos e scripts para automatizar tarefas das mais básicas as mais complexas. O CHAT então volta a tona, e independentemente do serviço de chat utilizado (Slack, Hipchat, Campfire, entre outros), temos inúmeras opções de bots para conectar a estes serviços. 

- [Hubot](https://hubot.github.com) (JavaScript e CoffeeScript)
- [Lita](https://www.lita.io) (Ruby)
- [Err..](http://errbot.io/en/latest/) (Python)  

Verificando as documentações destas ferramentas, é possível verificar o quão customizåvel e extensíveis as mesmas são. Só necessitando adicionar um script da linguagem suportada para adicionar uma funcionalidade e converter algo digitado no chat para um comando para execução de uma tarefa específica. 

Eu fiz um pequeno projeto recentemente usando Docker para subir um Hubot e conectar ao meu Slack pessoal e poder brincar tranquilamente, e encorajo a todos fazerem o mesmo, então se quiserem dar uma brincada inicial com ChatOps, verifiquem esse repositório.

- [ChatOps Begginers](https://github.com/pedrocesar-ti/hubot-slack-docker)

Grande parte dos plugins são configurados via variável de ambiente então se você passar seu token de acesso ao Slack, o nome e o canal para o bot. Tudo já funcionará com o simples comando abaixo:

```shell
docker run --name mybot -it  \
 -e HUBOT_SLACK_TOKEN='#######' \
 -e Hubot_SLACK_TEAM='#######' \
 -e Hubot_SLACK_BOTNAME='#######' \
 -d pedrocesarti/hubot-slack
```
Após o comando acima, seu bot já estará conectado ao chat e esperando por comandos basta só chamar o nome dele e dar um help, meu bot se chama macgyver, então:

```
macgyver help
```
Já mostraria todos os plugins ativados e como utilizá-los, conforme imagem abaixo.

<p align="center"><img src="https://dl.dropboxusercontent.com/s/d0mld4njpw70bmw/Screen%20Shot%202016-06-08%20at%207.13.36%20PM.png?dl=0"Hubot - Slack"></p>

A documentação do repositório mostra algumas outras opções e customizações que podem ser criadas, então se divirta.

## E daqui pra frente?
Depois de passarmos por muitas dores de cabeça com integrações no passado, estamos em uma época áurea em relação a integração e grande parte deste sucesso é a adoção cada vez mais pesada de APIs, tudo se tornou mais fácil, endpoints configurados, e tudo se resolve por meio de GETs e POSTs que retornam um JSON perfeito para ser tratado ;).

Levando em consideração que já temos inúmeros módulos já desenvolvidos para todos os bots, permitindo as mais variadas funcionalidades, como gerar um gráfico de utilização da rede, como inicializar uma instância na Amazoni AWS ou até mesmo criar uma regra no firewall e que eles permanecem expansíveis aguardando só um novo script para criar uma nova funcionalidade acredito então que a popularidade tende a continuar crescendo.  

ChatOps talvez não seja realmente para todos os ambientes, mas quanto mais destruimos barreiras entre os times e deixamos todo o processo mais transparente tudo se torna mais fácil então se eu tenho uma mensagem para deixar no final deste post é:

**USE CHATOPS E SEJA MAIS ÁGIL!!** 

