LIST(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/../../../cmake")

PROJECT(KlayGE)

CMAKE_MINIMUM_REQUIRED(VERSION 2.8.6)

IF(COMMAND cmake_policy)
	CMAKE_POLICY(SET CMP0003 NEW)
ENDIF(COMMAND cmake_policy)

SET(KLAYGE_MAJOR_VERSION 4)
SET(KLAYGE_MINOR_VERSION 9)
SET(KLAYGE_PATCH_VERSION 0)
SET(KLAYGE_VERSION ${KLAYGE_MAJOR_VERSION}.${KLAYGE_MINOR_VERSION}.${KLAYGE_PATCH_VERSION})

FIND_PATH(KLAYGE_PROJECT_DIR klayge_logo.ico PATHS ../../)
MARK_AS_ADVANCED(KLAYGE_PROJECT_DIR)
SET(KLAYGE_ROOT_DIR "${KLAYGE_PROJECT_DIR}/..")

INCLUDE(${KLAYGE_ROOT_DIR}/cmake/Common.cmake)
INCLUDE(${KLAYGE_ROOT_DIR}/cmake/Platform.cmake)
INCLUDE(${KLAYGE_ROOT_DIR}/cmake/Compiler.cmake)
INCLUDE(${KLAYGE_ROOT_DIR}/cmake/ConfigBoost.cmake)

SET_PROPERTY(GLOBAL PROPERTY USE_FOLDERS ON)

# Main settings and dependencies
SET(KLAYGE_CORELIB_NAME KlayGE_Core)  # Dependency of all other targets

SET(KLAYGE_OUTPUT_DIR "${KLAYGE_PROJECT_DIR}/lib/${KLAYGE_PLATFORM_NAME}")
SET(KLAYGE_BIN_DIR "${KLAYGE_PROJECT_DIR}/bin/${KLAYGE_PLATFORM_NAME}")

ADD_CUSTOM_TARGET(AllInEngine)
SET_TARGET_PROPERTIES(AllInEngine PROPERTIES FOLDER "Engine")

ADD_SUBDIRECTORY(Engine)
ADD_SUBDIRECTORY(Samples)
ADD_SUBDIRECTORY(Tutorials)

IF(KLAYGE_IS_DEV_PLATFORM)
	ADD_SUBDIRECTORY(Tests)
	ADD_SUBDIRECTORY(Tools)
	ADD_SUBDIRECTORY(Exporters)
ENDIF()


