cmake_minimum_required (VERSION 3.0)
project(lzma)				 

set(CMAKE_C_STANDARD 11)
set(LIBRARY_TYPE "STATIC")

set(CMAKE_INSTALL_INCLUDEDIR ${CMAKE_INSTALL_PREFIX}/include)
set(CMAKE_INSTALL_LIBDIR ${CMAKE_INSTALL_PREFIX}/lib)

if(LINUX)
    set(CMAKE_C_FLAGS "-fPIC" CACHE STRING "" FORCE)
endif()

# add sources
add_library(${PROJECT_NAME} ${LIBRARY_TYPE}
    src/7zAlloc.c
	src/7zArcIn.c
	src/7zBuf.c
	src/7zBuf2.c
	src/7zCrc.c
	src/7zCrcOpt.c
	src/7zDec.c
	src/7zFile.c
	src/7zStream.c
	src/Aes.c
	src/AesOpt.c
	src/Alloc.c
	src/Bcj2.c
	src/Bcj2Enc.c
	src/Bra.c
	src/Bra86.c
	src/BraIA64.c
	src/CpuArch.c
	src/Delta.c
	src/DllSecur.c
	src/LzFind.c
	src/LzFindMt.c
	src/Lzma2Dec.c
	src/Lzma2DecMt.c
	src/Lzma2Enc.c
	src/Lzma86Dec.c
	src/Lzma86Enc.c
	src/LzmaDec.c
	src/LzmaEnc.c
	src/LzmaLib.c
	src/MtCoder.c
	src/MtDec.c
	src/Ppmd7.c
	src/Ppmd7Dec.c
	src/Ppmd7Enc.c
	src/Sha256.c
	src/Sha256Opt.c
	src/Sort.c
	src/Threads.c
	src/Xz.c
	src/XzCrc64.c
	src/XzCrc64Opt.c
	src/XzDec.c
	src/XzEnc.c
	src/XzIn.c
 )
target_include_directories(${PROJECT_NAME} PUBLIC ".")
install(TARGETS ${PROJECT_NAME}   
		RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib)
install(FILES
    "${CMAKE_CURRENT_SOURCE_DIR}/src/7z.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/src/7zTypes.h"
    DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}")
	
if (LINUX)
    add_compile_options(-fPIC)
endif()
