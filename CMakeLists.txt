#
# project: fips-glslang
#
cmake_minimum_required(VERSION 2.8)

# include the fips main cmake file
get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
include("${FIPS_ROOT_DIR}/cmake/fips.cmake")

fips_setup()
fips_project(fips-glslang)

fips_begin_lib(glslang)
add_definitions(-DENABLE_HLSL)
add_definitions(-DENABLE_OPT=0)
fips_src(glslang/glslang/GenericCodeGen NO_RECURSE)
fips_src(glslang/glslang/MachineIndependent)
fips_src(glslang/glslang/Public NO_RECURSE)
fips_include_directories(../fips-glslang/glslang/OGLCompilersDLL)
if (FIPS_WINDOWS)
    fips_src(glslang/glslang/OSDependent/Windows NO_RECURSE)
elseif (FIPS_LINUX)
    fips_src(glslang/glslang/OSDependent/Unix NO_RECURSE)
endif()

fips_src(glslang/hlsl NO_RECURSE)
fips_src(glslang/OGLCompilersDLL NO_RECURSE)
fips_src(glslang/SPIRV NO_RECURSE)
fips_src(glslang/StandAlone NO_RECURSE)
fips_end_lib()
if(FIPS_WINDOWS AND ${CMAKE_VERSION} VERSION_GREATER_EQUAL "3.16.0")
    set_target_properties(glslang PROPERTIES UNITY_BUILD ON)
endif()

fips_finish()
