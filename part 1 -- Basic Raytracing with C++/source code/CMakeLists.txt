set(TARGET_NAME "BasicRayTracing")

# target
aux_source_directory("./lib" CPP_FILES)
add_executable(${TARGET_NAME} main.cpp ${CPP_FILES})

# link
target_link_libraries(${TARGET_NAME} PRIVATE GLUT::GLUT)
target_link_libraries(${TARGET_NAME} PRIVATE GLEW::GLEW)
target_link_libraries(${TARGET_NAME} PRIVATE glm::glm-header-only)

if(OpenMP_CXX_FOUND)
	target_link_libraries(${TARGET_NAME} PUBLIC OpenMP::OpenMP_CXX)
endif()
