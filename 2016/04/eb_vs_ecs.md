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
O Docker como plataforma para execução de aplicações é uma ferramenta realmente incrível, tudo que precisamos é de um sistema com kernel Linux e voilá. Algumas poucas abstrações em cima e temos um "Sistema Operacional inteiro", stacks e suas dependências resolvidas para suportar a aplicação que tanto desejamos ver rodando. Levando em consideração que só precisamos de um SO preparado, podemos sim adotar a utilização de uma VM (ou instância EC2) rodando o Docker Engine para realizarmos nossos deploys. Ousaria inclusive, em dizer que é uma forma um pouco mais simples de usar tudo o que a ferramenta tem para dar, mas ao mesmo tempo muito poderosa pois temos mais acessos e a chance de customizar mais conforme precisamos, e isso é importantíssimo as vezes.

#### E a automação?
Daí vem a pergunta, é possível automatizar as coisas desse jeito? E a resposta categórica é SIM, muito. Com o sistema aberto assim temos várias formas de automação, desde a máquina em que o Docker Engine é instalado até a forma como nos conectamos até a esta engine para fazer subir o container com a nossa aplicação.

Várias são as abordagens que podemos utilizar quanto a instalação do Docker e as configurações que podemos fazer para disponibilizá-lo. A ideia aqui não é apresentar um guia para instalação do Docker simplesmente, se você precisa fazer a instalação do Docker em uma máquina Linux você pode seguir esse tutorial [aqui](LINK DOCKER) da própria Docker que é bem explicativo. Eu particularmente gosto de gerenciar todas as configurações necessárias a partir de uma ferramenta como Puppet ou Ansible, mas também é possível que você faça todas as configurações em uma AMI customizada e ajuste as configs via **user data**. De novo, são várias as abordagens possíveis.

Mas como nós da Concrete gostamos de processos cada vez mais automatizados, abaixo segue um trecho de um playbook Ansible para criar uma nova instância EC2 e instalar o Docker e suas dependências para que possamos adotar nos nossos processos automatizados de provisionamento.

```yaml
---

- name: Cria instância EC2 com CentOS e Docker
hosts: localhost
connection: local
gather_facts: false
tasks:

- name: Cria EC2 Docker Host
ec2:
region: <REGION>
key_name: <MY_KEY>
instance_type: <INSTANCE_TYPE>
image: ami-fd0197e0
register: ec2

- name: Instala e configura o Docker
hosts: <INSTANCE_NAME>
remote_user: centos
sudo: yes
tasks:
- name: Cria arquivo do repo com base em arquivo local
copy: src=./docker.repo dest=/etc/yum.repos.d/docker.repo mode=0644

- name: Instala docker-engine via Yum
yum: name=docker-engine state=present

- name: Disabilita o SELinux
selinux: state=disabled

- name: Inicializa e Habilita o Docker na inicialização
service: name=docker state=started enabled=yes

```

Outro aspecto interessante sobre o deploy de containers em ambientes onde temos acesso a engine do Docker é a chance de nos conectarmos remotamente a ela e iniciar a execução de containers, por exemplo. Diretamente do client para o host:

```shell
docker -H tcp://192.168.2.100:5678 run -d pedrocesarti/node-project-sample
```
ou
```shell
curl -XPOST http://192.168.2.100:5678/images/create?fromImage=pedrocesarti/node-project-sample
```
Como dito anteriormente, essa é com certeza a que permite o maior número de customizações, se você não quiser fazer deploy via client diretamente, você pode ainda usar a API da engine e configurar a sua aplicação para realizar todas as operações via API REST (conforme mostrado acima também) ou ainda cadastrar todos os seus docker hosts em um docker-machine e disparar comandos em inúmeros dockers ao mesmo tempo. 

O céu é o limite nessa abordagem pessoal.

### Elastic Beanstalk - Deploy Docker
A segunda abordagem possível, é de utilizarmos o serviço de PaaS da AWS, o Elastic Beanstalk. A grande facilidade por trás de um PaaS é permitir o upload de seu código "as is" e ele resolver todos aqueles requisitos necessários pela plataforma onde o deploy acontecerá.

O Beanstalk permite o deploy em diversas plataformas, como aplicações rodando Java em Tomcat, NodeJS, PHP, Python, Ruby e é claro containers Docker \o/.

<p align="center"><img src="https://dl.dropboxusercontent.com/s/6mcg73ayvawnayb/Screen%20Shot%202016-06-28%20at%2010.15.41%20PM.png?dl=0"Beanstalk Hubot"></p>

No caso do deploy de containers Docker, temos a opção de realizar deploy de um container único ou ainda múltiplos containers no caso de uma stack de aplicações que desejamos colocar em execução em conjunto. Tudo que precisamos é criar um zip da nossa aplicação (incluindo Dockerfile e um Dockerrun.aws.json).


### ECS - Tasks configuradas
