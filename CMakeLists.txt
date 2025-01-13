cmake_minimum_required (VERSION 3.7)

file(GLOB sources *.cpp *.h)
file(GLOB sources_sdl_player sdl_player/*.cpp sdl_player/*.h)
file(GLOB sources_sync_audio sdl_player/Sync_Audio.*)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-register")

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

project (Blip_Buffer)

find_package(SDL REQUIRED)

include_directories(. ./player ${SDL_INCLUDE_DIRS})

set(demos
  1.waveform
  2.square
  3.clock_rate
  4.continuous
  multiple_waves
  stereo
  treble_bass
  buffering
  external_mixing
  delta_synth
)

foreach(demo ${demos})
  add_executable(${demo} ${sources} ${sources_sdl_player} demo/${demo}.cpp)
  target_link_libraries(${demo} ${SDL_LIBRARIES})
endforeach()

set(other_demos
  sample_formats
  sdl_audio
)

foreach(demo ${other_demos})
  add_executable(${demo} ${sources} ${sources_sync_audio} demo/${demo}.cpp)
  target_link_libraries(${demo} ${SDL_LIBRARIES})
endforeach()
