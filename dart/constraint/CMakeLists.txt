# Search all header and source files
file(GLOB hdrs "*.hpp")
file(GLOB srcs "*.cpp")
file(GLOB detail_hdrs "detail/*.hpp")
file(GLOB detail_srcs "detail/*.cpp")
dart_add_core_headers(${hdrs} ${detail_hdrs})
dart_add_core_sources(${srcs} ${detail_srcs})

# Generate header for this namespace
dart_get_filename_components(header_names "constraint headers" ${hdrs})
dart_generate_include_header_file(
  "${CMAKE_CURRENT_BINARY_DIR}/constraint.hpp"
  "dart/constraint/"
  ${header_names}
)

# Install
if(NOT DART_BUILD_DARTPY)
  install(
    FILES ${hdrs} ${CMAKE_CURRENT_BINARY_DIR}/constraint.hpp
    DESTINATION include/dart/constraint
    COMPONENT headers
  )
  install(
    FILES ${detail_hdrs}
    DESTINATION include/dart/constraint/detail
    COMPONENT headers
  )
endif()

dart_format_add(
  BoxedLcpConstraintSolver.hpp
  BoxedLcpConstraintSolver.cpp
  BoxedLcpSolver.hpp
  ContactConstraint.hpp
  ContactConstraint.cpp
  DantzigBoxedLcpSolver.hpp
  DantzigBoxedLcpSolver.cpp
  MimicMotorConstraint.hpp
  MimicMotorConstraint.cpp
  PgsBoxedLcpSolver.hpp
  PgsBoxedLcpSolver.cpp
  SmartPointer.hpp
  detail/BoxedLcpSolver-impl.hpp
)
