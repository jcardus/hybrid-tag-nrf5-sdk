cmake_minimum_required(VERSION 3.20)

set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_SYSTEM_PROCESSOR arm)

# Toolchain
set(CMAKE_C_COMPILER arm-none-eabi-gcc)
set(CMAKE_CXX_COMPILER arm-none-eabi-g++)
set(CMAKE_ASM_COMPILER arm-none-eabi-gcc)
set(CMAKE_OBJCOPY arm-none-eabi-objcopy)
set(CMAKE_SIZE arm-none-eabi-size)

set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

project(ble_app_beacon_pca10040_s132 C ASM)

set(SDK_ROOT ${CMAKE_CURRENT_SOURCE_DIR}/../../../../../..)
set(PROJ_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../..)

# Source files
set(SRC_FILES
    ${SDK_ROOT}/components/libraries/log/src/nrf_log_backend_serial.c
    ${SDK_ROOT}/components/libraries/log/src/nrf_log_frontend.c
    ${SDK_ROOT}/components/libraries/button/app_button.c
    ${SDK_ROOT}/components/libraries/util/app_error.c
    ${SDK_ROOT}/components/libraries/util/app_error_weak.c
    ${SDK_ROOT}/components/libraries/timer/app_timer.c
    ${SDK_ROOT}/components/libraries/util/app_util_platform.c
    ${SDK_ROOT}/components/libraries/hardfault/hardfault_implementation.c
    ${SDK_ROOT}/components/libraries/util/nrf_assert.c
    ${SDK_ROOT}/components/libraries/util/sdk_errors.c
    ${SDK_ROOT}/components/boards/boards.c
    ${SDK_ROOT}/components/drivers_nrf/clock/nrf_drv_clock.c
    ${SDK_ROOT}/components/drivers_nrf/common/nrf_drv_common.c
    ${SDK_ROOT}/components/drivers_nrf/gpiote/nrf_drv_gpiote.c
    ${SDK_ROOT}/components/drivers_nrf/uart/nrf_drv_uart.c
    ${SDK_ROOT}/components/libraries/bsp/bsp.c
    ${SDK_ROOT}/components/libraries/bsp/bsp_nfc.c
    ${PROJ_DIR}/main.c
    ${SDK_ROOT}/external/segger_rtt/RTT_Syscalls_GCC.c
    ${SDK_ROOT}/external/segger_rtt/SEGGER_RTT.c
    ${SDK_ROOT}/external/segger_rtt/SEGGER_RTT_printf.c
    ${SDK_ROOT}/components/ble/common/ble_advdata.c
    ${SDK_ROOT}/components/ble/common/ble_conn_params.c
    ${SDK_ROOT}/components/ble/common/ble_srv_common.c
    ${SDK_ROOT}/components/toolchain/gcc/gcc_startup_nrf52.S
    ${SDK_ROOT}/components/toolchain/system_nrf52.c
    ${SDK_ROOT}/components/softdevice/common/softdevice_handler/softdevice_handler.c
)

