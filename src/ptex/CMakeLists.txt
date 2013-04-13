set(SRCS
    PtexCache.cpp
    PtexFilters.cpp
    PtexHalf.cpp
    PtexReader.cpp
    PtexSeparableFilter.cpp
    PtexSeparableKernel.cpp
    PtexTriangleFilter.cpp
    PtexTriangleKernel.cpp
    PtexUtils.cpp
    PtexWriter.cpp)

set(HDRS
		PtexCache.h
		PtexDict.h
		PtexHalf.h
		PtexHashMap.h
		PtexInt.h
		PtexIO.h
		PtexMutex.h
		PtexPlatform.h
		PtexReader.h
		PtexSeparableFilter.h
		PtexSeparableKernel.h
		PtexTriangleFilter.h
		PtexTriangleKernel.h
		Ptexture.h
		PtexUtils.h
		PtexWriter.h)

add_library(Ptex_static STATIC ${SRCS} ${HDRS})
set_target_properties(Ptex_static PROPERTIES OUTPUT_NAME Ptex_static COMPILE_FLAGS /DPTEX_STATIC DEBUG_POSTFIX "_d")

add_library(Ptex_dynamic SHARED ${SRCS} ${HDRS})
set_target_properties(Ptex_dynamic PROPERTIES OUTPUT_NAME Ptex DEBUG_POSTFIX "_d")

if (WIN32)
	set_target_properties(Ptex_dynamic PROPERTIES COMPILE_FLAGS /DPTEX_EXPORTS)
endif (WIN32)

target_link_libraries(Ptex_dynamic ${CMAKE_THREAD_LIBS_INIT} ${ZLIB_LIBRARIES})

install(TARGETS Ptex_static Ptex_dynamic
		RUNTIME DESTINATION bin
		LIBRARY DESTINATION lib
		ARCHIVE DESTINATION lib)
		
install(FILES ${HDRS} DESTINATION include)
