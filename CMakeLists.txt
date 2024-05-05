cmake_minimum_required(VERSION 3.12)    

include(pico_sdk_import.cmake)          

project(core_temp_to_mqtt C CXX ASM)    

set(CMAKE_C_STANDARD 11)                
set(CMAKE_CXX_STANDARD 17)              

set(PICO_BOARD pico_w)                  

pico_sdk_init()                         

add_executable(core_temp_to_mqtt main.c)

pico_enable_stdio_usb(core_temp_to_mqtt 1)
pico_enable_stdio_uart(core_temp_to_mqtt 0)


target_include_directories(core_temp_to_mqtt PRIVATE
        ${CMAKE_CURRENT_LIST_DIR}       
)

target_link_libraries(core_temp_to_mqtt
        tinyusb_board
        pico_cyw43_arch_lwip_threadsafe_background
        pico_stdlib
        pico_lwip_mqtt
        hardware_adc
    )

pico_add_extra_outputs(core_temp_to_mqtt)
