.. modules

******************
Module Environment
******************

.. contents:: Conteúdo

Introdução
==========

O module é usado para facilitar o chaveamento de ambientes de programação. Esta ferramenta permite que o usuário escolha qual(is) ferramenta(s) deseja usar, como por exemplo, versão do compilador, biblioteca matemática, MPI, etc.

Utilização do Module
====================

Comandos basicos do module.

+-------------------------------------------+---------------------------------------------+
| Comando                                   | Descrição                                   |
+===========================================+=============================================+
| module list                               | lista os módulos carregados                 |
+-------------------------------------------+---------------------------------------------+
| module avail                              | lista os módulos disponiveis                |
+-------------------------------------------+---------------------------------------------+
| module help [modulefile]                  | mostra a sintaxe do comando module          |
+-------------------------------------------+---------------------------------------------+
| module load modulefile [modulefile ...]   | carrega o(s) módulo(s) correspondente(s)    |
+-------------------------------------------+---------------------------------------------+
| module unload modulefile [modulefile ...] | descarrega o(s) módulo(s) correspondente(s) |
+-------------------------------------------+---------------------------------------------+

Exemplos de Uso do Module
=========================

Segue abaixo alguns exemplos de como utilizar o comando module.
Nenhum módulo é carregado por padrão.

.. code-block:: bash

   user@login1:~> module list
   No Modulefiles Currently Loaded.

O comando abaixo lista os módulos disponiveis. É importante observar que os módulos são separados por grupos. Deve-se ter o cuidado de utiliza-lo de forma correta. Por exemplo, os modulos abaixo do ``/sw/apps/pgi16/modulefiles`` devem ser utilizado junto com o compilador PGI. Outro exemplo, uma das implementações do padrão MPI é feita através do ``mvapich`` e este por sua vez tem 3 versões diferentes, uma para cada compilador (PGI, Intel e GNU).

.. code-block:: bash

  user@login1:~> module avail
  
  ------------------------------------------------------------ /usr/share/lmod/lmod/modulefiles ------------------------------------------------------------
     Core/lmod    Core/settarg

  ---------------------------------------------------------------- /opt/images/modulefiles -----------------------------------------------------------------
     openmpi/4.1.2a1    openmpi/4.1.4      (D)    rstudio_singularity/3.6.2           rstudio_singularity/4.2.0 (D)
     openmpi/4.1.3      python/3.6-jupyter        rstudio_singularity/4.2.0-custom    spark/3.2.2

  --------------------------------------------------------- /usr/share/lmod/lmod/modulefiles/Core ----------------------------------------------------------
     lmod    settarg
  
  ---------------------------------------------------------- /opt/images/spack/share/modulefiles -----------------------------------------------------------
     autoconf/2.69-avy                         jasper/3.0.3-dje         (D)    nasm/2.15.05-qre                            tar/1.34-htd
     automake/1.16.5-ypt                       krb5/1.19.3-fvw                 ncurses/6.3-kib                             tcsh/6.24.00-sf5
     berkeley-db/18.1.40-7qf                   libaec/1.0.6-al5                netcdf-c/4.9.0-openmpi-4.1.4-4b7            time/1.9-ryh
     bison/3.8.2-wvt                           libedit/3.1-20210216-2ox        netcdf-fortran/4.6.0-openmpi-4.1.4-cue      util-macros/1.19.3-zav
     bzip2/1.0.8-qfr                           libevent/2.1.12-net             numactl/2.0.14-2dm                          wps/4.3.1-openmpi-4.1.4-jup
     ca-certificates-mozilla/2022-10-11-rg2    libiconv/1.16-grt               openmpi/4.1.4-uya                           wps/4.3.1-openmpi-4.1.4-nry  (D)
     cmake/3.24.3-kex                          libjpeg-turbo/2.1.3-cxs         openssh/9.1p1-wtz                           wrf/4.4-openmpi-4.1.4-pbu
     diffutils/3.8-5wz                         libpciaccess/0.16-wvs           openssl/1.1.1s-uqi                          wrf/4.4-openmpi-4.1.4-dmpar
     gcc/12.2.0-vuo3f                          libpng/1.6.37-woj               parallel-netcdf/1.12.3-openmpi-4.1.4-lna    wrf/4.4-openmpi-4.1.4-serial
     gdbm/1.23-3ak                             libsigsegv/2.13-zxg             perl/5.36.0-bzc                             wrf/4.4-openmpi-4.1.4-w3r    (D)
     gettext/0.21.1-y2v                        libtirpc/1.2.6-eue              pigz/2.7-mr6                                xz/5.2.7-vow
     hdf5/1.12.2-openmpi-4.1.4-ahr             libtool/2.4.7-pj7               pkgconf/1.8.0-qzo                           zlib/1.2.13-lct
     hwloc/2.8.0-6da                           libxml2/2.10.1-dba              pmix/4.1.2-p7f                              zstd/1.5.2-2xw
     jasper/2.0.32-5yg                         m4/1.4.19-ef4                   readline/8.1.2-nyx
  
    Where:
     D:  Default Module
  
  If the avail list is too long consider trying:
  
  "module --default avail" or "ml -d av" to just list the default modules.
  "module overview" or "ml ov" to display the number of modules for each name.

Use "module spider" to find all possible modules and extensions.
Use "module keyword key1 key2 ..." to search for all possible modules matching any of the "keys".


.. note::
  
  Repare os diretórios dos modulefiles. Eles mostram a dependência entre os pacotes. Por exemplo, os modules abaixo do 
  diretório ``/opt/images/spack/share/modulefiles`` são os pacotes que foram compilados usando o package manager spack. 
  O mesmo acontece em outros diretórios. Recomenda-se que utilize o mesmo compilador, no caso de dependência de pacotes, 
  para evitar problemas de incompatibilidade.

.. warning::

  Os modules (incluindo as versões) utilizados para compilar **devem ser os mesmos** a serem incluidos no script de submissão do job.

Obtendo informações sobre os módulos
------------------------------------

.. code-block:: bash

  user@login1:~> module help gcc

------------------------ Module Specific Help for "gcc/12.2.0-vuo3f" ------------------------------------
The GNU Compiler Collection includes front ends for C, C++, Objective-C,
Fortran, Ada, and Go, as well as libraries for these languages.

.. code-block:: bash

  user@login1:~> module whatis gcc
  gcc/12.2.0-vuo3f : The GNU Compiler Collection includes front ends for C, C++, Objective-C, Fortran, Ada, and Go, as well as libraries for these languages.

Carregando, listando e descarregando um módulo.

.. code-block:: bash

  [user@login1:~]$ module load gcc/12.2.0-vuo3f
  [user@login1 ~]$ module list
  
  Currently Loaded Modules:
    1) gcc/12.2.0-vuo3f

  [user@login1 ~]$ module unload gcc/12.2.0-vuo3f
  [user@login1 ~]$ module list
  No modules loaded


Dependências
------------

Alguns modulos carregam um module de todas as dependências, **excluindo** o compilador são carregadas.

.. code-block:: bash

 [user1@login1:~]$ module list
 No Modulefiles Currently Loaded.
 [user1@login1:~]$ module load netcdf-c
 