set(Sources WASMSerialization.cpp)
set(PublicHeaders ${WAVM_INCLUDE_DIR}/WASM/WASM.h)
include_directories(${WAVM_INCLUDE_DIR}/WASM)

IF(WIN32)
  add_library(WASM SHARED ${Sources} ${PublicHeaders})
ELSE()
  add_library(WASM STATIC ${Sources} ${PublicHeaders})
ENDIF()
add_definitions(-DWEBASSEMBLY_API=DLL_EXPORT)
target_link_libraries(WASM Logging IR)

install(TARGETS WASM
   LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
   ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR})
