if (NOT TARGET aziotsharedutil)
    option(use_http "" OFF)
    option(use_wsio "" OFF)
    option(use_cppunittest "" OFF)

    # By default, CMake turns on /W3 for all MSVC builds.
    # azure_c_shared_utility's CMakeLists.txt will then append /W4 to the
    # CMAKE_CXX_FLAGS and CMAKE_C_FLAGS this causes a warning from cl.exe. To
    # prevent this warning, we will remove /W3 from the CMAKE_CXX_FLAGS and
    # CMAKE_C_FLAGS before adding the azure_c_shared_utiltiy sub directory
    string(REGEX REPLACE " /W3" "" CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
    string(REGEX REPLACE " /W3" "" CMAKE_C_FLAGS "${CMAKE_C_FLAGS}")

    add_subdirectory(src EXCLUDE_FROM_ALL)

else()
    message(STATUS "aziotsharedutil is already a target. Skipping adding it twice")
endif()

add_library(azure::aziotsharedutil ALIAS aziotsharedutil)