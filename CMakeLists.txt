#
# project: fips-glslang
#
cmake_minimum_required(VERSION 3.21)

if (NOT FIPS_IMPORT)
# include the fips main cmake file
get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
include("${FIPS_ROOT_DIR}/cmake/fips.cmake")
    project(fips-glslang)
    fips_setup()
endif()


fips_begin_lib(glslang)
add_definitions(-DENABLE_HLSL)
add_definitions(-DENABLE_OPT=1)
fips_src(glslang/glslang/GenericCodeGen NO_RECURSE)
fips_src(glslang/glslang/MachineIndependent)
fips_src(glslang/glslang/HLSL)
fips_src(glslang/glslang/Public NO_RECURSE)
fips_include_directories(glslang/OGLCompilersDLL)
if (FIPS_WINDOWS)   
    fips_src(glslang/glslang/OSDependent/Windows NO_RECURSE)
elseif (FIPS_LINUX OR FIPS_MACOS)
    fips_src(glslang/glslang/OSDependent/Unix NO_RECURSE)
endif()

fips_src(glslang/hlsl NO_RECURSE)
fips_src(glslang/OGLCompilersDLL NO_RECURSE)
fips_src(glslang/SPIRV NO_RECURSE)
fips_src(glslang/StandAlone NO_RECURSE)

fips_src(spirv-tools/source NO_RECURSE)
#fips_src(spirv-tools/source/fuzz NO_RECURSE)
fips_src(spirv-tools/source/link NO_RECURSE)
fips_src(spirv-tools/source/opt NO_RECURSE)
fips_src(spirv-tools/source/reduce NO_RECURSE)
fips_src(spirv-tools/source/util NO_RECURSE)
fips_src(spirv-tools/source/val NO_RECURSE)
target_include_directories(glslang PRIVATE spirv-tools/include)
target_include_directories(glslang PRIVATE spirv-tools/source)
target_include_directories(glslang PRIVATE spirv-tools/)
target_include_directories(glslang PRIVATE spirv-tools/external/spirv-headers/include)
target_include_directories(glslang PRIVATE spirv-headers/include)

#target_include_directories(glslang PRIVATE spirv-tools/external/protobuf/src)
fips_end_lib()
target_include_directories(glslang PUBLIC spirv-tools/include)
