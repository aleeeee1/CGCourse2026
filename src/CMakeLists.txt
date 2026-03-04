# si ok l'ha fatto deepseek
function(target_copy_shaders TARGET_NAME)
    set(SHADER_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/shaders")
    
    if(EXISTS "${SHADER_SOURCE_DIR}")
        message(STATUS "Copying shaders for ${TARGET_NAME} from ${SHADER_SOURCE_DIR}")
        
        add_custom_command(TARGET ${TARGET_NAME} POST_BUILD
            COMMAND ${CMAKE_COMMAND} -E copy_directory
                "${SHADER_SOURCE_DIR}"
                "$<TARGET_FILE_DIR:${TARGET_NAME}>/shaders"
            COMMENT "Copying shaders for ${TARGET_NAME}"
        )
    else()

        set(SHADER_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../shaders")
        if(EXISTS "${SHADER_SOURCE_DIR}")
            add_custom_command(TARGET ${TARGET_NAME} POST_BUILD
                COMMAND ${CMAKE_COMMAND} -E copy_directory
                    "${SHADER_SOURCE_DIR}"
                    "$<TARGET_FILE_DIR:${TARGET_NAME}>/shaders"
                COMMENT "Copying shaders for ${TARGET_NAME} from parent"
            )
        else()
            message(WARNING "No shaders folder found for ${TARGET_NAME}")
        endif()
    endif()
endfunction()



add_subdirectory(code_00_raytracer)
add_subdirectory(code_01_setup_glfw)
add_subdirectory(code_02_my_first_triangle)
add_subdirectory(code_03_wrapping_shaders_buffers)
add_subdirectory(code_04_robotic_arm_transformations)


