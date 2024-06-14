include(${CMAKE_SOURCE_DIR}/cmake/pr_common.cmake)

set(PROJ_NAME HLLib)
pr_add_library(${PROJ_NAME} SHARED)

pr_add_external_dependency(${PROJ_NAME} zlib LIBRARY PUBLIC)
pr_add_external_dependency(${PROJ_NAME} zlib_build HEADER_ONLY PUBLIC)

pr_add_headers(${PROJ_NAME} "HLLib/")
pr_add_sources(${PROJ_NAME} "HLLib/")

pr_add_compile_definitions(${PROJ_NAME} -DHLLIB_EXPORTS=1 -DUSE_ZLIB=1)

if(UNIX)
	target_compile_options(${PROJ_NAME} PRIVATE -O2 -g -fpic -funroll-loops -fvisibility=hidden)
	target_link_options(${PROJ_NAME} PRIVATE -shared -Wl,-soname,libhl.so.2)
endif()

pr_finalize(${PROJ_NAME})
