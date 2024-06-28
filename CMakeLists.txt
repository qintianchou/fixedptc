cmake_minimum_required(VERSION 3.5)

project(fixedptc LANGUAGES C)

if (NOT "${CMAKE_C_COMPILER_ID}" STREQUAL "Clang" AND NOT "${CMAKE_C_COMPILER_ID}" STREQUAL "GNU")
    message(FATAL_ERROR "Only Clang and GCC are supported")
endif()

add_executable(test test.c)

add_executable(verify32 verify.c)
set_target_properties(verify32 PROPERTIES COMPILE_FLAGS -DFIXEDPT_BITS=32)
if ("${CMAKE_SYSTEM_NAME}" MATCHES "Linux")
    target_link_libraries(verify32 "m")
endif()

add_executable(verify64 verify.c)
set_target_properties(verify64 PROPERTIES COMPILE_FLAGS -DFIXEDPT_BITS=64)
if ("${CMAKE_SYSTEM_NAME}" MATCHES "Linux")
    target_link_libraries(verify64 "m")
elseif("${CMAKE_SYSTEM_NAME}" MATCHES "Windows")
    get_filename_component(BIN_DIR "${CMAKE_C_COMPILER}" DIRECTORY)
    set(BUILDIN_LIB_PATH ${BIN_DIR}/../lib/clang/17/lib/windows/clang_rt.builtins-x86_64.lib)
    target_link_libraries(verify64 ${BUILDIN_LIB_PATH})
endif()
