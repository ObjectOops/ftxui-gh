cmake_minimum_required (VERSION 3.11)

# --- Fetch FTXUI --------------------------------------------------------------
include(FetchContent)

set(FETCHCONTENT_UPDATES_DISCONNECTED TRUE)
FetchContent_Declare(ftxui
  GIT_REPOSITORY https://github.com/ArthurSonzogni/ftxui
  GIT_TAG v3.0.0
  # GIT_TAG dfdbe1eecf0451e0da5420c4b9c39ecb415681ac
)

FetchContent_GetProperties(ftxui)
if(NOT ftxui_POPULATED)
  FetchContent_Populate(ftxui)
  add_subdirectory(${ftxui_SOURCE_DIR} ${ftxui_BINARY_DIR} EXCLUDE_FROM_ALL)
endif()

# ------------------------------------------------------------------------------

project(static
  LANGUAGES CXX
  VERSION 1.0.0
)

add_executable(static src/main.cpp)
target_include_directories(static PRIVATE src)

target_link_libraries(static
  PRIVATE ftxui::screen
  PRIVATE ftxui::dom
  PRIVATE ftxui::component # Not needed for this example.
)

if (EMSCRIPTEN) 

  string(APPEND CMAKE_CXX_FLAGS " -Wall -std=c++17") 
  # -O3 flag has to be specified in linking.

  string(APPEND CMAKE_CXX_FLAGS " -s USE_PTHREADS") 
  string(APPEND CMAKE_EXE_LINKER_FLAGS " -s ASYNCIFY") 
  string(APPEND CMAKE_EXE_LINKER_FLAGS " -s PROXY_TO_PTHREAD") 

  foreach(file "index.html" "sw.js")
    configure_file("src/${file}" ${file})
  endforeach(file)
endif() 
