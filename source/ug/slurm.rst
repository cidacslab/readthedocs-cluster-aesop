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
