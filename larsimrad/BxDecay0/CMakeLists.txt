cet_make_library(LIBRARY_NAME RadioGen INTERFACE
  SOURCE BaseRadioGen.h
  LIBRARIES INTERFACE
  lardata::DetectorPropertiesService
  larcore::Geometry_Geometry_service
  larcoreobj::SummaryData
  nugen::EventGeneratorBase
  nusimdata::SimulationBase
  nurandom::RandomUtils_NuRandomService_service
  art_root_io::TFileService_service
  art::Framework_Principal
  art::Framework_Services_Registry
  messagefacility::MF_MessageLogger
  fhiclcpp::fhiclcpp
  cetlib::cetlib
  cetlib::container_algorithms
  cetlib_except::cetlib_except
  ROOT::Core
  ROOT::EG
  ROOT::Geom
  ROOT::Gpad
  ROOT::Hist
  ROOT::MathCore
  ROOT::Physics
  CLHEP::Random
)

cet_write_plugin_builder(lar::RadioGenModule art::EDProducer Modules
  INSTALL_BUILDER
  LIBRARIES CONDITIONAL
  larsimrad::RadioGen
)

include(lar::RadioGenModule)

cet_build_plugin(Decay0Gen lar::RadioGenModule
  LIBRARIES PRIVATE
  BxDecay0::BxDecay0
)

cet_build_plugin(SpectrumVolumeGen lar::RadioGenModule)

install_headers()
install_fhicl()
install_source()
