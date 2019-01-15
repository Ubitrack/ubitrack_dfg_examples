Ubitrack Dataflow Examples (and collection of test cases for QA)
----------------------------------------------------------------

| Description                            | Linux x64    | Windows x64 | Macos x64 |
|:---------------------------------------|:-------------|:------------|:----------|
| basic_videodisplay_opengl.dfg          | ok           |             |           |
| basic_videodisplay_opengl_gpuimage.dfg | fail[1]      |             |           |
| basic_videodisplay_opencv.dfg          | fail[2]      |             |           |
| calibrate_camera_aruco.dfg             | ok           |             |           |
| calibrated_videodisplay_opengl.dfg     | ok           |             |           |
| tracking_aruco.dfg                     | incorrect[3] |             |           |
| tracking_ubitrack_marker.dfg           | ok           |             |           |


[1] Ubuntu 18.04 x64: relocation error: lib/libutvision.so.1.3: symbol clGetGLContextInfoKHR version OPENCL_1.0 not defined in file libOpenCL.so.1 with link time reference

[2] Ubuntu 18.04 x64: OpenCV(3.4.3) /opencv/modules/highgui/src/window.cpp:615: error: (-2:Unspecified error) The function is not implemented. Rebuild the library with Windows, GTK+ 2.x or Carbon support. If you are on Ubuntu or Debian, install libgtk2.0-dev and pkg-config, then re-run cmake or configure script in function 'cvNamedWindow'

[3] Augmented model (coord_system.dae): rotation is not correct => Programming error, check with Frieder/Felix, probably located in aruco-marker tracker component, since visualization looks valid