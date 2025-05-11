add_executable(AHCM
    src/AHCM.cpp
    include/AHCM.h
)

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET AHCM PROPERTY CXX_STANDARD 20)
endif()

# Crow
set(CROW_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/third_party/Crow-master/include")
include_directories(${CROW_INCLUDE_DIR})

# Asio
set(ASIO_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/third_party/asio-1.30.2/include")
include_directories(${ASIO_INCLUDE_DIR})

