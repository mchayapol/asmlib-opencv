CMAKE_MINIMUM_REQUIRED (VERSION 2.6)
PROJECT( asmlib-opencv )

#set (CMAKE_MODULE_PATH ".;${CMAKE_MODULE_PATH}")
set (CMAKE_PREFIX_PATH "f:/dev/opencv/build;${CMAKE_PREFIX_PATH}")
# set (CMAKE_MODULE_PATH "f:/dev/opencv/build;${CMAKE_MODULE_PATH}")
set (CMAKE_INSTALL_PREFIX "../build")
set (OPENCV_INCLUDE_DIR "f:/dev/opencv/sources/include;f:/dev/opencv/sources/include;F:/dev/opencv/sources/modules/core/include;F:/dev/opencv/build;F:/dev/opencv/sources/modules/imgproc/include;F:/dev/opencv/sources/modules/photo/include;F:/dev/opencv/sources/modules/video/include;F:/dev/opencv/sources/modules/highgui/include;;F:/dev/opencv/sources/modules/imgcodecs/include;F:/dev/opencv/sources/modules/objdetect/include;F:/dev/opencv/sources/modules/videoio/include")

FIND_PACKAGE( OpenCV REQUIRED )
SET(LIB_SRC_LIST modelfile.cpp asmmodel.cpp shapevec.cpp similaritytrans.cpp afreader.cpp modelimage.cpp  shapemodel.cpp shapeinfo.cpp)

INCLUDE_DIRECTORIES( ${OPENCV_INCLUDE_DIR} )
OPTION(ENABLE_ANNOTATOR "Compile the GUI point annotator (Qt Needed)" OFF)

IF (ENABLE_ANNOTATOR)
	ADD_SUBDIRECTORY (annotation)
ENDIF (ENABLE_ANNOTATOR)

FIND_PACKAGE( Doxygen )
IF (DOXYGEN_FOUND)
	CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile @ONLY)
	ADD_CUSTOM_TARGET(doc
		${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile
		WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
		COMMENT "Generating API and source documentation with Doxygen" VERBATIM
	)
ENDIF(DOXYGEN_FOUND)

ADD_SUBDIRECTORY(demo)
ADD_SUBDIRECTORY(lib)
