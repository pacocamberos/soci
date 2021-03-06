###############################################################################
#
# This file is part of CMake configuration for SOCI library
#
# Copyright (C) 2010 Mateusz Loskot <mateusz@loskot.net>
# Distributed under the Boost Software License, Version 1.0.
# (See accompanying file LICENSE_1_0.txt or copy at
# http://www.boost.org/LICENSE_1_0.txt)
#
###############################################################################

include(CMakeDependentOption)

option(SOCI_POSTGRESQL_NOPARAMS
  "Do not use input parameters. PostgreSQL 7.x portability."
  OFF)

option(SOCI_POSTGRESQL_NOBINDBYNAME
  "Disable query rewriting to native form. PostgreSQL 7.0 portability."
  OFF)

cmake_dependent_option(SOCI_POSTGRESQL_NOPREPARE
  "Disable prepared statements. Set ON if SOCI_POSTGRESQL_NOBINDBYNAME is ON. PostgreSQL 7.0 portability." ON
  SOCI_POSTGRESQL_NOBINDBYNAME OFF)

if(SOCI_POSTGRESQL_NOPARAMS)
  add_definitions(-DSOCI_POSTGRESQL_NOPARAMS=1)
endif()

if(SOCI_POSTGRESQL_NOBINDBYNAME)
message("X")
  add_definitions(-DSOCI_POSTGRESQL_NOBINDBYNAME=1)
endif()

if(SOCI_POSTGRESQL_NOPREPARE)
message("Y")
  add_definitions(-DSOCI_POSTGRESQL_NOPREPARE=1)
endif()

soci_backend(PostgreSQL
  DEPENDS PostgreSQL
  HEADERS soci-postgresql.h common.h
  DESCRIPTION "SOCI backend for PostgreSQL database engine"
  AUTHORS "Maciej Sobczak, Stephen Hutton"
  MAINTAINERS "Maciej Sobczak")

add_subdirectory(test)
