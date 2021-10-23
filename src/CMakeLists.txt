# CMAKE required version
cmake_minimum_required (VERSION 3.0)

if(APPLE)
    set(TARGET "OSX" CACHE STRING "target platform")
    set(ARCH "x86_64" CACHE STRING "target architecture")
endif()

set(LIBRARY_TYPE "STATIC" CACHE STRING "Library type")

if("${TARGET}" STREQUAL "IOS")
    set(IOS TRUE)
endif()													
if(UNIX AND NOT APPLE AND NOT IOS)
   set(LINUX TRUE)
endif()

# set the project name
project (lzma)						 

if(CMAKE_SIZEOF_VOID_P EQUAL 8)
    if (WIN32)
        set(WIN64 TRUE)
    endif()
endif()

set(CMAKE_C_STANDARD 11)
set (LIBRARY_TYPE "STATIC")

if(LINUX)
    set(CMAKE_C_FLAGS "-fPIC" CACHE STRING "" FORCE)
endif()

# add sources
add_library(${PROJECT_NAME} ${LIBRARY_TYPE}
    7zAlloc.c
	7zArcIn.c
	7zBuf.c
	7zBuf2.c
	7zCrc.c
	7zCrcOpt.c
	7zDec.c
	7zFile.c
	7zStream.c
	Aes.c
	AesOpt.c
	Alloc.c
	Bcj2.c
	Bcj2Enc.c
	Bra.c
	Bra86.c
	BraIA64.c
	CpuArch.c
	Delta.c
	DllSecur.c
	LzFind.c
	LzFindMt.c
	Lzma2Dec.c
	Lzma2DecMt.c
	Lzma2Enc.c
	Lzma86Dec.c
	Lzma86Enc.c
	LzmaDec.c
	LzmaEnc.c
	LzmaLib.c
	MtCoder.c
	MtDec.c
	Ppmd7.c
	Ppmd7Dec.c
	Ppmd7Enc.c
	Sha256.c
	Sha256Opt.c
	Sort.c
	Threads.c
	Xz.c
	XzCrc64.c
	XzCrc64Opt.c
	XzDec.c
	XzEnc.c
	XzIn.c
 )

if (CMAKE_BUILD_TYPE MATCHES Debug)
    target_compile_definitions(${PROJECT_NAME} PUBLIC
        DEBUG
    )
else()
    target_compile_definitions(${PROJECT_NAME} PUBLIC
        NDEBUG
    )
endif()

if (LINUX)
    add_compile_options(-fPIC)
endif()
