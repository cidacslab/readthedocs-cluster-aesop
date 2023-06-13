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
As filas disponíveis no cluster estão mostradas abaixo.

.. code-block:: bash

  [user@login1 ~]$ sinfo
  PARTITION     AVAIL  TIMELIMIT  NODES  STATE NODELIST
  cpu              up   infinite      1   idle c002
  cpu_iterativo    up   infinite      1    mix c001
  gpu              up   infinite      1  down* gpu1
  gpu_iterativo    up   infinite      1  down* gpu1


Jobs
====
Jobs são formados por uma ou várias etapas sequenciais, cada uma consistindo 
de uma ou várias tarefas paralelas que serão encaminhados para os nós de processamento, de acordo com seus respectivos recursos, tais como: 
CPUs, GPUs, memória, etc; que serão alocados pelo **SLURM**.

Um *job script* é um script em *shell*, por exemplo um script *Bash*, cujos comentários que começam por ``#BATCH`` serão entendidos pelo **SLURM**
como parâmetros que descrevem solicitações de recursos e outras opções de submissão.

.. important::

  As diretivas ``#BATCH`` devem aparecer no início do arquivo de submissão, antes de qualquer outra linha, exceto a primeira que deve ter o ``#!/bin/bash``.

.. important::

  É importante ressaltar que todo o job executado através do sistema de fila, o resultado não será exibido na tela. Tudo o que o programa escrever
  será redirecionado para um arquivo que é definido pelo parametro ``--output``. No caso de omissão deste parâmetro, o arquivo de saída será o nome do 
  job mais o seu *jobid*, por exemplo, ``slurm-2732.out``. 


Exemplos de Scripts
===================

