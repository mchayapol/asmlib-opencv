PROJECT( asmlib-opencv-demo )
FIND_PACKAGE( OpenCV REQUIRED )
SET(TEST_SRC main.cpp XGetopt.cpp)

INCLUDE_DIRECTORIES( ../lib/ )
# INCLUDE_DIRECTORIES( f:/dev/opencv/build/include/opencv )

ADD_EXECUTABLE( demo ${TEST_SRC})
TARGET_LINK_LIBRARIES( demo asm ${OpenCV_LIBS})
