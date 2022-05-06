# ======================================================================
#  larsimrad main build file
#
#  cd .../path/to/build/directory
#  source .../path/to/larsimrad/ups/setup_for_development <-d|-p>
#  buildtool [-I /install/path] -bt[i] -jN
# ======================================================================

cmake_minimum_required(VERSION 3.20 FATAL_ERROR)
# cmake_policy(VERSION 3.19) ### MIGRATE-ACTION-COMPATIBILITY (migrate-3.13.00) - Uncomment to preserve compatibility with older CMake versions

find_package(cetmodules REQUIRED)
project(larsimrad VERSION 09.04.15 LANGUAGES CXX)

# cetbuildtools contains our cmake modules

include(CetCMakeEnv)
cet_cmake_env()

# -Wno-unused-variable needed because of CLHEP
cet_set_compiler_flags(DIAGS CAUTIOUS
  WERROR
  NO_UNDEFINED
  EXTRA_FLAGS -pedantic -Wno-unused-local-typedefs -Wno-unused-variable
)

cet_report_compiler_flags() ### MIGRATE-ACTION-RECOMMENDED (migrate-3.13.00) - add args: REPORT_THRESHOLD VERBOSE

find_package(canvas_root_io REQUIRED)
find_package(art REQUIRED EXPORT)
find_package(art_root_io REQUIRED EXPORT)
find_package(nugen REQUIRED EXPORT)
find_package(nurandom REQUIRED EXPORT)
find_package(GSL REQUIRED)

find_package( larcore REQUIRED )
find_package( larcoreobj REQUIRED )
find_package( lardataobj REQUIRED )
find_package( lardataalg REQUIRED )
find_package( lardata REQUIRED )
find_package( larsim REQUIRED )
find_package( bxdecay0 REQUIRED )

# macros for dictionary and simple_plugin
include(ArtDictionary)
include(ArtMake)
include(BuildPlugins)

# source
add_subdirectory(larsimrad)

# tests
#add_subdirectory(test)

# ups - table and config files

# packaging utility
cet_cmake_config()
