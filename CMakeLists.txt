cmake_minimum_required(VERSION 3.9.2)

project(libusb)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
include(EnableWarnings)

# currently this cmake file is windows specific

set(LIBUSB_SRCS
  libusb/core.c
  libusb/descriptor.c
  libusb/hotplug.c
  libusb/io.c
  libusb/strerror.c
  libusb/sync.c
  libusb/os/poll_windows.c
  libusb/os/windows_nt_common.c
  libusb/os/threads_windows.c
  libusb/os/windows_usbdk.c
  libusb/os/windows_winusb.c
)

set(LIBUSB_HDRS
  msvc/config.h
  libusb/libusb.h
  libusb/libusbi.h
  libusb/version.h
  libusb/version_nano.h
  libusb/os/windows_common.h
  libusb/os/windows_nt_common.h
  libusb/os/windows_nt_shared_types.h
  libusb/os/threads_windows.h
  libusb/os/windows_common.h
  libusb/os/windows_usbdk.h
  libusb/os/windows_winusb.h
)

add_library( libusb_static ${LIBUSB_SRCS}  ${LIBUSB_HDRS} )
target_include_directories( libusb_static  PUBLIC libusb )
target_include_directories( libusb_static  PRIVATE msvc )

set_property(TARGET libusb_static PROPERTY CXX_STANDARD 14)
set_property(TARGET libusb_static PROPERTY CXX_STANDARD_REQUIRED ON)

# enable warnings
enable_warnings(libusb_static)

target_compile_options(libusb_static PRIVATE /W4389)
