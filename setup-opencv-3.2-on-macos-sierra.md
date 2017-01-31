# How to install opencv 3.2 on macOS sierra with python 3.6

##Prerequisits

* install xcode
* install homebrew (http://brew.sh)

##Install python3

```
brew install python3
brew linkapps python3
```

##setup virtualenv

```
/usr/local/bin/pip3.6 install virtualenv virtualenvwrapper
echo "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.bash_profile

mkvirtualenv computer-vision -p python3
# make sure you are inside (computer-vision) virtualenv

pip install numpy matplotlib scikit-image imutils

```

#install opencv from source

```
brew install cmake pkg-config jpeg libpng libtiff openexr eigen tbb

mkdir ~/opencv
wget https://github.com/opencv/opencv/archive/3.2.0.zip
unzip 3.2.0.zip 
wget https://github.com/opencv/opencv_contrib/archive/3.2.0.zip
unzip 3.2.0.zip.1

mkidr opencv-3.2.0/build
cd opencv-3.2.0/build

# fix: http://answers.opencv.org/question/121587/undefined-freetype-symbols-when-building-opencv-320/

cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=~/opencv/opencv_contrib-3.2.0/modules \
    -D PYTHON3_LIBRARY=/usr/local/Cellar/python3/3.6.0/Frameworks/Python.framework/Versions/3.6/lib/python3.6/config-3.6m-darwin/libpython3.6.dylib \
    -D PYTHON3_INCLUDE_DIR=/usr/local/Cellar/python3/3.6.0/Frameworks/Python.framework/Versions/3.6/include/python3.6m/ \
    -D PYTHON3_EXECUTABLE=$VIRTUAL_ENV/bin/python \
    -D BUILD_opencv_python2=OFF -D BUILD_opencv_python3=ON -D INSTALL_PYTHON_EXAMPLES=ON \
    -D INSTALL_C_EXAMPLES=OFF -D BUILD_EXAMPLES=ON ..
    
