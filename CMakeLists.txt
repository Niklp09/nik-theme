project(Nik2Theme)

cmake_minimum_required(VERSION 3.16.0 FATAL_ERROR)

include(WriteBasicConfigVersionFile)
include(FeatureSummary)

find_package(ECM 1.5.0 REQUIRED NO_MODULE)
set(CMAKE_MODULE_PATH ${ECM_MODULE_PATH} ${ECM_KDE_MODULE_DIR})

find_package(KF5 ${KF5_MIN_VERSION} REQUIRED COMPONENTS Plasma)

include(ECMInstallIcons)
include(KDEInstallDirs)
include(KDECMakeSettings)
include(KDECompilerSettings)
include(GenerateExportHeader)

message(STATUS "build yakuake-theme")
add_subdirectory(yakuake)

message(STATUS "build SDDM theme")
configure_file(sddm-theme/theme.conf.cmake ${CMAKE_CURRENT_BINARY_DIR}/sddm-theme/theme.conf)

install(DIRECTORY sddm-theme/ DESTINATION ${KDE_INSTALL_FULL_DATADIR}/sddm/themes/nik
        PATTERN "README.txt" EXCLUDE
        PATTERN "dummydata" EXCLUDE
        PATTERN "theme.conf.cmake" EXCLUDE)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/sddm-theme/theme.conf DESTINATION ${KDE_INSTALL_FULL_DATADIR}/sddm/themes/nik)

feature_summary(WHAT ALL INCLUDE_QUIET_PACKAGES FATAL_ON_MISSING_REQUIRED_PACKAGES)
