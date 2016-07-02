# Infraestrutura como código

Uma das práticas recorrentes na minha vida é a análise da forma como eu faço as coisas atualmente e como eu cheguei lá. Sendo eu um SysAdmin por paixão, esses dias parei para analisar as ferramentas que utilizo atualmente no meu dia a dia de trabalho, a forma como eu as utilizo e também nas inúmeras opções que tenho para substituir essas ferramentas assim que eu quiser por outras com basicamente a mesma funcionalidade.

Lembrei dos tempos áureos
```shell
ssh root@host ‘comando ; comando ; comando’
```


Uma das práticas que eu tenho na minha vida é de parar e pensar algumas coisas do que faço e porque faço, e assim acontece também no meu dia-a-dia profissional. Essa semana eu estava pensando em uma “Arquitetura Perfeita” no ponto de vista de criação de infraestrutura e deploy de aplicações. Esse post tem por objetivo compartilhar alguns problemas que eu vi ao longo dos anos e algumas características levantadas.

Pensava em que ferramentas usar, qual a melhor solução de todas as disponíveis. Obviamente eu não cheguei a lugar nenhum, porque como eu, você deve entender que a melhor infraestrutura é aquela que funciona melhor pra você.

Mesmo não obtendo uma resposta exata sobre cada aspecto, eu passei por DIVERSAS ferramentas e isso me fez pensar novamente porque fazemos assim e o fundamento de algumas coisas. Pra quem gerenciou ou ainda gerencia infraestrutura física (bare-metal) lembra das dores da automação, aquele script maroto dando comandos por ssh ainda tiram as noites de sono dos SysAdmins.

Mas passamos por inúmeros problemas nessa abordagem, desde modificações na plataforma até a necessidade de escalabilidade da arquitetura, então .
