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

O comando abaixo lista os módulos disponiveis. É importante observar que os módulos são separados por 
grupos. Deve-se ter o cuidado de utiliza-lo de forma correta. Por exemplo, os modulos abaixo do 
``/opt/images/spack/share/lmod/gcc/13.1.0`` devem ser utilizado junto com o compilador GCC versão 13.1.0. Outro exemplo, uma das 
implementações do padrão MPI é feita através do ``openmpi``.

.. code-block:: bash

  user@login1:~> module avail

  ------------------------------------------------------- /usr/share/lmod/lmod/modulefiles -------------------------------------------------------
  Core/lmod   Core/settarg (D)

  ----------------------------------------------------- /opt/images/modulefiles --------------------------------------------------------
  openmpi/4.1.2a1   openmpi/4.1.4         rstudio_singularity/3.6.2           rstudio_singularity/4.2.0 (D)
  openmpi/4.1.3     python/3.6-jupyter    rstudio_singularity/4.2.0-custom    spark/3.2.2

  --------------------------------------------- /opt/images/spack/share/lmod/gcc/13.1.0 ------------------------------------------------
  autoconf-archive/2023.02.20-46o     gdbm/1.23-4v5               libpciaccess/0.17-jny   ncurses/6.4-snx         tar/1.34-wbi
  autoconf/2.69-az5                   gettext/0.21.1-m7u          libpng/1.6.39-65w       numactl/2.0.14-z2h      tcsh/6.24.00-b7s
  automake/1.16.5-zs4                 gmake/4.4.1-6o6             libsigsegv/2.14-vwn     openmpi/4.1.5-t25 (D)   texinfo/7.0.3-abp
  berkeley-db/18.1.40-tyl             gmp/6.2.1-6ca               libtirpc/1.2.6-7tq      openssh/9.2p1-u5p       time/1.9-6js
  bison/3.8.2-blf                     hwloc/2.9.1-x76             libtool/2.4.7-5io       openssl/1.1.1t-mo3      util-macros/1.19.3-qom
  bzip2/1.0.8-nfj                     jasper/2.0.32-xue           libxcrypt/4.4.33-bol    patch/2.7.6-26x         xz/5.4.1-bq5
  c-blosc/1.21.2-rno                  krb5/1.20.1-oxy             libxml2/2.10.3-dqi      perl/5.36.0-56j         zlib/1.2.13-ixd
  ca-certificates-mozilla/2023-csd    libaec/1.0.6-caj            lz4/1.9.4-nwv           pigz/2.7-f24            zstd/1.5.5-wys
  cmake/3.26.3-26r                    libedit/3.1-20210216-ks5    m4/1.4.19-7um           pkgconf/1.9.5-t5y
  diffutils/3.9-qeq                   libevent/2.1.12-fo4         mpc/1.3.1-s37           pmix/4.2.3-3qq
  gawk/5.2.1-a6o                      libiconv/1.17-xzr           mpfr/4.2.0-qbu          readline/8.2-re5
  gcc/13.1.0-z7b                      libjpeg-turbo/2.1.5-smy     nasm/2.15.05-upr        snappy/1.1.10-oil

  ---------------------------------- /opt/images/spack/share/lmod/openmpi/4.1.5-t252iac/gcc/13.1.0 -------------------------------------
  hdf5/1.10.9-b4h       netcdf-fortran/4.6.0-ryp      wps/4.5-bt7       wrf/4.4.2-serial    wrf/4.4.2-2eg (D)
  netcdf-c/4.9.2-adn    parallel-netcdf/1.12.3-6iz    wrf/4.4.2-dmpar   wrf/4.4.2-slp

  ---------------------------------------------- /usr/share/lmod/lmod/modulefiles/Core -------------------------------------------------
  lmod    settarg (D)

    Where:
     D:  Default Module
  
  If the avail list is too long consider trying:
  
  "module --default avail" or "ml -d av" to just list the default modules.
  "module overview" or "ml ov" to display the number of modules for each name.
  
  Use "module spider" to find all possible modules and extensions.
  Use "module keyword key1 key2 ..." to search for all possible modules matching any of the "keys".


.. note::
  
  Repare os diretórios dos modulefiles. Eles mostram a dependência entre os pacotes. Por exemplo, os 
  modules abaixo do diretório ``/opt/images/spack/share/lmod/gcc/13.1.0`` são os pacotes que foram 
  compilados usando o compilador ``gcc`` versão 13.1.0. 
  O mesmo acontece em outros diretórios. Recomenda-se que utilize o mesmo compilador, no caso de 
  no script de submissão do job.

Obtendo informações sobre os módulos
------------------------------------

.. code-block:: bash

  user@login1:~> module help gcc

-------------- Module Specific Help for "gcc/13.1.0-z7b" --------------------------
The GNU Compiler Collection includes front ends for C, C++, Objective-C,
Fortran, Ada, and Go, as well as libraries for these languages.

.. code-block:: bash

  user@login1:~> module whatis gcc
  gcc/13.1.0-z7b : The GNU Compiler Collection includes front ends for C, C++, Objective-C, Fortran, 
  Ada, and Go, as well as libraries for these languages.

Carregando, listando e descarregando um módulo.

.. code-block:: bash

  [user@login1:~]$ module load gcc/13.1.0-z7b
  [user@login1 ~]$ module list
  
  Currently Loaded Modules:
    1) gcc/13.1.0-z7b

  [user@login1 ~]$ module unload gcc/13.1.0-z7b
  [user@login1 ~]$ module list
  No modules loaded


Dependências
------------

Os módulos, de forma geral, carregam automaticamente os **module** de todas as dependências, 
**excluindo** o compilador.

.. code-block:: bash

 [user1@login1:~]$ module list
 No Modulefiles Currently Loaded.

 [user1@login1:~]$  module load netcdf-c/4.9.2-adn
 [user1@login1 ~]$ module list

 Currently Loaded Modules:
   1) bzip2/1.0.8-nfj     6) c-blosc/1.21.2-rno     11) libxml2/2.10.3-dqi  16) tar/1.34-wbi              21) libxcrypt/4.4.33-bol  26) pkgconf/1.9.5-t5y
   2) lz4/1.9.4-nwv       7) libaec/1.0.6-caj       12) ncurses/6.4-snx     17) gettext/0.21.1-m7u        22) openssh/9.2p1-u5p     27) hdf5/1.10.9-b4h
   3) snappy/1.1.10-oil   8) libpciaccess/0.17-jny  13) hwloc/2.9.1-x76     18) openssl/1.1.1t-mo3        23) libevent/2.1.12-fo4   28) netcdf-c/4.9.2-adn
   4) zlib/1.2.13-ixd     9) libiconv/1.17-xzr      14) numactl/2.0.14-z2h  19) krb5/1.20.1-oxy           24) pmix/4.2.3-3qq
   5) zstd/1.5.5-wys     10) xz/5.4.1-bq5           15) pigz/2.7-f24        20) libedit/3.1-20210216-ks5  25) openmpi/4.1.5-t25
