# Copyright 2021 CNRS - Airbus SAS
# Author: Florent Lamiraux, Joseph Mirabel
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are
# met:

# 1. Redistributions of source code must retain the above copyright
# notice, this list of conditions and the following disclaimer.

# 2. Redistributions in binary form must reproduce the above copyright
# notice, this list of conditions and the following disclaimer in the
# documentation and/or other materials provided with the distribution.

# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
# "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
# LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
# A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
# HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
# SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
# LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
# DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
# THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
# (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
# OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

find_package(pal_navigation_cfg_tiago)
if (pal_navigation_cfg_tiago_FOUND)
  set(pal_navigation_cfg_tiago_SHARE ${pal_navigation_cfg_tiago_PREFIX}/share/pal_navigation_cfg_tiago)
  install(CODE "execute_process(COMMAND ${CMAKE_COMMAND} -E make_directory \"${CMAKE_INSTALL_PREFIX}/${CATKIN_PACKAGE_SHARE_DESTINATION}/tiago/config/base/\")")
  foreach(subdir "common" "global_planner")
    set(filepath "${pal_navigation_cfg_tiago_SHARE}/config/base/${subdir}")
    install(CODE "execute_process(COMMAND ${CMAKE_COMMAND} -E create_symlink \"${filepath}\" \"${CMAKE_INSTALL_PREFIX}/${CATKIN_PACKAGE_SHARE_DESTINATION}/tiago/config/base/${subdir}\")")
  endforeach()
  install(FILES common/teb/local_planner.yaml
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/tiago/config/base/teb)
  install(FILES common/pal/local_planner.yaml
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/tiago/config/base/pal)
endif ()

OPTION(USE_TIAGO_DEBURRING "Install files for tiago deburring demo" OFF)
IF(USE_TIAGO_DEBURRING)
  ADD_SUBDIRECTORY(deburring)
ENDIF()
