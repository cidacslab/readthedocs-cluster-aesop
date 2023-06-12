*****
SLURM
*****

.. contents:: Conteudo

Introducao
==========

O gerenciador de filas utilizado no cluster e o `SLURM Workload Manager <https://slurm.schedmd.com/>`_. 
Ele e um agendador de tarefas gratuito e de codigo aberto.

Comandos basicos
================
.. list-table:: Comandos basicos
    :align: center
    :header-rows: 1

    * - Comando
      - Descricao
      - Exemplo
    * - ``sbatch``
      - Submite um job script
      - ``sbatch test.job``
    * - ``sinfo``
      - Informa o estado das particoes e nos gerenciados pelo SLURM
      - ``sinfo``
    * - ``squeue``
      - Informa estado dos **jobs**
      - ``squeue``
    * - ``scancel``
      - Cancela um job pendente ou em execucao
      - ``scancel 1234``

SLURM Partitions
================
As filas disponiveis no cluster estao mostradas abaixo.

.. code-block:: bash
  [user@login1 ~]$ sinfo
  PARTITION     AVAIL  TIMELIMIT  NODES  STATE NODELIST
  cpu              up   infinite      1   idle c002
  cpu_iterativo    up   infinite      1    mix c001
  gpu              up   infinite      1  down* gpu1
  gpu_iterativo    up   infinite      1  down* gpu1


Exemplos de Scripts
===================

