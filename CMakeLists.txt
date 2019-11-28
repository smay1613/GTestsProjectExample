cmake_minimum_required(VERSION 3.0)

project(HomeworkProject VERSION 1.0.0)

set(sources
    "src/impl.cpp"
)

set(headers
    "src/impl.h")

set(BUILD_DIR ${CMAKE_CURRENT_SOURCE_DIR}/build)
set(TEST true)

add_library(HomeworkProject SHARED ${sources})

set_target_properties(HomeworkProject PROPERTIES
                        C_STANDARD 11
                        CXX_STANDARD 11
                        PUBLIC_HEADER "${headers}"
)

target_compile_options(HomeworkProject PRIVATE -Wall -Wextra)

target_include_directories(HomeworkProject
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/src
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
)

# Introduce variables:
# * CMAKE_INSTALL_LIBDIR
# * CMAKE_INSTALL_BINDIR
# * CMAKE_INSTALL_INCLUDEDIR
include(GNUInstallDirs)

set(CMAKE_INSTALL_LIBDIR ${BUILD_DIR}/install)
set(CMAKE_INSTALL_BINDIR ${BUILD_DIR}/bin)
set(CMAKE_INSTALL_LIBDIR ${BUILD_DIR}/lib)


install(
    TARGETS HomeworkProject
    EXPORT "${TARGETS_EXPORT_NAME}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    PUBLIC_HEADER DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

if (TEST)
    message("TESTING ENABLED")
    add_subdirectory(tests)
endif()
