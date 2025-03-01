# Установка минимальной требуемой версии CMake.
cmake_minimum_required(VERSION 3.27.9 FATAL_ERROR)

# Название проекта.
project(ProjectEngine)



# Создание исполняемого файла проекта.
add_executable(${PROJECT_NAME} src/main.cpp)

# Указание стандарта C++17 для компиляции.
target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_17)

# Установка проекта как основного для Visual Studio.
set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${PROJECT_NAME})

# Установка директории вывода исполняемых файлов.
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)



# Установка параметров для библиотек.
set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(GLFW_INSTALL OFF CACHE BOOL "" FORCE)

# Добавление поддиректорий с библиотеками.
add_subdirectory(lib/glfw)
add_subdirectory(lib/glad)
add_subdirectory(lib/glm)

# Связывание библиотек с проектом.
target_link_libraries(${PROJECT_NAME} glad glfw)

# Подключение заголовочных файлов GLFW.
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_SOURCE_DIR}/lib/glfw/include)

# Подключение заголовочных файлов GLAD.
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_SOURCE_DIR}/lib/glad/include)

# Подключение заголовочных файлов GLM.
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_SOURCE_DIR}/lib/glm)
