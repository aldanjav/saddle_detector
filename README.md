# saddle_detector
A novel similarity-covariant feature detector that extracts points whose
neighborhoods, when treated as a 3D intensity surface, have a saddle-like
intensity profile. The saddle condition is verified efficiently by intensity
comparisons on two concentric rings that must have exactly two dark-to-bright
and two bright-to-dark transitions satisfying certain geometric constraints.
Saddle is a fast approximation of Hessian detector as ORB detector is for
Harris detector. Experiments show that the Saddle features are general, evenly
spread and appearing in high density in a range of images.

The Saddle detector is among the fastest proposed. In comparison with detector
with similar speed, the Saddle features show superior matching performance on
number of challenging datasets.

# Python3 support
This fork adds the python3 support for the original saddle_detector package. So far, it was tested on MacOS catalina and Fedora 30.
The saddle_detector package was first migrated to opencv4 (very minor changes)
and then the OpenCV scripts for creating python wrappers were adapted. If the
host system has Python3, NumPy, and OpenCV 4 installed, the python module
pysaddlepts is built automatically.

## Building and installation
Make sure you have CMake, Python3, Numpy, and OpenCV 4 installed on your system. To install the `pysaddlepts` module run following in your terminal (please, change `<YOUR_PYTHONPATH>` to the python path where you want to install the compiled python moudule):
```
cd <build_path>
git clone https://github.com/brejchajan/saddle_detector.git
cd saddle_detector
mkdir build && cd build
cmake -DPYTHON_INSTALL_PATH=<YOUR_PYTHONPATH> ..
make
make install
```

# Testing pysaddle python module
To test the python module, run:
```
cd <build_path>/saddle_detector
python3 build/pysaddletest.py
```

A test image with detected keypoints should be shown. Please note that the default parameter setting of the keypoint detector may be slightly different to the C++ version.
