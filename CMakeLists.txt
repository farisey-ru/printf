cmake_minimum_required (VERSION 3.9)
project(printf C)

option(FLOAT "Support float (%f)" ON)
if   (NOT FLOAT)
	add_definitions(-DPRINTF_DISABLE_SUPPORT_FLOAT)
endif(NOT FLOAT)

option(EXPONENTIAL "Support exponential (%e/%g)" ON)
if   (NOT EXPONENTIAL)
	add_definitions(-DPRINTF_DISABLE_SUPPORT_EXPONENTIAL)
endif(NOT EXPONENTIAL)

option(LONG_LONG "Support long long (%llu or %p)" ON)
if   (NOT LONG_LONG)
	add_definitions(-DPRINTF_DISABLE_SUPPORT_LONG_LONG)
endif(NOT LONG_LONG)

option(PTRDIFF "Support ptrdiff (%t)" ON)
if   (NOT PTRDIFF)
	add_definitions(-DPRINTF_DISABLE_SUPPORT_PTRDIFF_T)
endif(NOT PTRDIFF)

option(PTR_MAC "Support MAC-address (%pM)" OFF)
if   (PTR_MAC)
	add_definitions(-DPRINTF_ENABLE_SUPPORT_MAC)
endif(PTR_MAC)

option(PTR_IP4 "Support IPv4-address (%pI4)" OFF)
if   (PTR_IP4)
	add_definitions(-DPRINTF_ENABLE_SUPPORT_IP4)
endif(PTR_IP4)

option(PTR_IP6 "Support IPv6-address (%pI6)" OFF)
if   (PTR_IP6)
	add_definitions(-DPRINTF_ENABLE_SUPPORT_IP6)
endif(PTR_IP6)

# numeric defines

option(NTOA_BUFSIZ "ntoa conversion buffer size" OFF)
if   (NTOA_BUFSIZ)
	add_definitions(-DPRINTF_NTOA_BUFFER_SIZE=${NTOA_BUFSIZ})
endif(NTOA_BUFSIZ)

# below mean if FLOAT is ON.
option(FTOA_BUFSIZ "ftoa conversion buffer size" OFF)
if   (FTOA_BUFSIZ)
	add_definitions(-DPRINTF_FTOA_BUFFER_SIZE=${FTOA_BUFSIZ})
endif(FTOA_BUFSIZ)

option(DEF_FLOAT_PREC "default float precision" OFF)
if   (DEF_FLOAT_PREC)
	add_definitions(-DPRINTF_DEFAULT_FLOAT_PRECISION=${DEF_FLOAT_PREC})
endif(DEF_FLOAT_PREC)

option(MAX_FLOAT "largest float suitable to print with %f" OFF)
if   (MAX_FLOAT)
	add_definitions(-DPRINTF_MAX_FLOAT=${MAX_FLOAT})
endif(MAX_FLOAT)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_library(printf SHARED printf.c)
target_compile_options(printf PUBLIC -Wall -Wextra -pedantic -Werror)
