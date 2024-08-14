set(LIBURING_DIR ${CMAKE_CURRENT_SOURCE_DIR})

set(LIBURING_LIB_PATH ${LIBURING_DIR}/src/liburing.a)
if (NOT EXISTS ${LIBURING_LIB_PATH})
    message(STATUS "Building liburing")
    execute_process(
            COMMAND ./configure --cc=clang --cxx=clang++
            WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
            OUTPUT_QUIET
    )

    execute_process(
            COMMAND make
            WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
            OUTPUT_QUIET
    )
endif ()

add_library(liburing STATIC IMPORTED GLOBAL)
set_property(TARGET liburing PROPERTY
        IMPORTED_LOCATION ${LIBURING_LIB_PATH})
target_include_directories(liburing INTERFACE ${LIBURING_DIR}/src/include)