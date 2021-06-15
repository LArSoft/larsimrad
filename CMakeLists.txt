# ======================================================================
#  larsimrad main build file
#
#  cd .../path/to/build/directory
#  source .../path/to/larsimrad/ups/setup_for_development <-d|-p>
#  buildtool [-I /install/path] -bt[i] -jN
# ======================================================================

cmake_minimum_required (VERSION 3.19 FATAL_ERROR)

project(larsimrad VERSION 09.01.09 LANGUAGES CXX)

find_package(cetmodules REQUIRED)
find_package(canvas_root_io)
find_package(art)

include(CetCMakeEnv)
cet_cmake_env()

# -Wno-unused-variable needed because of CLHEP
cet_set_compiler_flags(DIAGS CAUTIOUS
  WERROR
  NO_UNDEFINED
  EXTRA_FLAGS -pedantic -Wno-unused-local-typedefs -Wno-unused-variable
)

cet_report_compiler_flags()

# these are minimum required versions, not the actual product versions
find_ups_product(art_root_io)
find_ups_product( larcore )
find_ups_product( larcoreobj )
find_ups_product( lardataobj )
find_ups_product( lardata )
find_ups_product( larsim )
find_ups_product( bxdecay0 )
find_ups_product( nugen )
find_ups_product( gsl )
find_package( nurandom COMPONENT RandomUtils_NuRandomService_service )

# macros for dictionary and simple_plugin
include(ArtDictionary)
include(ArtMake)
include(BuildPlugins)

# source
add_subdirectory(larsimrad)

# tests
#add_subdirectory(test)

# ups - table and config files
if(WANT_UPS)
add_subdirectory(ups)
endif()

# packaging utility
include(UseCPack)
