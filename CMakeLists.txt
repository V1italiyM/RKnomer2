cmake_minimum_required(VERSION 3.10)
project(House_and_Theme)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Добавляем исполняемый файл для примера
add_executable(example house_and_theme.cpp)

# GoogleTest
include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/refs/tags/release-1.10.0.tar.gz
)
# Для Windows: Предотвращаем переопределение параметров компилятора/линкера родительского проекта
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

# Отключаем обработку предупреждений как ошибок для Google Test
target_compile_options(gtest PRIVATE -Wno-error=maybe-uninitialized)

# Отключаем обработку предупреждений о неинициализированных переменных как ошибок
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-error=maybe-uninitialized")

# Добавляем исполняемый файл для тестов
add_executable(tests tests.cpp)
target_link_libraries(tests gtest_main)

include(GoogleTest)
gtest_discover_tests(tests)
