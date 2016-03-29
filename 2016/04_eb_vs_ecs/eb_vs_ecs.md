# Elastic Beanstalk vs. EC2 Cluster Service - Aplicações Dockerizadas

Bom você já estudou sobre arquiteturas e viu que talvez a quebra de grande aplicações em microserviços seja o caminho para o futuro dos produtos que entregamos, diminuir complexidade, diminuir pontos de falha, reaproveitamento da infraestrura, automação de todo o processo, etc... São vários os motivos que levam a grande parte do setor migrar seus serviços cada vez mais complexos para esse "NOVO CONCEITO" (sim entre aspas e maiúsculo), porque o conceito não é tão novo assim né?! A ideia não é nova, mas agora temos diversas ferramentas para nos ajudar a colocar tudo isso junto e o mais impressionante de tudo, **FAZER TUDO FUNCIONAR**.

Quando falamos em termos ferramentas atualmente, estamos falando de todas as tecnologias atuais que nos auxiliam e de muitos conceitos que voltaram a ativa "repaginados", como a própria computação em nuvem (virtualzação + serviço), automação de infraestrutura e IaaC, automação de deploy e porque não de CONTAINERS. 

Sim! Containers (e engole esse choro!), aqui vamos falar especificamente de **Docker**. 

Aí geralmente começa aquela discussão infinita sobre rodar container em produção ou não. Você pode olhar o histórico das ferramentas que tem surgido ao longo dos últimos anos e dizer que o Docker talvez não esteja maduro (em relação a tempo) suficiente para rodar certos serviços críticos, ok. Você pode vir com aquela velha história de quebrar o sistema porque o container não é totalmente isolado e tem acesso em alguns namespaces críticos, ok também. Ou ainda ser mais **hardcore** ainda e implicar com o empilhamento de serviço por versão ser um grande erro, **OK**, já entendi seu ponto (e eu também pensava assim há um tempo atrás). Mas não leve a mal o que eu vou dizer, em muitos lugares nos chamam de **arquitetos de sistemas** e se a gente não aprender a lidar com o "material" que é dado para trabalharmos, vamos ter que começar a nos especializar em outra coisa que não seja __tecnologia__.

##AWS
Com toda a certeza você deve ter se perguntado algumas vezes, "porque discutir tudo isso?", ou então, "ué, não era um post sobre AWS?".

Pronto, você está no post certo, mas sempre é bom relembrar as necessidades que temos antes de tomar decisão entre alguma ferramenta ou tecnologia. Por isso, tanta discussão.

###Elastic Beanstalk
###ECS

