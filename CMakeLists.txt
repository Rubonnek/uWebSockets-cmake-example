cmake_minimum_required (VERSION 3.5.1)

# Set application properties
set(SINGLE_THREAD_ECHO_NAME single_thread_echo_server)

# Add other flags to current project only
set(CMAKE_C_FLAGS_DEBUG "${CXX_COMPILATION_FLAGS} -g -Wall")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} ${CXX_COMPILATION_FLAGS} -ldl")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${CXX_COMPILATION_FLAGS} -std=gnu99 -Wall")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${CXX_COMPILATION_FLAGS} -ldl -std=c++11 -Wno-deprecated-declarations -Wno-reorder")

# Choose the sources
set(SINGLE_THREAD_ECHO_SOURCES
	src/echo.cpp
	)

set(SINGLE_THREAD_ECHO_HEADERS
	)

# Build single threaded program the program
add_executable(${SINGLE_THREAD_ECHO_NAME} ${SINGLE_THREAD_ECHO_SOURCES} ${SINGLE_THREAD_ECHO_HEADERS})

# Set the shared libraries we already got compiled in the system:
set(SINGLE_THREAD_ECHO_SHARED_LIBRARIES
	ssl
	crypto
	uv
	uWS
	z
	)

# Link the program with the needed libraries
target_link_libraries(${SINGLE_THREAD_ECHO_NAME} ${SINGLE_THREAD_ECHO_SHARED_LIBRARIES})

# Set the variables for building the client:
set(MULTITHREADED_ECHO_NAME multi_thread_echo_server)
set(MULTITHREADED_ECHO_SOURCES
	src/multithreaded_echo.cpp
	)
set(MULTITHREADED_ECHO_HEADERS
	)

# Build the program
add_executable(${MULTITHREADED_ECHO_NAME} ${MULTITHREADED_ECHO_SOURCES} ${MULTITHREADED_ECHO_HEADERS}) # Sets the executable name

# Set the shared libraries we already got compiled in the system:
set(MULTITHREADED_ECHO_SHARED_LIBRARIES
	ssl
	crypto
	uv
	uWS
	pthread
	z
	)

# Link it with the necessary libraires:
target_link_libraries(${MULTITHREADED_ECHO_NAME} ${MULTITHREADED_ECHO_SHARED_LIBRARIES})
