idf_build_get_property(target IDF_TARGET)
if(NOT "${target}" STREQUAL "esp32s2")
    return()
endif()

if(NOT BOOTLOADER_BUILD)
    # [refactor-todo] propagate these requirements for compatibility
    # remove in the future
    set(legacy_reqs driver efuse soc)
endif()

idf_component_register(REQUIRES xtensa "${legacy_reqs}"
                       REQUIRED_IDF_TARGETS esp32s2)

target_linker_script(${COMPONENT_LIB} INTERFACE "ld/esp32s2.peripherals.ld")
