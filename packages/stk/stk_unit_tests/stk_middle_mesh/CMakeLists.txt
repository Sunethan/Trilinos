TRIBITS_INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR})
TRIBITS_INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR})
TRIBITS_INCLUDE_DIRECTORIES(${${PARENT_PACKAGE_NAME}_BINARY_DIR}/stk_util/stk_util)
TRIBITS_INCLUDE_DIRECTORIES(${${PARENT_PACKAGE_NAME}_SOURCE_DIR}/stk_middle_mesh)
TRIBITS_INCLUDE_DIRECTORIES(${${PARENT_PACKAGE_NAME}_SOURCE_DIR}/stk_middle_mesh/stk_middle_mesh)
TRIBITS_INCLUDE_DIRECTORIES(${${PARENT_PACKAGE_NAME}_SOURCE_DIR}/stk_middle_mesh/stk_middle_mesh/predicates)

FILE(GLOB SOURCES *.cpp util/*.cpp)


TRIBITS_ADD_EXECUTABLE(
    stk_middle_mesh_utest
    SOURCES ${SOURCES}
    TESTONLYLIBS stk_unit_main
    COMM serial mpi
    NOEXEPREFIX
    )

TRIBITS_ADD_TEST(
    stk_middle_mesh_utest
    ARGS ""
    COMM serial mpi
    NUM_MPI_PROCS 1
    NOEXEPREFIX
    )
