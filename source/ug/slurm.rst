*****
SLURM
*****

.. contents:: Conteudo

Introdução
==========

O gerenciador de filas utilizado no cluster é o `SLURM Workload Manager <https://slurm.schedmd.com/>`_. 
Ele é um agendador de tarefas gratuito e de código aberto.

Comandos básicos
================
.. list-table:: Comandos básicos
    :align: center
    :header-rows: 1

    * - Comando
      - Descrição
      - Exemplo
    * - ``sbatch``
      - Submite um job script
      - ``sbatch test.job``
    * - ``sinfo``
      - Informa o estado das partições e nos gerenciados pelo SLURM
      - ``sinfo``
    * - ``squeue``
      - Informa estado dos **jobs**
      - ``squeue``
    * - ``scancel``
      - Cancela um job pendente ou em execucao
      - ``scancel 1234``

SLURM Partitions
================
Atualmente existem quatro filas filas disponíveis no cluster que são:

.. list-table:: Filas
    :align: center
    :header-rows: 1

    * - Fila
      - Descrição
    * - ``cpu``
      - fila para jobs que utilizam apenas CPUs
    * - ``cpu_iterativo``
      - fila para sessão iterativa que utiliza, apenas CPUs
    * - ``gpu``
      - fila para jobs que utilizam GPUs
    * - ``gpu_iterativo``
      - fila para sessão iterativa que utiliza GPUs

O comando abaixo mostra as filas.

.. code-block:: bash

  [user@login1 ~]$ sinfo
  PARTITION     AVAIL  TIMELIMIT  NODES  STATE NODELIST
  cpu              up   infinite      1   idle c002
  cpu_iterativo    up   infinite      1    mix c001
  gpu              up   infinite      1   idle gpu1
  gpu_iterativo    up   infinite      1   idle gpu1


Jobs
====
Jobs são formados por uma ou várias etapas sequenciais, cada uma consistindo 
de uma ou várias tarefas paralelas que serão encaminhados para os nós de processamento, de acordo com seus respectivos recursos, tais como: 
CPUs, GPUs, memória, etc; que serão alocados pelo **SLURM**.

Um *job script* é um script em *shell*, por exemplo um script *Bash*, cujos comentários que começam por ``#BATCH`` serão entendidos pelo **SLURM**
como parâmetros que descrevem solicitações de recursos e outras opções de submissão.

.. important::

  As diretivas ``#BATCH`` devem aparecer no início do arquivo de submissão, antes de qualquer outra linha, exceto a primeira que deve ter o 
  *shell* usado, normalmente, ``#!/bin/bash``.

.. important::

  É importante ressaltar que todo o job executado através do sistema de fila, o resultado não será exibido na tela. Tudo o que o programa escrever
  será redirecionado para um arquivo que é definido pelo parametro ``--output``. No caso de omissão deste parâmetro, o arquivo de saída será o nome do 
  job mais o seu *jobid*, por exemplo, ``slurm-2732.out``. 

.. list-table:: Principais parâmetros utilizados nos jobs
    :align: center
    :header-rows: 1

    * - Parâmetro
      - Função
    * - ``-N``, ``--nodes``
      - número de nós a ser alocados
    * - ``-n``, ``--ntasks``
      - número total de processos
    * - ``-c``, ``--cpus-per-task``
      - número de *threads*
    * - ``--ntasks-per-node``
      - número de processos por nó
    * - ``-p``, ``--partition``
      - seleciona a partição/fila para execução
    * - ``-J``, ``--job-name``
      - nome do job
    * - ``-o``, ``--output``
      - nome do arquivo de saída do job
    * - ``-e``, ``--error``
      - nome do arquivo de saída pra os erros de execução do job
    * - ``--time``
      - define o tempo máximo de execução 
    * - ``--exclusive``
      - aloca o nó para uso exclusivo


Exemplos de Scripts
===================

Suponha o job abaixo com o nome de ``teste.job``.

.. code-block:: bash

  #!/bin/bash
  #SBATCH --nodes=1
  #SBATCH --ntasks=128
  #SBATCH --partition=cpu
  #SBATCH --job-name=teste
  #SBATCH --output=%x-%j.out
  #SBATCH --error=%x-%j.err
  #SBATCH --time=12:00:00
  
  # entra no diretorio de submissao
  cd $SLURM_SUBMIT_DIR 

  # carrega o modules
  module load gcc/12.2.0

  # executa o programa
  ./teste


Para submeter o job acima basta digitar o comando abaixo. O número ``3125``
corresponde ao *jobid* que identifica o job no SLURM.

.. code-block:: bash

  [user@login1 test]$ sbatch teste.job
  Submitted batch job 3125

Ao terminar a execução deste job será gerado um arquivo com o nome 
``teste-3125.out``. Onde a primeira parte do nome corresponde
ao *nome do job* e a segunda parte corresponde ao *jobid* do job,
ambos definidos no script.