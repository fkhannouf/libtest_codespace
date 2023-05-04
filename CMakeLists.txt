cmake_minimum_required(VERSION 3.16)
project(uuid_lib C)

set(CMAKE_C_STANDARD 11)

# Specify the include directories
include_directories(
        include
)

# Specify the optimization flags
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -O3")

# Specify the sources
add_executable(uuid.library
        uuid_files/init.c
        uuid_files/main/Obtain.c
        uuid_files/main/Release.c
        uuid_files/main/UuidA.c
        uuid_files/main/FreeUuid.c
        uuid_files/main/UuidToText.c
        uuid_files/main/uuid_v1.c
        uuid_files/main/uuid_v4.c
        uuid_files/main/uuid_v5.c
        uuid_files/main/uuid_preset.c
        uuid_files/main/uuid_string.c
        uuid_files/main/store.c
)

# Set the common compilation flags
# set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -Werror -Wno-pedantic -Wno-unused-parameter -Wno-unused-variable -Wno-unused-function -Wno-unused-but-set-variable -Wno-unused-but-set-parameter -Wno-unused-value -Wno-unused-result -Wno-unused-label -Wno-unused-local-typedefs -Wno-unused-const-variable -Wno-unused-macros -Wno-unused-local-typedefs -Wno-unused-const-variable -Wno-unused-macros -Wno-unused-local-typedefs -Wno-unused-const-variable -Wno-unused-macros -Wno-unused-local-typedefs -Wno-unused-const-variable -Wno-unused-macros -Wno-unused-local-typedefs -Wno-unused-const-variable -Wno-unused-macros -Wno-unused-local-typedefs -Wno-unused-const-variable -Wno-unused-macros -Wno-unused-local-typedefs -Wno-unused-const-variable -Wno-unused-macros -Wno-unused-local-typedefs -Wno-unused-const-variable -Wno-unused-macros -Wno-unused-local-typedefs -Wno-unused-const-variable -Wno-unused-macros -Wno-unused-local-typedefs -Wno-unused-const-variable -Wno-unused-macros -Wno-unused-local-typedefs -Wno-unused-const-variable -Wno-unused-macros")

# Specify the linker flags for the library target
set_target_properties(uuid.library
        PROPERTIES
        LINK_FLAGS "-nostartfiles"
)

# Copy the target to source directory
add_custom_command(TARGET uuid.library POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:uuid.library> ${CMAKE_SOURCE_DIR}
)

# Setup the test target
add_executable(uuid_test
        uuid.c
)

# Specify the libraries for the test target
target_link_libraries(uuid_test PUBLIC auto)

# Copy the target to source directory
add_custom_command(TARGET uuid_test POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:uuid_test> ${CMAKE_SOURCE_DIR}
)
