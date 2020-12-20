cmake_minimum_required(VERSION 3.1)
project(bitsery_uring
        LANGUAGES CXX
        VERSION 0.1)

#========== find prerequisites ===================
find_package(Bitsery 5.2.0 REQUIRED)
# append CMAKE_MODULE_PATH so we could find IoUring package
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
find_package(IoUring 0.7 REQUIRED)

#============= setup target ======================
add_library(bitsery_uring INTERFACE)
# create alias, so that user could always write target_link_libraries(... Bitsery::bitsery)
# despite of bitsery target is imported or not
add_library(Bitsery::bitsery_uring ALIAS bitsery_uring)

include(GNUInstallDirs)
target_include_directories(bitsery_uring INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>)
target_compile_features(bitsery_uring INTERFACE
        cxx_auto_type) # todo append more features, as we go
target_link_libraries(bitsery_uring
        INTERFACE Bitsery::bitsery IoUring::IoUring)

#=============== setup installation =======================
include(CMakePackageConfigHelpers)
write_basic_package_version_file(${CMAKE_CURRENT_BINARY_DIR}/BitseryUringConfigVersion.cmake
        COMPATIBILITY SameMinorVersion)
install(TARGETS bitsery_uring
        EXPORT bitseryUringTargets
        INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
install(EXPORT bitseryUringTargets
        FILE "BitseryUringConfig.cmake"
        NAMESPACE Bitsery::
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/BitseryUring)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/BitseryUringConfigVersion.cmake
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/BitseryUring)
install(DIRECTORY include/bitsery_uring
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})


add_subdirectory(examples)

enable_testing()
add_subdirectory(tests)
