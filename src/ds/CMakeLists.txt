###########################################################
# CMakeLists for ds module

add_library(ds OBJECT
        src/Root.cc
        src/MCPMT.cc
        src/RunStore.cc)
# Set our include directories
target_include_directories(ds PUBLIC
        $<BUILD_INTERFACE:${RATPAC_INCDIR}>
        $<INSTALL_INTERFACE:include>)

file(COPY include/ DESTINATION ${RATPAC_INCDIR})

#################################################
# Create Root Dictionary

# hack hack hack hack hack
include_directories(${RATPAC_INCDIR})

root_generate_dictionary(G__RATDict
        RAT/DS/Root.hh
        RAT/DS/EV.hh
        RAT/DS/MC.hh
        RAT/DS/MCParticle.hh
        RAT/DS/MCPhoton.hh
        RAT/DS/MCPMT.hh
        RAT/DS/MCSummary.hh
        RAT/DS/PMT.hh
        RAT/DS/RunStore.hh
        RAT/DS/Run.hh
        RAT/DS/PosFit.hh
        RAT/DS/PMTInfo.hh
        RAT/DS/MCTrack.hh
        RAT/DS/MCTrackStep.hh
        RAT/DS/Calib.hh
        RAT/DS/Centroid.hh
        RAT/DS/PathFit.hh
        RAT/DS/BonsaiFit.hh
        RAT/DSReader.hh
        RAT/DSWriter.hh
        RAT/TrackNav.hh
        RAT/TrackNode.hh
        RAT/TrackCursor.hh
        RAT/DB.hh
        RAT/DBLink.hh
        RAT/DBTextLoader.hh
        RAT/DBJsonLoader.hh
        RAT/HTTPDownloader.hh
        RAT/Log.hh
        RAT/ObjInt.hh
        RAT/ObjDbl.hh
        LINKDEF include/RAT/DS/LinkDef.hh
        DEPENDENCIES core ds db io)

add_library(RATDict OBJECT G__RATDict.cxx)
target_include_directories(RATDict PUBLIC
        $<BUILD_INTERFACE:${RATPAC_INCDIR}>
        $<INSTALL_INTERFACE:include>)

# Export the proper dicitonary file to lib
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/libRATDict.rootmap
              ${CMAKE_CURRENT_BINARY_DIR}/libRATDict_rdict.pcm
        DESTINATION lib)
