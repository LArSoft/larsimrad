# ======================================================================
#  larsimrad main build file
#
#  cd .../path/to/build/directory
#  source .../path/to/larsimrad/ups/setup_for_development <-d|-p>
#  buildtool [-I /install/path] -bt[i] -jN
# ======================================================================

cmake_minimum_required(VERSION 3.20 FATAL_ERROR)

find_package(cetmodules REQUIRED)
project(larsimrad VERSION 10.00.03 LANGUAGES CXX)

include(CetCMakeEnv)
cet_cmake_env()

cet_set_compiler_flags(DIAGS CAUTIOUS
  WERROR
  NO_UNDEFINED
  EXTRA_FLAGS -pedantic
)

cet_report_compiler_flags(REPORT_THRESHOLD VERBOSE)

find_package(larcore REQUIRED EXPORT)
find_package(larcoreobj REQUIRED EXPORT)
find_package(lardataobj REQUIRED EXPORT)
find_package(lardata REQUIRED EXPORT)

find_package(nugen REQUIRED EXPORT)
find_package(nurandom REQUIRED EXPORT)
find_package(nusimdata REQUIRED EXPORT)

find_package(art REQUIRED EXPORT)
find_package(art_root_io REQUIRED EXPORT)
find_package(fhiclcpp REQUIRED EXPORT)
find_package(cetlib REQUIRED EXPORT)
find_package(cetlib_except REQUIRED EXPORT)

if (DEFINED ENV{BXDECAY0_LIB})
  set(BxDecay0_DIR $ENV{BXDECAY0_LIB}/cmake/BxDecay0)
endif()
find_package(BxDecay0 REQUIRED EXPORT)
find_package(CLHEP COMPONENTS Random REQUIRED EXPORT)
find_package(ROOT COMPONENTS Core EG Geom Gpad Hist Physics)

# macros for dictionary and simple_plugin
include(CetMake)
include(BuildPlugins)

cet_cmake_module_directories(Modules BINARY)

# source
add_subdirectory(larsimrad)

# packaging utility
cet_cmake_config()
