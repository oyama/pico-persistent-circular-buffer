cmake_minimum_required(VERSION 3.13...3.27)

if(NOT PICO_SDK_PATH)
  set(PICO_SDK_PATH ${CMAKE_CURRENT_LIST_DIR}/lib/pico-sdk)
endif()
include(${PICO_SDK_PATH}/external/pico_sdk_import.cmake)

project(circularbuffer C CXX ASM)

set(PICO_BOARD pico_w)
set(FAMILY rp2040)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

pico_sdk_init()

add_executable(circularbuffer
  main.c
  circular_buffer.c
  flash_onboard.c
)
target_link_libraries(circularbuffer
  hardware_adc
  hardware_flash
  hardware_rtc
  hardware_sync
  pico_stdlib
)

target_include_directories(circularbuffer
  PRIVATE
  ${CMAKE_CURRENT_LIST_DIR}/include
)

pico_enable_stdio_usb(circularbuffer 1)
pico_add_extra_outputs(circularbuffer)