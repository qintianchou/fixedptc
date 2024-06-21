cmake_minimum_required(VERSION 3.5)

project(fixedptc VERSION 0.1.0 LANGUAGES C)

add_executable(test test.c)

add_executable(verify32 verify.c)
set(BUILD32_FLAGS "-DFIXEDPT_BITS=32")
set_target_properties(verify32 PROPERTIES COMPILE_FLAGS ${BUILD32_FLAGS})

# add_executable(verify64 verify.c)
# set(BUILD64_FLAGS "-DFIXEDPT_BITS=64")
# set_target_properties(verify64 PROPERTIES COMPILE_FLAGS ${BUILD64_FLAGS})
