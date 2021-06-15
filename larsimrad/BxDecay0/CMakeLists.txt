include_directories ( ENV BXDECAY0_INC )
cet_find_library( BXDECAY0 NAMES BxDecay0 PATHS ENV BXDECAY0_LIB  )

art_make(MODULE_LIBRARIES
         larsim_Simulation
         lardataalg_DetectorInfo
         lardataobj_Simulation
         nusimdata_SimulationBase
         larcoreobj_SummaryData
         larcorealg_Geometry
         larcore_Geometry_Geometry_service
         ${BXDECAY0}
         art::Framework_Services_Registry
         art_root_io::tfile_support
         art_root_io::TFileService_service
         art_Persistency_Provenance
         messagefacility::MF_MessageLogger
         nurandom::RandomUtils_NuRandomService_service
         ROOT::Core
         ROOT::EG
         ROOT::Geom
         ${ROOT_LIBRARIES}
        )

#         ${BxDecay0_LIBRARIES}
install_headers()
install_fhicl()
install_source()
