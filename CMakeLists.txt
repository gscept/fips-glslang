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
fips_include_directories(../fips-glslang/glslang)
fips_src(glslang/ NO_RECURSE)
fips_end_lib()

fips_finish()