# Conceitos-multiprogramacao-e-programacao-concorrente
Conceitos multiprogramação e programação concorrente

Marcelo Morgenstern					GTI Módulo III - Noturno



PROGRAMAÇÃO CONCORRENTE

A programação concorrente foi usada inicialmente na construção de sistemas operacionais. Atualmente, ela é usada para desenvolver aplicações em todas as áreas da computação. Este tipo de programação tornou-se ainda mais importante com o advento dos sistemas distribuídos e das máquinas com arquitetura paralela. Neste capítulo serão apresentados os conceitos básicos e os mecanismos clássicos da programação concorrente.

1 - Definição

A grande maioria dos programas escritos são programas seqüenciais. Nesse caso, existe somente um fluxo de controle (fluxo de execução, linha de execução, thread) no programa. Isso permite, por exemplo, que o programador realize uma "execução imaginária" de seu programa apontando com o dedo, a cada instante, o comando que está sendo executada no momento.
Um programa concorrente pode ser visto como se tivesse vários fluxos de execução. Para o programador realizar agora uma "execução imaginária", ele vai necessitar de vários dedos, um para cada fluxo de controle. 
O termo "programação concorrente" vem do inglês concurrent programming, onde concurrent significa "acontecendo ao mesmo tempo". Uma tradução mais adequada seria programação concomitante. Entretanto, o termo programação concorrente já está solidamente estabelecido no Brasil. Algumas vezes é usado o termo programação paralela com o mesmo sentido.
É comum em sistemas multiusuário que um mesmo programa seja executado simultaneamente por vários usuários. Por exemplo, um editor de texto. Entretanto, ter 10 execuções simultâneas do editor de texto não faz dele um programa concorrente. O que se tem são 10 processos independentes executando o mesmo programa seqüencial (compartilhando o mesmo código). Cada processo tem a sua área de dados e ignora a existência das outras execuções do programa. Esses processos não interagem entre si (não trocam informações). Um programa é considerado concorrente quando ele (o próprio programa, durante a sua execução) origina diferentes processos. Esses processos, em geral, irão interagir entre si.

2 - Motivação

A programação concorrente é mais complexa que a programação seqüencial. Um programa concorrente pode apresentar todos os tipos de erros que aparecem nos programas seqüenciais e, adicionalmente, os erros associados com as interações entre os processos. Muitos erros dependem do exato instante de tempo em que o escalonador do sistema operacional realiza um chaveamento de contexto. Isso torna muitos erros difíceis de reproduzir e de identificar.
Apesar da maior complexidade, existem muitas áreas nas quais a programação concorrente é vantajosa. Em sistemas nos quais existem vários processadores (máquinas paralelas ou sistemas distribuídos), é possível aproveitar esse paralelismo e acelerar a execução do programa. Mesmo em sistemas com um único processador, existem razões para o seu uso em vários tipos de aplicações.
O uso da programação concorrente é natural nas aplicações que apresentam paralelismo intrínseco, ditas aplicações inerentemente paralelas. Nessas aplicações pode-se distinguir facilmente funções para serem realizadas em paralelo. Este é o caso do spooling de impressão, exemplo que será apresentado a seguir. Pode-se dizer que, em geral, a programação concorrente tem aplicação natural na construção de sistemas que tenham de implementar serviços que são requisitados de forma imprevisível .Nesse caso, o programa concorrente terá um processo para realizar cada tipo de serviço. 

3 - Especificação do paralelismo

Para construir um programa concorrente, antes de mais nada, é necessário ter a capacidade de especificar o paralelismo dentro do programa. Essa especificação pode ser feita de diversas maneiras. Uma delas utiliza os comandos fork, quit e join. 
O comando (ou função) fork pode ser implementado de duas maneiras distintas: ele pode criar um novo processo ou criar apenas um novo fluxo de execução dentro de um processo já existente. A função fork retorna um número inteiro que é a identificação do novo processo ou do novo fluxo criado. Um fluxo de execução também é denominado linha de execução ou thread.
Os comandos quit e join são auxiliares ao fork. Quando o comando quit é executado, o processo (ou thread) que o executa termina imediatamente. O comando join(id) bloqueia quem o executa até que termine o processo (ou thread) identificado por id.

Diferença entre thread e processo

O que melhor distingue uma thread de um processo é o espaço de endereçamento. Todas as threads de um processo trabalham no mesmo espaço de endereçamento, que é a memória lógica do “processo hospedeiro”. Isto é, quando se tem um conjunto de threads dentro de um processo, todas as threads executam o código do processo e compartilham as suas variáveis. Por outro lado, quando se tem um conjunto de processos, cada processo trabalha num espaço de endereçamento próprio, com um conjunto separado de variáveis.
No caso de um processo com N threads, tem-se um único registro descritor (o registro do processo hospedeiro) e N mini-descritores de threads. O mini-descritor de cada thread é usado para salvar os valores dos registradores da UCP (PC, PSW, etc.). Adicionalmente, cada thread possui uma pilha, que é usada para as chamadas e retornos de procedimentos. 
É mais fácil chavear a execução entre threads (de um mesmo processo) do que entre processos, pois tem-se menos informações para salvar e restaurar. Por esse motivo, as threads são chamadas também de "processos leves".
BIBLIOGRAFIA
TOSCANI, S., OLIVEIRA, R., CARISSIMI, A., Sistemas Operacionais e Programação Concorrente. Série didática do II-UFRGS, 2003.
