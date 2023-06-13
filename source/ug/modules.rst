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
  
  ------------------------------------------------------- /opt/images/spack/share/lmod/gcc/12.2.0 ----------------------------------------------------------
     autoconf/2.69-avy                         gettext/0.21.1-y2v              libjpeg-turbo/2.1.3-cxs    ncurses/6.3-kib       readline/8.1.2-nyx
     automake/1.16.5-ypt                       hwloc/2.8.0-6da                 libpciaccess/0.16-wvs      numactl/2.0.14-2dm    tar/1.34-htd
     berkeley-db/18.1.40-7qf                   jasper/2.0.32-5yg               libpng/1.6.37-woj          openmpi/4.1.4-uya     tcsh/6.24.00-sf5
     bison/3.8.2-wvt                           jasper/3.0.3-dje         (D)    libsigsegv/2.13-zxg        openssh/9.1p1-wtz     time/1.9-ryh
     bzip2/1.0.8-qfr                           krb5/1.19.3-fvw                 libtirpc/1.2.6-eue         openssl/1.1.1s-uqi    util-macros/1.19.3-zav
     ca-certificates-mozilla/2022-10-11-rg2    libaec/1.0.6-al5                libtool/2.4.7-pj7          perl/5.36.0-bzc       xz/5.2.7-vow
     cmake/3.24.3-kex                          libedit/3.1-20210216-2ox        libxml2/2.10.1-dba         pigz/2.7-mr6          zlib/1.2.13-lct
     diffutils/3.8-5wz                         libevent/2.1.12-net             m4/1.4.19-ef4              pkgconf/1.8.0-qzo     zstd/1.5.2-2xw
     gdbm/1.23-3ak                             libiconv/1.16-grt               nasm/2.15.05-qre           pmix/4.1.2-p7f
  
  ---------------------------------------------- /opt/images/spack/share/lmod/openmpi/4.1.4-uyavddi/gcc/12.2.0 ---------------------------------------------
   hdf5/1.12.2-ahr       netcdf-fortran/4.6.0-cue      wps/4.3.1-dmpar    wps/4.3.1-nry           wrf/4.4-pbu      wrf/4.4-serial
   netcdf-c/4.9.0-4b7    parallel-netcdf/1.12.3-lna    wps/4.3.1-jup      wps/4.3.1-serial (D)    wrf/4.4-dmpar    wrf/4.4-w3r    (D)

    Where:
     D:  Default Module
  
  If the avail list is too long consider trying:
  
  "module --default avail" or "ml -d av" to just list the default modules.
  "module overview" or "ml ov" to display the number of modules for each name.
  
  Use "module spider" to find all possible modules and extensions.
  Use "module keyword key1 key2 ..." to search for all possible modules matching any of the "keys".


.. note::
  
  Repare os diretórios dos modulefiles. Eles mostram a dependência entre os pacotes. Por exemplo, os modules abaixo do 
  diretório ``/opt/images/spack/share/lmod/gcc/12.2.0`` são os pacotes que foram compilados usando o compilador ``gcc`` versão 12.2.0. 
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

Os módulos, de forma geral, carregam automaticamente os **module** de todas as dependências, **excluindo** o compilador.

.. code-block:: bash

 [user1@login1:~]$ module list
 No Modulefiles Currently Loaded.
 [user1@login1:~]$ module load netcdf-c/4.9.0-4b7
 [user1@login1 ~]$ module list
  
  Currently Loaded Modules:
    1) libaec/1.0.6-al5        5) zlib/1.2.13-lct      9) numactl/2.0.14-2dm  13) tar/1.34-htd        17) libedit/3.1-20210216-2ox  21) openmpi/4.1.4-uya
    2) libpciaccess/0.16-wvs   6) libxml2/2.10.1-dba  10) bzip2/1.0.8-qfr     14) gettext/0.21.1-y2v  18) openssh/9.1p1-wtz         22) pkgconf/1.8.0-qzo
    3) libiconv/1.16-grt       7) ncurses/6.3-kib     11) pigz/2.7-mr6        15) openssl/1.1.1s-uqi  19) libevent/2.1.12-net       23) hdf5/1.12.2-ahr
    4) xz/5.2.7-vow            8) hwloc/2.8.0-6da     12) zstd/1.5.2-2xw      16) krb5/1.19.3-fvw     20) pmix/4.1.2-p7f            24) netcdf-c/4.9.0-4b7
