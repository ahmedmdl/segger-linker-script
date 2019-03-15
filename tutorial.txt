we shall name our project in the project explorer PR to differentiate it from the project tab option inside segger
so navigate to 
PR->internal files 
right click and select "exclude from build" on both 
 cortex_m_startup.s
 segger_thumb_startup.s

right click on PR
select options
search for:
1."memory map macros" then copy and replace if u have something else: 
FLASH_START=0x1F000
SRAM_START=0x20002000

2."memory segments" then copy and replace if u have something else:
FLASH RX 0x00000000 0x00040000
SRAM RWX 0x20000000 0x00004000

 
3. target device then choose "nRF51822__xxAA"

4- section placement file then choose "flash_placement.xml"

5- "section placement macros" then write:
FLASH_START=0x1F000
SRAM_START=0x20002000

6- user include directories then replace what u have with this:
./../../../config/ble_app_uart_c_pca10028_s130
./../../../config
./../../../../../../components
./../../../../../../components/ble/ble_advertising
./../../../../../../components/ble/ble_db_discovery
./../../../../../../components/ble/ble_dtm
./../../../../../../components/ble/ble_racp
./../../../../../../components/ble/ble_services/ble_ancs_c
./../../../../../../components/ble/ble_services/ble_ans_c
./../../../../../../components/ble/ble_services/ble_bas
./../../../../../../components/ble/ble_services/ble_bas_c
./../../../../../../components/ble/ble_services/ble_cscs
./../../../../../../components/ble/ble_services/ble_cts_c
./../../../../../../components/ble/ble_services/ble_dfu
./../../../../../../components/ble/ble_services/ble_dis
./../../../../../../components/ble/ble_services/ble_gls
./../../../../../../components/ble/ble_services/ble_hids
./../../../../../../components/ble/ble_services/ble_hrs
./../../../../../../components/ble/ble_services/ble_hrs_c
./../../../../../../components/ble/ble_services/ble_hts
./../../../../../../components/ble/ble_services/ble_ias
./../../../../../../components/ble/ble_services/ble_ias_c
./../../../../../../components/ble/ble_services/ble_lbs
./../../../../../../components/ble/ble_services/ble_lbs_c
./../../../../../../components/ble/ble_services/ble_lls
./../../../../../../components/ble/ble_services/ble_nus
./../../../../../../components/ble/ble_services/ble_nus_c
./../../../../../../components/ble/ble_services/ble_rscs
./../../../../../../components/ble/ble_services/ble_rscs_c
./../../../../../../components/ble/ble_services/ble_tps
./../../../../../../components/ble/common
./../../../../../../components/ble/nrf_ble_qwr
./../../../../../../components/ble/peer_manager
./../../../../../../components/boards
./../../../../../../components/device
./../../../../../../components/drivers_nrf/adc
./../../../../../../components/drivers_nrf/clock
./../../../../../../components/drivers_nrf/common
./../../../../../../components/drivers_nrf/comp
./../../../../../../components/drivers_nrf/delay
./../../../../../../components/drivers_nrf/gpiote
./../../../../../../components/drivers_nrf/hal
./../../../../../../components/drivers_nrf/i2s
./../../../../../../components/drivers_nrf/lpcomp
./../../../../../../components/drivers_nrf/pdm
./../../../../../../components/drivers_nrf/power
./../../../../../../components/drivers_nrf/ppi
./../../../../../../components/drivers_nrf/pwm
./../../../../../../components/drivers_nrf/qdec
./../../../../../../components/drivers_nrf/rng
./../../../../../../components/drivers_nrf/rtc
./../../../../../../components/drivers_nrf/saadc
./../../../../../../components/drivers_nrf/spi_master
./../../../../../../components/drivers_nrf/spi_slave
./../../../../../../components/drivers_nrf/swi
./../../../../../../components/drivers_nrf/timer
./../../../../../../components/drivers_nrf/twi_master
./../../../../../../components/drivers_nrf/twis_slave
./../../../../../../components/drivers_nrf/uart
./../../../../../../components/drivers_nrf/usbd
./../../../../../../components/drivers_nrf/wdt
./../../../../../../components/libraries/bsp
./../../../../../../components/libraries/button
./../../../../../../components/libraries/crc16
./../../../../../../components/libraries/crc32
./../../../../../../components/libraries/csense
./../../../../../../components/libraries/csense_drv
./../../../../../../components/libraries/experimental_section_vars
./../../../../../../components/libraries/fds
./../../../../../../components/libraries/fifo
./../../../../../../components/libraries/fstorage
./../../../../../../components/libraries/gpiote
./../../../../../../components/libraries/hardfault
./../../../../../../components/libraries/hci
./../../../../../../components/libraries/led_softblink
./../../../../../../components/libraries/log
./../../../../../../components/libraries/log/src
./../../../../../../components/libraries/low_power_pwm
./../../../../../../components/libraries/mem_manager
./../../../../../../components/libraries/pwm
./../../../../../../components/libraries/queue
./../../../../../../components/libraries/scheduler
./../../../../../../components/libraries/slip
./../../../../../../components/libraries/timer
./../../../../../../components/libraries/twi
./../../../../../../components/libraries/uart
./../../../../../../components/libraries/usbd
./../../../../../../components/libraries/usbd/class/audio
./../../../../../../components/libraries/usbd/class/cdc
./../../../../../../components/libraries/usbd/class/cdc/acm
./../../../../../../components/libraries/usbd/class/hid
./../../../../../../components/libraries/usbd/class/hid/generic
./../../../../../../components/libraries/usbd/class/hid/kbd
./../../../../../../components/libraries/usbd/class/hid/mouse
./../../../../../../components/libraries/usbd/class/msc
./../../../../../../components/libraries/usbd/config
./../../../../../../components/libraries/util
./../../../../../../components/softdevice/common/softdevice_handler
./../../../../../../components/softdevice/s130/headers
./../../../../../../components/softdevice/s130/headers/nrf51
./../../../../../../components/toolchain
./../../../../../../components/toolchain/cmsis/include
./../../../../../../external/segger_rtt
./../config

7- "linker" then select GNU

right click on PR and select add existing file then add 
thumb_crt0.s
flash_placement.xml
click yes on the warning

under PR->nRF_libraries in ur project u will find "retarget.c"
remove it then right click on nRF_libraries and select "add existing file" and add my "retarget.c" 

then rebuild and all should work
