project(Bug CXX)

if(CMAKE_CXX_COMPILER_VERSION)
    message(STATUS "Compiler version found!")
else()
    message(STATUS "Compiler version NOT found!")
endif()