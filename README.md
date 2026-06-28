 OBJETIVO DESTE SCRIPT:
       Script simples e rápido para avisos de compromissos. Ao
        ser executado ele mostra o compromissos agendados para o
        dia corrente e também os compromissos agendados para os
        dias à frente. Além disso também emite um lembrete
        baseado na hora do compromisso. A quantidade de dias
        dessa antevisão dos compromissos à frente pode ser
        definido facilmente. (linha: 'DiasDosLembretes=7')

        Em relação ao "agenda 3.x" foi acrescentado a
        possibilidade de lembretes, através de uma caixa gráfica
        (dialog), ou através de uma música, no horário do
        compromisso .

        Em relação ao "agenda 4.X" houve uma simplificação geral
        do funcionamento, eliminando diretórios e resumindo tudo
        a dois arquivos. (agenda.sh e o agenda.txt)
        Acréscimo da possibilidade de marcar compromissos por dia
        da semana ou para todos os anos ou todos os meses ou todos
        os dias.

	  Versão 5.3
	  Simplificação do "MENU PRINCIPAL", agora com duas opções.

        Versão 5.4
        Limpeza do código






 VERSÃO:
       5.4
       2016/08/19



 LICENÇA:
       GLP, E SEU USO É DE SUA TOTAL RESPONSÁBILIDADE.



 AUTOR:
       Ricardo Sabaliauskas
       <rsabaliauskas@gmail.com>



 DEPENDÊNCIAS:

       Subentendendo-se que é necessário o bash numa versão rescente:

        1) Um Editor de texto a ser defenido conforme a
           disponibilidade do seu sistema ou de sua preferência
           (linha: Editor=kate no script 'agenda.sh').

       2) Ter instalado:
          - 'dialog'
          - 'Konsole' (é o default, mas você pode configurar o
            'gnome-terminal' ou outro console gráfico de sua preferência)
            edite linha: 'Terminal="konsole --noclose -e"', mas note
            que também é necessário incluir o parâmetro para executar
            um comando.




   #############################################################
  ########   1.0) PREPARAÇÃO
#########  ****************************************************

   Este script esta licenciado sob a GLP e seu uso é de sua inteira
   responsabilidade. Trata-se de um 'avisador', ou agenda, de compromissos para quem
   usa muito o computador. Seu uso padrão fará com que um aviso com os compromissos
   de todo o dia e mais uma antevisão de sete dias, que podem ser modificados, a
   frente apareça na inicialização do ambiente grafico. Ele pode ser usado em
   ambientes sem modo gráficos e além disso existe também um segundo aviso baseado
   nos horários dos compromissos. Esse segundo aviso pode ser uma tela gráfica (dialog)
   ou um aviso sonoro através de um mp3 ou os dois juntos. A vantagem dele sobre
   outros tipos de 'agenda', como o evolution ou o korganizer, é que neste script
   os agendamentos são rápidos e o aprendizado também. Também permite o
   uso de parâmetros para torna-ĺo ainda mais ágil. (Um exemplo disso: Suponha que
   você queria apenas agendar e não precisa ver nenhum compromisso, então execute
   "bash agenda.sh 1" e o agendamento já estará em execução).



1º PASSO: (PERMISSÕES DE EXECUÇÃO AO SCRIPT)
***************************************************

   Dê permissão de execução aos script 'agenda.sh'.

   Para fazer isso pela linha de comando, supondo que você já está dentro do
    diretório em que o script 'agenda.sh' está presente:

   meu_usuario@meu_computador:~$ chmod +x agenda.sh



 2º PASSO: (CONFIGURAÇÃO INTERNA DOS SCRIPST)