# Include directories
set(INC_FOLDERS
    ${SDK_ROOT}/components/drivers_nrf/comp
    ${SDK_ROOT}/components/drivers_nrf/twi_master
    ${SDK_ROOT}/components/ble/ble_services/ble_ancs_c
    ${SDK_ROOT}/components/ble/ble_services/ble_ias_c
    ${SDK_ROOT}/components/libraries/pwm
    ${SDK_ROOT}/components/softdevice/s132/headers/nrf52
    ${SDK_ROOT}/components/libraries/usbd/class/cdc/acm
    ${SDK_ROOT}/components/libraries/usbd/class/hid/generic
    ${SDK_ROOT}/components/libraries/usbd/class/msc
    ${SDK_ROOT}/components/libraries/usbd/class/hid
    ${SDK_ROOT}/components/libraries/log
    ${SDK_ROOT}/components/ble/ble_services/ble_gls
    ${SDK_ROOT}/components/libraries/fstorage
    ${SDK_ROOT}/components/drivers_nrf/i2s
    ${SDK_ROOT}/components/libraries/gpiote
    ${SDK_ROOT}/components/drivers_nrf/gpiote
    ${SDK_ROOT}/components/boards
    ${SDK_ROOT}/components/drivers_nrf/common
    ${SDK_ROOT}/components/ble/ble_advertising
    ${SDK_ROOT}/components/drivers_nrf/adc
    ${SDK_ROOT}/components/ble/ble_services/ble_bas_c
    ${SDK_ROOT}/components/ble/ble_services/ble_hrs_c
    ${SDK_ROOT}/components/libraries/queue
    ${SDK_ROOT}/components/ble/ble_dtm
    ${SDK_ROOT}/components/toolchain/cmsis/include
    ${SDK_ROOT}/components/ble/ble_services/ble_rscs_c
    ${SDK_ROOT}/components/drivers_nrf/uart
    ${SDK_ROOT}/components/ble/common
    ${SDK_ROOT}/components/ble/ble_services/ble_lls
    ${SDK_ROOT}/components/drivers_nrf/wdt
    ${SDK_ROOT}/components/libraries/bsp
    ${SDK_ROOT}/components/ble/ble_services/ble_bas
    ${SDK_ROOT}/components/libraries/experimental_section_vars
    ${SDK_ROOT}/components/softdevice/s132/headers
    ${SDK_ROOT}/components/ble/ble_services/ble_ans_c
    ${SDK_ROOT}/components/libraries/slip
    ${SDK_ROOT}/components/libraries/mem_manager
    ${SDK_ROOT}/external/segger_rtt
    ${SDK_ROOT}/components/libraries/csense_drv
    ${SDK_ROOT}/components/drivers_nrf/hal
    ${SDK_ROOT}/components/ble/ble_services/ble_nus_c
    ${SDK_ROOT}/components/drivers_nrf/rtc
    ${SDK_ROOT}/components/ble/ble_services/ble_ias
    ${SDK_ROOT}/components/libraries/usbd/class/hid/mouse
    ${SDK_ROOT}/components/drivers_nrf/ppi
    ${SDK_ROOT}/components/ble/ble_services/ble_dfu
    ${SDK_ROOT}/components/drivers_nrf/twis_slave
    ${SDK_ROOT}/components
    ${SDK_ROOT}/components/libraries/scheduler
    ${SDK_ROOT}/components/ble/ble_services/ble_lbs
    ${SDK_ROOT}/components/ble/ble_services/ble_hts
    ${SDK_ROOT}/components/drivers_nrf/delay
    ${SDK_ROOT}/components/libraries/crc16
    ${SDK_ROOT}/components/drivers_nrf/timer
    ${SDK_ROOT}/components/libraries/util
    ${SDK_ROOT}/components/drivers_nrf/pwm
    ${CMAKE_CURRENT_SOURCE_DIR}/../config
    ${SDK_ROOT}/components/libraries/usbd/class/cdc
    ${SDK_ROOT}/components/libraries/csense
    ${SDK_ROOT}/components/drivers_nrf/rng
    ${SDK_ROOT}/components/libraries/low_power_pwm
    ${SDK_ROOT}/components/libraries/hardfault
    ${SDK_ROOT}/components/ble/ble_services/ble_cscs
    ${SDK_ROOT}/components/libraries/uart
    ${SDK_ROOT}/components/libraries/hci
    ${SDK_ROOT}/components/libraries/usbd/class/hid/kbd
    ${SDK_ROOT}/components/drivers_nrf/spi_slave
    ${SDK_ROOT}/components/drivers_nrf/lpcomp
    ${SDK_ROOT}/components/libraries/timer
    ${SDK_ROOT}/components/drivers_nrf/power
    ${SDK_ROOT}/components/libraries/usbd/config
    ${SDK_ROOT}/components/toolchain
    ${SDK_ROOT}/components/libraries/led_softblink
    ${SDK_ROOT}/components/drivers_nrf/qdec
    ${SDK_ROOT}/components/ble/ble_services/ble_cts_c
    ${SDK_ROOT}/components/drivers_nrf/spi_master
    ${SDK_ROOT}/components/ble/ble_services/ble_nus
    ${SDK_ROOT}/components/ble/ble_services/ble_hids
    ${SDK_ROOT}/components/drivers_nrf/pdm
    ${SDK_ROOT}/components/libraries/crc32
    ${SDK_ROOT}/components/libraries/usbd/class/audio
    ${SDK_ROOT}/components/ble/peer_manager
    ${SDK_ROOT}/components/drivers_nrf/swi
    ${SDK_ROOT}/components/ble/ble_services/ble_tps
    ${SDK_ROOT}/components/ble/ble_services/ble_dis
    ${SDK_ROOT}/components/device
    ${SDK_ROOT}/components/ble/nrf_ble_qwr
    ${SDK_ROOT}/components/libraries/button
    ${SDK_ROOT}/components/libraries/usbd
    ${SDK_ROOT}/components/drivers_nrf/saadc
    ${SDK_ROOT}/components/ble/ble_services/ble_lbs_c
    ${SDK_ROOT}/components/ble/ble_racp
    ${SDK_ROOT}/components/toolchain/gcc
    ${SDK_ROOT}/components/libraries/fds
    ${SDK_ROOT}/components/libraries/twi
    ${SDK_ROOT}/components/drivers_nrf/clock
    ${SDK_ROOT}/components/ble/ble_services/ble_rscs
    ${SDK_ROOT}/components/drivers_nrf/usbd
    ${SDK_ROOT}/components/softdevice/common/softdevice_handler
    ${SDK_ROOT}/components/ble/ble_services/ble_hrs
    ${SDK_ROOT}/components/libraries/log/src
)

