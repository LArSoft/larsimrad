include_directories ( $ENV{NUGEN_INC} ) ### MIGRATE-ACTION-RECOMMENDED (migrate-3.13.00) - avoid directory-scope functions: use target_link_libraries() with target semantics or target_include_directories() whenever possible
cet_find_library( BXDECAY0 NAMES BxDecay0 PATHS ENV BXDECAY0_LIB NO_DEFAULT_PATH ) ### MIGRATE-ACTION-REQUIRED (migrate-3.13.00) - avoid: use find_package() with custom Find<pkg>.cmake for Spack compatibility

art_make(MODULE_LIBRARIES
         larsim_Simulation
         lardataalg_DetectorInfo
         lardataobj_Simulation
         nusimdata::SimulationBase
         larcoreobj_SummaryData
         larcorealg_Geometry
         larcore_Geometry_Geometry_service
         nurandom::RandomUtils_NuRandomService_service
         BXDECAY0
         art::Framework_Services_Registry
         art_root_io::tfile_support
         art_root_io::TFileService_service
         art::Persistency_Provenance
         messagefacility::MF_MessageLogger
         ROOT::Core
         ROOT::EG
         ROOT::Geom
        ) ### MIGRATE-ACTION-RECOMMENDED (migrate-3.13.00) - deprecated: use art_make_library(), art_dictonary(), and cet_build_plugin() with explicit source lists and plugin base types

install_headers()
install_fhicl()
install_source()
