cmake_minimum_required(VERSION 3.0.0)

set(ETH_CMAKE_DIR "${CMAKE_CURRENT_LIST_DIR}/webthree-helpers/cmake" CACHE PATH "The path to the cmake directory")
list(APPEND CMAKE_MODULE_PATH ${ETH_CMAKE_DIR})

set(UTILS_DIR "${CMAKE_CURRENT_LIST_DIR}/webthree-helpers/utils" CACHE PATH "The path to the utils libraries directory")
set(DEV_DIR "${CMAKE_CURRENT_LIST_DIR}/libweb3core" CACHE PATH "The path to the dev libraries directory")
set(ETH_DIR "${CMAKE_CURRENT_LIST_DIR}/libethereum" CACHE PATH "The path to the eth libraries directory")
set(WEB3_DIR "${CMAKE_CURRENT_LIST_DIR}/webthree" CACHE PATH "The path to the webthree libraries directory")
set(SOL_DIR "${CMAKE_CURRENT_LIST_DIR}/solidity" CACHE PATH "The path to the solidity libraries directory")
set(JSONCPP_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/install/x64/include" CACHE PATH "The path to the jsoncpp headers directory")
set(JSONCPP_LIBRARY "${CMAKE_CURRENT_LIST_DIR}/install/x64/lib" CACHE PATH "The path to the jsoncpp libraries directory")
set(LEVELDB_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/install/x64/include" CACHE PATH "The path to the leveldb headers directory")
set(LEVELDB_LIBRARY "${CMAKE_CURRENT_LIST_DIR}/install/x64/lib" CACHE PATH "The path to the leveldb libraries directory")
set(CRYPTOPP_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/install/x64/include" CACHE PATH "The path to the cryptopp headers directory")
set(CRYPTOPP_LIBRARY "${CMAKE_CURRENT_LIST_DIR}/install/x64/lib" CACHE PATH "The path to the cryptopp libraries directory")
set(MINIUPNPC_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/install/x64/include" CACHE PATH "The path to the miniupnpc headers directory")
set(MINIUPNPC_LIBRARY "${CMAKE_CURRENT_LIST_DIR}/install/x64/lib" CACHE PATH "The path to the miniupnpc libraries directory")

set(Boost_USE_STATIC_LIBS ON)
set(BOOST_LIBRARYDIR "${CMAKE_CURRENT_LIST_DIR}/install/win64/lib" CACHE PATH "The path to the boost libraries directory")
set(Boost_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/install/win64/include" CACHE PATH "The path to the boost libraries directory")

# set cmake_policies
include(EthPolicy)
eth_policy()

# project name and version should be set after cmake_policy CMP0048
project(cpp-ethereum VERSION "1.2.2")

include(EthCompilerSettings)

include(EthExecutableHelper)

include(EthDependencies)

include(EthUtils)

include(EthOptions)
configure_project(GUI SOLIDITY)

add_subdirectory(webthree-helpers/utils)

add_subdirectory(libweb3core)
add_subdirectory(libethereum)
add_subdirectory(webthree)

if (SOLIDITY)
	add_subdirectory(solidity)
endif()

if (GUI)
	add_subdirectory(alethzero)
	if (SOLIDITY)
		add_subdirectory(mix)
	endif()
	eth_appdmg()
	eth_nsis()
endif()
