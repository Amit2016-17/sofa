cmake_minimum_required(VERSION 3.12)
project(SofaMiscForceField)

find_package(SofaFramework REQUIRED) # SofaHelper
find_package(SofaCommon REQUIRED) # SofaDeformable
find_package(SofaGeneral REQUIRED) # SofaBoundaryCondition SofaGeneralTopology

set(HEADER_FILES
    config.h
    initMiscForcefield.h
    )

set(SOURCE_FILES
    initMiscForcefield.cpp
    )

list(APPEND HEADER_FILES
    GearSpringForceField.h
    GearSpringForceField.inl
    MeshMatrixMass.h
    MeshMatrixMass.inl
    )
list(APPEND SOURCE_FILES
    GearSpringForceField.cpp
    MeshMatrixMass.cpp
    )

if(SOFA_WITH_DEPRECATED_COMPONENTS)
    list(APPEND HEADER_FILES
        LennardJonesForceField.h
        LennardJonesForceField.inl
        )
    list(APPEND SOURCE_FILES
        LennardJonesForceField.cpp
        )
endif()

add_library(${PROJECT_NAME} SHARED ${HEADER_FILES} ${SOURCE_FILES})
target_link_libraries(${PROJECT_NAME} PUBLIC SofaHelper SofaDeformable SofaBoundaryCondition SofaMiscTopology SofaGeneralTopology)

sofa_install_targets(SofaMisc ${PROJECT_NAME} "SofaMisc/${PROJECT_NAME}")
