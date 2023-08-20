# Carolina_Puga_DDF_TI_agosto2023
**Case Técnico**
*Item 1, 3 e 5*


**Item 1**

Para monitorar a satisfação do cliente e eficiência da equipe de suporte na plataforma Dadosfera, devemos considerar os seguintes dados: 

1. Chamados(Tickets)
1. Data e hora início Tickets
2. Data e hora atualização Tickets
1. Data e hora final Tickets
2. Status Tickets
3. Pesquisa de Satisfação
4. Quantidade de atendentes do suporte

Os dados serão extraídos da base do Service Desk, identificaremos o tipo de arquivo e formato do dado `(JSON, XML ou outros)`. Em seguida, realizaremos o tratamento dos dados como: remover linhas repetidas, desconsiderar campos vazios, padronizá-los e cruzar bases relacionadas com esses dados `(Padronizar 'Estado' e cruzar dados de ID com o nome/cadastro do cliente)`. 

Ao final, vamos carregar os dados dentro do ambiente da Dadosfera. Agora sim, trabalharemos os dados:

- Quantidade de Tickets
  - Somar chamados = Volume total diário de chamados
    - A informação colabora para cruzarmos a quantidade de tickets x o número de atendentes do suporte, para verificarmos sobre a sobrecarga da área
      
- Cruzar Data e hora de início e final
  - Final - início = Resultando no Tempo do chamado
    - A informação colabora para metrificarmos o tempo de efetiva conclusão dos chamados

- Tempo de resposta
   - Filtrar Status **Novo** + Data e hora início Tickets e Filtrar Status **Aberto** + Data e hora atualização Tickets
  
     Data e hora atualização Tickets - Data e hora atualização Tickets = Tempo de resposta
     - Conseguimos medir o tempo médio de para início de atendimento, como também monitorar o tempo de demora para atualizações de status
  
   - Filtrar Status **Aberto** + Data e hora atualização Tickets e Filtrar Status **Em espera** + Data e hora atualização Tickets
 
     Data e hora atualização Tickets do **Em espera** - Data e hora atualização Tickets **Resolvido** = Tempo de resposta
     - Conseguimos medir o tempo médio de para finalização de atendimento, como também monitorar o tempo de demora para atualizações de status

     **Novo**  indica que nenhuma ação foi tomada no ticket.

     **Aberto**  indica que um ticket foi atribuído a um agente e está em andamento. 

     **Pendente**  indica que o agente está aguardando mais informações do solicitante. 

     **Em espera**  indica que o agente está esperando informações ou ações de um terceiro que não é o solicitante. 

     **Resolvido**  indica que o agente enviou uma solução.

- Chamados não resolvidos
  - Somar chamados **Em espera** = Volume total de chamados não resolvidos 

    % Chamados não resolvidos -> número total de atendimentos / número de chamado **Em espera**
    - É possível calcular uma média semanal de chamados não resolvidos e acompanhar a sazonalidade dos chamados, monitorando o aumento ou diminuição. 

- Net Promoter Score (NPS)
  - O consumidor atribui uma classificação ao serviço que pode variar de 0 a 10.

  0 a 6: clientes não satisfeitos com o serviço. 
  7 a 8: clientes neutros
  9 a 10: clientes satisfeitos 

  Entre 0 a 8 os clientes não recomendariam o serviço/produto devido ao suporte.

  Entre 9 e 10 são clientes satisfeitos e fiéis, dos quais recomendariam a empresa. 

  Para isso, será necessário coletar os dados de pesquisa pós atendimento e contabilizar os clientes entre, não satisfeitos, neutros e satisfeitos. Representado através de um    
  gráfico de pizza por 3 cores:

  9 a 10 -> verde (Ótimo)
  7 a 8 -> amarelo (Neutro)
  0 a 6 -> vermelho (Ruim) 

  Teremos como resultado:

  Promotores -> soma de todos os atendimentos na faixa verde

  % Promotores -> número total de atendimentos / número de atendimentos na faixa verde

  % Detratores -> número total de atendimentos / número de atendimentos na faixa vermelha

  NPS = % Promotores - % Detratores

___

**Item 3**

Para uma gestão de acesso efetiva precisamos, realizar os seguintes processos:

1. Centralizar os controles de acesso em uma única plataforma
3. Centralizar a autorização de acesso aos dados 
4. Característica única para acesso aos sistemas com uma multipla verificação
5. Ter um portal de acesso aos dados de acordo com o perfil
6. Sistema de busca e relatórios para acesso aos dados

___

**Item 5**

**SELECT** com (*) devolve todos os campos, o **FROM** informa qual a tabela (users_emails) e o **WHERE**, as condições de menos 30 dias a partir da data com a função **DATE_SUB** onde informamos a coluna (Data_cadastro) e o intervalo de 30 dias. 

`SELECT * FROM users_emails WHERE DATE_SUB(Data_cadastro, interval 30 day)`

Resultado da consulta será disponibilizado em `CSV` aos interessados por e-mail
