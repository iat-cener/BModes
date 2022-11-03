
set(NWTCLIBS_SOURCES NWTC_Library.f90 NWTC_IO.f90 NWTC_Num.f90 NWTC_Aero.f90
  ModMesh.f90 DoubPrec.f90)

#get_filename_component(FCNAME "${CMAKE_Fortran_COMPILER}" NAME)

if (APPLE OR UNIX)
  if (${CMAKE_Fortran_COMPILER_ID} STREQUAL "GNU")
    list (APPEND NWTCLIBS_SOURCES SysGnuLinux.f90)

  elseif (FCNAME MATCHES "ifort.*")
    list (APPEND NWTCLIBS_SOURCES SysIFL.f90)
  endif ()
elseif (WIN32)
  if (${CMAKE_Fortran_COMPILER_ID} STREQUAL "GNU")
    list (APPEND NWTCLIBS_SOURCES SysGnuWin.f90)
  elseif (FCNAME MATCHES "ifort.*")
    list (APPEND NWTCLIBS_SOURCES SysIVF.f90)
  endif ()
endif (APPLE OR UNIX)

message(${NWTCLIBS_SOURCES})
add_library(nwtclibs  ${NWTCLIBS_SOURCES})
target_link_libraries(nwtclibs ${LAPACK_LIBRARIES} ${CMAKE_DL_LIBS})

install(TARGETS nwtclibs
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib)
