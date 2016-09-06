# AWS e as aplicações Dockerizadas

Bom você já estudou sobre arquiteturas e viu que talvez a quebra de grande aplicações em microserviços seja o caminho para o futuro dos produtos que entregamos, diminuir complexidade, reduzir pontos de falhas, reaproveitamento da infraestrura, automação de todo o processo, etc... São vários os motivos que levam a grande parte do setor migrar seus serviços cada vez mais complexos para esse "NOVO CONCEITO" (sim, entre aspas e maiúsculo), porque o conceito não é tão novo assim né?! A ideia não é nova, mas agora temos ferramentas disponíveis para nos ajudar a colocar tudo isso junto e o mais impressionante de tudo, **FAZER TUDO FUNCIONAR**.

A ideia de utilizar containers para a entrega de microserviços em produção tem sido uma prática muito bem aceita e esse post visa trazer as soluções da Amazon para o deploy de aplicações dockerizadas. Vamos deployar uma imagem de teste em diferentes serviços e verificar o comportamento das soluções.

## Velha discussão sobre containers
Sim! Containers em produção (e engole esse choro aí!), aqui vamos falar especificamente de **Docker**. 

Geralmente nessa hora se começam aquelas discussões sobre rodar container em produção ou não. Você pode olhar o histórico das ferramentas que tem surgido ao longo dos últimos anos e dizer que o Docker talvez não esteja maduro (em relação a tempo) para rodar certos serviços críticos, ok. Você pode vir com aquela velha história de quebrar o sistema porque o container não é totalmente isolado e tem acesso em alguns [namespaces críticos](video hittler), ok também. Ou ainda ser mais **hardcore** ainda e implicar com o empilhamento de serviço por versão ser um grande erro, **OK**, já entendi seu ponto (e eu também pensava assim há um tempo atrás). Mas não leve a mal o que eu vou dizer agora, em muitos lugares nos chamam de **arquitetos de sistemas** e se a gente não aprender a lidar com o "material" que é dado para trabalharmos, vamos ter que começar a nos especializar em outra coisa que não seja __tecnologia__.

Se ainda pensarmos em questões como portabilidade, reproducibilidade e até mesmo escalabilidade containers são sim o grande nome do momento. Então não tenha receio de usar, administro atualmente algumas aplicações (sim, não são todas) que rodam em containers e em produção e sem dor de cabeça.

##AWS

Iniciei alguns projetos no passado que tinham a necessidade de serem deployados em containers, a aplicação já estava toda embarcada em imagens Docker (exatamente o que os desenvolvedores rodavam localmente) e precisávamos somente shippar nossos containers para os nossos diferentes ambientes. Mas daí vinha uma decisão difícil a ser tomada, qual ferramenta utilizar para colocar nossos containers para rodar. Só na AWS temos três ferramentas diferentes para deployar nossos containers, são elas: usando instâncias EC2 configuradas como Docker Hosts, o Elastic Beanstalk que serve para deployar diversas plataformas de serviço e por último mas não menos importante ECS que é o serviço especializado da Amazon para rodar containers.

### EC2 - Docker Host
O Docker como plataforma para execução de aplicações é uma ferramenta realmente incrível, tudo que precisamos é de um sistema com kernel Linux e voilá. Algumas poucas abstrações em cima e temos um "Sistema Operacional inteiro", stacks e suas dependências resolvidas para suportar a aplicação que tanto desejamos ver rodando. Levando em consideração que só precisamos de um SO preparado podemos sim levar em consideração a utilização sistema rodando Linuxusaria dizer que a forma mais primitiva e menos suscetível a falhas é instalar a 


### Elastic Beanstalk - Deploy Docker
### ECS - Tasks configuradas
