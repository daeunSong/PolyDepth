cmake_minimum_required(VERSION 2.8.11)

SET(PROJECT_NAME PolyDepth)
project(${PROJECT_NAME})

set(VERSION_MAJOR 1)
set(VERSION ${VERSION_MAJOR})

set( HDRS
	${PROJECT_NAME}/include/PolyDepth.h
	${PROJECT_NAME}/include/MeshObject.h
	${PROJECT_NAME}/include/ClearConfiguration.h
        ${PROJECT_NAME}/include/stopwatch.h
)

set( SRCS
	${PROJECT_NAME}/src/PolyDepth.cpp
	${PROJECT_NAME}/src/MeshObject.cpp
        ${PROJECT_NAME}/src/stopwatch.cpp
)

set( DEMO_SRCS
	demo/src/main.cpp
	demo/src/model.cpp
	demo/src/stopwatch.cpp
)

add_subdirectory(C2A)
add_library(${PROJECT_NAME} STATIC ${HDRS} ${SRCS})
add_dependencies(${PROJECT_NAME} C2A)

target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_NAME}/include)
target_link_libraries(${PROJECT_NAME} C2A)


option(BUILD_SAMPLES "Build samples" ON)


find_package(OpenGL)
find_package(GLUT)

add_executable(demo ${DEMO_SRCS})
target_include_directories(demo PUBLIC demo/include ${OPENGL_INCLUDE_DIRS} ${GLUT_INCLUDE_DIR})
target_link_libraries(demo PolyDepth C2A PQP ${OPENGL_LIBRARIES} ${GLUT_LIBRARIES})


