#######
# Dlt - Diagnostic Log and Trace
# @licence make begin@
 #
 # Copyright (C) 2011, BMW AG - Alexander Wenzel <alexander.wenzel@bmw.de>
 # 
 # This program is free software; you can redistribute it and/or modify it under the terms of the 
 # GNU Lesser General Public License, version 2.1, as published by the Free Software Foundation.
 # This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even 
 # the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Lesser General 
 # Public License, version 2.1, for more details.
 # 
 # You should have received a copy of the GNU Lesser General Public License, version 2.1, along 
 # with this program; if not, see <http://www.gnu.org/licenses/lgpl-2.1.html>.
 # 
 # Note that the copyright holders assume that the GNU Lesser General Public License, version 2.1, may 
 # also be applicable to programs even in cases in which the program is not a library in the technical sense.
 # 
 # Linking DLT statically or dynamically with other modules is making a combined work based on DLT. You may 
 # license such other modules under the GNU Lesser General Public License, version 2.1. If you do not want to 
 # license your linked modules under the GNU Lesser General Public License, version 2.1, you 
 # may use the program under the following exception.
 # 
 # As a special exception, the copyright holders of DLT give you permission to combine DLT 
 # with software programs or libraries that are released under any license unless such a combination is not
 # permitted by the license of such a software program or library. You may copy and distribute such a 
 # system following the terms of the GNU Lesser General Public License, version 2.1, including this
 # special exception, for DLT and the licenses of the other code concerned.
 # 
 # Note that people who make modified versions of DLT are not obligated to grant this special exception 
 # for their modified versions; it is their choice whether to do so. The GNU Lesser General Public License, 
 # version 2.1, gives permission to release a modified version without this exception; this exception 
 # also makes it possible to release a modified version which carries forward this exception.
 #
 # @licence end@
########

function(convert_odt ODT_FILE)
  set(pdf "${CMAKE_CURRENT_BINARY_DIR}/${ODT_FILE}.pdf")
  set(odt "${CMAKE_CURRENT_SOURCE_DIR}/${ODT_FILE}.odt")
  add_custom_command(
    OUTPUT ${pdf}
    DEPENDS ${odt}
    COMMAND unoconv
    ARGS --format=pdf --stdout ${odt} > ${pdf}
  )
endfunction(convert_odt) 

convert_odt("GENIVI_UserManual_DLT_Client")
convert_odt("GENIVI_UserManual_DLT_Daemon")
convert_odt("GENIVI_Specification_DLT_Daemon")

ADD_CUSTOM_TARGET(Documents ALL echo DEPENDS 
${CMAKE_CURRENT_BINARY_DIR}/GENIVI_UserManual_DLT_Client.pdf 
${CMAKE_CURRENT_BINARY_DIR}/GENIVI_UserManual_DLT_Daemon.pdf 
${CMAKE_CURRENT_BINARY_DIR}/GENIVI_Specification_DLT_Daemon.pdf)

INSTALL(FILES 	${CMAKE_CURRENT_SOURCE_DIR}/GENIVI_UserManual_DLT_Client.odt
		${CMAKE_CURRENT_SOURCE_DIR}/GENIVI_UserManual_DLT_Daemon.odt
		${CMAKE_CURRENT_SOURCE_DIR}/GENIVI_Specification_DLT_Daemon.odt
		${CMAKE_CURRENT_BINARY_DIR}/GENIVI_UserManual_DLT_Client.pdf 
		${CMAKE_CURRENT_BINARY_DIR}/GENIVI_UserManual_DLT_Daemon.pdf 
		${CMAKE_CURRENT_BINARY_DIR}/GENIVI_Specification_DLT_Daemon.pdf
		${CMAKE_CURRENT_SOURCE_DIR}/GENIVI_Specification_DLT_Daemon.vsd
	DESTINATION "doc/${CMAKE_PROJECT_NAME}"
	COMPONENT doc)