*************************************************

   Você pode colocar o script 'agenda.sh' em qualquer lugar que deseje, mas caso
   você não esteja acostumado ao ambiente Linux recomendo que você coloque o
   script 'agenda.sh' dentro do seu diretório 'home' (echo /home/$USER), sendo
   este um lugar de fácil acesso, lugar aonde normalmente os gerenciadores de
   arquivos (como o 'Nautilus', do ambiente gráfico 'GNOME', ou o 'Konqueror',
   do ambiente gráfico 'KDE)' se localizam ao serem abertos por default, sem
   que haja necessidade de que especifique algum caminho.

   Se você pretende executar o script 'agenda.sh' em seu diretório 'home' (echo
   /home/$USER) possivelmente não precisará, inicialmente, mudar nenhuma variável
   dentro do script.

   Se tiver problemas na execução, possivelmente ao executá-lo em outro diretório,
   e precisar ajustar mais explicitamente o local de execução, então proucra a linha
   'LocalizacaoDoScript="/home/$USER"' e edite-a conforme necessidade. Caso a localização
   do seu diretório contenha nomes com espaços vazios será obrigatório o '"'
   (aspas) imediatamente depois do igual e imediatamente após a última letra,
   conforme exemplo abaixo:

       LocalizacaoDoScript="/home/eu/Agenda de Compromissos"



3º PASSO: (INICIALIZAÇÃO NO SEU AMBIENTE GRÁFICO)
***************************************************************

   Para cumprir bem o papel de 'avisador' de compromissos é necessário fazer com que
   o script 'agenda.sh' seja executado no início da inicialização do seu ambiente
   gráfico para que você possa ter a visão geral dos compromissos logo no inicio do
   uso do seu computador. Para isso acontecer é necessário fazer uma configuração
   que varia de ambiente gráfico para ambiente gráfico, e ela é normalmente fácil,
   mas infelizmente não será possível eu abordar cada uma dessas configurações,
   porque existem vários ambientes gráficos. Então, vou explicar a configuração
   da execução do script 'agenda.sh' no ambiente gráfico que mais conheço, o KDE
   3.5.10 (eu uso Slackware 14 com o KDE 3.5.10), mas essa explicação também serve
   para a série KDE 4.x.


No 'KDE':
---------

   Abra um editor de texto e digite, ou cole, as 2 linhas abaixo:

=== INICIO === (copie da linha '#! /bin/bash' até uma linha antes do '=== FIM ===
 e se tiver presente remova as duas letras iniciais '' de cada linha)
   #! /bin/bash

   # Iniciar o Cronometro:
   bash /home/$USER/agenda.sh 0 &

   # Alertar os horários dos compromissos através do dialog:
   konsole -e bash /home/$USER/agenda.sh &

=== FIM ===

   NOTE: O endereço acima '/home/$USER/agenda.sh' é válido somente se você tiver
   deixado o script 'agenda.sh' dentro do diretório 'home', caso contrário, ajuste
   o caminho corretamente.

   Agora salve-o com qualquer nome, eu sugiro 'autostart.sh'. De permissão de execução
   e mova-o para o diretório '.kde/Autostart' de seu usuário:

   meu_usuario@meu_computador:~$ chmod +x autostart.sh

   meu_usuario@meu_computador:~$ mv autostart.sh /home/$USER/.kde/Autostart



   #############################################################
  ########   2.0) FUNCIONAMENTO
#########  ****************************************************

   O funcionamento do script 'agenda.sh' é simples e ágil e ele foi criado justamento
   para isto. No Linux existem vários programas, e bem sofisticados por sinal, que
   permitem agendamentos de lembretes de tarefas e compromissos, como por exemplo o
   'Korganizer' ou o 'Evolution'. Porém os agendamentos de tarefas neles demoram
   muito, se comparado com este script, e, somando-se isto ao fato deste script poder
   ser usado em ambientes sem o modo gráfico resulta em um diferencial que foi o
   motivo de eu faze-lo.

   Ao executá-lo (bash agenda.sh) você tera o seguinte 'tela':

           julho 2010           agosto 2010          setembro 2010
      Do Se Te Qu Qu Se Sá  Do Se Te Qu Qu Se Sá  Do Se Te Qu Qu Se Sá
                   1  2  3   1  2  3  4  5  6  7            1  2  3  4
       4  5  6  7  8  9 10   8  9 10 11 12 13 14   5  6  7  8  9 10 11
      11 12 13 14 15 16 17  15 16 17 18 19 20 21  12 13 14 15 16 17 18
      18 19 20 21 22 23 24  22 23 24 25 26 27 28  19 20 21 22 23 24 25
      25 26 27 28 29 30 31  29 30 31              26 27 28 29 30

      ================================================================
      ***   COMPROMISSOS  DE HOJE   ****   24-Ago-2010 Ter 13:23   ***
      14:00 -> Dentista
      ================================================================
      ***   COMPROMISSOS  FUTUROS   ****   P/ os próximos 7 dias   ***
      Para daqui a 1 dias:
                                13:00 -> Dentista
      Para daqui a 2 dias:
                              13:00 -> Dentista
       ================================================================
      Tecle "ENTER" p/ acessar o menu ou a letra "q" + "ENTER" p/ sair
      ou digite diretamente a opção, se você lembrar, e tecle  "ENTER"


   Como podemos observar, depois dos calendários existem dois campos separados pelas
   linhas duplas. A primeira é dos COMPROMISSOS DE HOJE para o dia de hoje e eles são
   realçados pela cor vermelha. No caso deste exemplo temos um compromisso 'Dentista'
   as '14:00' hrs. e as 14 hrs um segundo aviso (caixa gráfica ou uma música ou os
   dois) serão executados para alertá-lo sobre a hora do compromisso. O segundo campo
   é dos COMPROMISSOS FUTUROS que são avisos dos compromissos dos dias seguintes. No
   exemplo acima temos avisos para os 2 próximos dias para que tenhamos uma idéia do
   que nos espera. Por default o script exibe os compromissos de hoje e os compromissos
   dos próximos 7 dias mas se você preferir pode mudar esse comportamento configurando
   a variável 'DiasDosLembretes=7'. Se não quizer nenhuma antevisão dos compromissos
   futuros então troque o número 7 por 0, nesta variável.

   Estando diante da 'tela' acima e teclando 'ENTER' você verá estará nessa outra tela:



      *********************** MENU PRINCIPAL ***********************

      "ENTER") Para voltar a visualização dos compromissos deste dia.
         q) Para sair deste programa.

         1)  Agendar compromisso.
         2)  Ver compromissos agendados.
         3)  Ver compromissos.deste MÊS.
         4)  Alterar.
         5)  Deletar.



   Esta outra tela é o Menu Principal e ela oferece 5 opções, conforme visto,
   bastando escolher uma delas digitando o número correspondente (de 1 a 5) e teclando
   'ENTER'. Se você teclar 'ENTER' sem escolher opção alguma então você voltará a
   'tela' anterior, a de visualização de compromissos.

   A partir da versão 5.3 o MENU PRINCIPAL foi simplificado a apenas duas opções.

   Em agumas situações, quando você tiver dentro do comando less, será necessário teclar
     "q"+"ENTER" para sair, "q" de quit.


   1)  Agendar compromisso.
   ------------------------

   Esta é a mais importânte opção e por isso vou falar mais dela. Essa opção
   faz algumas perguntas e elas são auto-explicativas e o único cuidado mesmo é
   o de sempre usar dois dígitos nas respostas de dia e mês, e quando preciso,
   4 dígitos para anos. O formato para horas é 'HHMM', ou seja, dois dígitos para
   horas (de 0 a 23), e dois dígitos para os minutos (de 0 a 59). Não Use os :
   (dois pontos). Exemplos:

      1200 1630 0817

   Com relação as semanas, para simplificar e facilitar o agendamento a seguinte
     correspondência foi adotado:

     "1" para domingo.

     "2" para segunda. (Como é fácil notar a maioria dos números tem uma relação
         com o nome do dia da semana, e é expressa em 1 digito apenas.)

     "3" para terça.

     "4" para quarta.

     "5" para quinta.

     "6" para sexta.

     "7" para sábado.


   Você poderá digitar mais de uma opção nas respostas para as perguntas. Se
   você colocou vários dias e vários meses no agendamento de um compromisso então o
   compromisso será agendado para aqueles dias em todos os meses que você colocou. Por
   exemplo, coloquei os dias 05 e 06 e o mês 08 e 09, então serão agendados os
   compromissos para o dia 05 e 06 do mês 08 e 05 e 06 do mês 09.

   Algumas perguntas quando não respondidas assumirão uma resposta padrão, mas isto
   é indicado na própria pergunta. Isto acontece para tornar as coisas mais ágeis.

   Quando você digitar 'x' (minúsculo) nas respostas das perguntas de Ano, Mês, Dia,
   Dia Da Semana ou horas, então os avisos de compromissos assumirão o sequinte valor:

   Anos  - o ano será anotado como A@@@, A de (A)nos, e na execução do script
   isso será substituido pelo ano atual. Em outras palavras o compromisso será
   exibido em todo os anos em que a data se tornar verdadeira (Se você responder 'x'
   em tudo, os compromissos estes serão exibidos todos os anos, todos os meses,
   todos os dias, de hora em hora).

   O mesmo acontece com as outras opções:

   M@    representa todos (M)eses.
   D@    representa todos (D)ias.
   S@@   representa todos dias da (S)emana.
   H@@@@ representa todos (H)oras (no caso de horas o aviso será executado de hora em
         hora e não de minuto em minuto).


   Para torna-lo ainda mais ágel recomendo criar, dentro do seu arquivo '.bashrc',
   um aliás para que este script seja executado como se fosse um comando, apenas
   digitando um nome, sugiro 'agenda'. Para isto abra o arquivo '.bashrc', em seu
   diretório 'home' e próximo do final do arquivo aonde tem várias linhas começada
   pela palavra 'alias' acrescente a seguinte linha:
      alias agenda='bash /home/$USER/agenda.sh'

   NOTE: O endereço acima '/home/$USER/agenda.sh' é válido somente se você tiver
   deixado o script 'agenda.sh' dentro do diretório 'home', caso contrário, ajuste
   o caminho correspondente.


   Um outro detalhe em adição ao anterior é que este script aceita o uso de
   parâmetros. Por exemplo, você pode apenas querer agendar um compromisso rapidamente
   e nada mais que isso. Então, em vez de você executar o script 'agenda.sh' e
   depois procurar a opção de agendamento teclando 'ENTER' e teclando '1' você
   pode encurtar isto digitando no terminal 'agenda 1' (se seu arquivo '.bashrc'
   estiver editado conforme dica anterior ou bash agenda.sh 1) e ele abrirá o script
   já na opção de agendamento.

   Os parâmetros aceitos são:

      '0' para iniciar a função cronometro'.

      '1' ou 'agendamento' para fazer os agendamentos de compromissos.

      '2' ou 'editar' para editar compromissos.
 
       '2' ou 'todos' para visualizar todos os compromissos.
 
       '3' ou 'mes' para escolher um mês e visualizar os compromissos dele.
 
       '4' ou 'alterar' para alterar um compromisso agendado.
 
       '5' ou 'deletar' para deletar um deletar um compromisso.

      '-h' ou '--help' ou 'h' ou 'help' para acessar esta ajuda.

      '-H' ou 'H' para ajuda mais completa.

      'dxx', onde 'x' são números 0-9, (exemplo d09), ('d' de dia), para ver compromissos
	   do dia xx para o mês e ano atual.

      'mxx', onde 'x' são números 0-9, (exemplo m02), ('m' de mês), para ver compromissos
	   do mês xx do ano atual.

      'axx', onde 'x' são números 0-9, (exemplo a13), ('a' de ano), para ver compromissos
	   do ano xx.

      'axxxx', onde 'x' são números 0-9, (exemplo a2013), ('a' de ano), para ver compromissos
	   do ano xxxx.

      'xx-xxxx', onde 'x' são números 0-9, (exemplo 02-2013), para ver compromissos do
	   mes-ano xx-xxxx.

      'xxxx-xx', onde 'x' são números 0-9, (exemplo 2013-02), para ver compromissos do
	   ano-mes xxxx-xx.

      'xx-xx-xxxx', onde 'x' são números 0-9, (exemplo 15-02-2013), para ver compromissos
	   do dia-mes-ano.

      'xxxx-xx-xx', onde 'x' são números 0-9, (exemplo 2013-02-2013), para ver compromissos
	   do ano-mes-dia.

      '+x', onde 'x' são números 0-9, (exemplo +7), para ver os compromissos do 7º dia a frente.

      '++x', onde 'x' são números 0-9, (exemplo ++7), para ver compromissos de hoje até o
	   7º dia a frente.

   Uma última recomendação é o de testar a execução deste script mo sistema
   bem antes de usá-lo pra valer apenas para garantir que todas as configurações
   estejam corretas.