# Compiler definitions
add_definitions(
    -DNRF52
    -DNRF52_PAN_64
    -DSOFTDEVICE_PRESENT
    -DBOARD_PCA10040
    -DNRF52832
    -DNRF52_PAN_12
    -DNRF52_PAN_58
    -DNRF52_PAN_54
    -DNRF52_PAN_31
    -DNRF52_PAN_51
    -DNRF52_PAN_36
    -DCONFIG_GPIO_AS_PINRESET
    -DBLE_STACK_SUPPORT_REQD
    -DNRF52_PAN_15
    -DNRF_SD_BLE_API_VERSION=3
    -DSWI_DISABLE0
    -DNRF52_PAN_20
    -DNRF52_PAN_55
    -DS132
)

# Compiler flags
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -mcpu=cortex-m4 -mthumb -mabi=aapcs -mfloat-abi=hard -mfpu=fpv4-sp-d16")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -O3 -g3")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -ffunction-sections -fdata-sections -fno-strict-aliasing")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fno-builtin --short-enums")

set(CMAKE_ASM_FLAGS "${CMAKE_ASM_FLAGS} -mcpu=cortex-m4 -mthumb -mabi=aapcs -mfloat-abi=hard -mfpu=fpv4-sp-d16")
set(CMAKE_ASM_FLAGS "${CMAKE_ASM_FLAGS} -x assembler-with-cpp")

set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -mcpu=cortex-m4 -mthumb -mabi=aapcs -mfloat-abi=hard -mfpu=fpv4-sp-d16")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -T${CMAKE_CURRENT_SOURCE_DIR}/ble_app_beacon_gcc_nrf52.ld")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,--gc-sections --specs=nano.specs -lc -lnosys")

# Create executable
add_executable(${PROJECT_NAME}.elf ${SRC_FILES})
target_include_directories(${PROJECT_NAME}.elf PRIVATE ${INC_FOLDERS})

# Create hex file
add_custom_command(TARGET ${PROJECT_NAME}.elf POST_BUILD
    COMMAND ${CMAKE_OBJCOPY} -O ihex ${PROJECT_NAME}.elf ${PROJECT_NAME}.hex
    COMMENT "Creating HEX file"
)

# Flash targets
add_custom_target(flash
    COMMAND openocd -f interface/stlink.cfg -f target/nrf52.cfg -c "program ${PROJECT_NAME}.hex verify reset exit"
    DEPENDS ${PROJECT_NAME}.elf
    COMMENT "Flashing application"
)

add_custom_target(flash_softdevice
    COMMAND openocd -f interface/stlink.cfg -f target/nrf52.cfg -c "program ${SDK_ROOT}/components/softdevice/s132/hex/s132_nrf52_3.0.0_softdevice.hex verify reset exit"
    COMMENT "Flashing softdevice"
)

add_custom_target(erase
    COMMAND openocd -f interface/stlink.cfg -f target/nrf52.cfg -c "init; reset halt; nrf5 mass_erase; exit"
    COMMENT "Erasing chip"
)
