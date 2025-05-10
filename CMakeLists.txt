cmake_minimum_required(VERSION 3.31)
project(AudioPlugin)

set(CMAKE_CXX_STANDARD 20)

# JUCE'u sistemde bulamazsa FetchContent ile indir
include(FetchContent)

# JUCE'un daha önce eklenip eklenmediğini kontrol et
if(NOT EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/JUCE/CMakeLists.txt")
    message(STATUS "JUCE bulunamadı, FetchContent ile indiriliyor...")
    FetchContent_Declare(
        JUCE
        GIT_REPOSITORY https://github.com/juce-framework/JUCE.git
        GIT_TAG        master # veya belirli bir sürüm etiketi
    )
    FetchContent_MakeAvailable(JUCE)
else()
    add_subdirectory(JUCE)
endif()

add_executable(AudioPlugin main.cpp)

target_link_libraries(AudioPlugin PRIVATE
    juce::juce_core
    juce::juce_events
    juce::juce_audio_basics
    juce::juce_audio_devices
    juce::juce_audio_formats
    juce::juce_audio_processors
    juce::juce_audio_utils
    juce::juce_graphics
    juce::juce_gui_basics
)

