# Original notes

Implementation for MobiCom'18 paper **DeepCache: Principled Cache for Mobile Deep Vision**.

---

This implementation is based on [Tencent ncnn](https://github.com/Tencent/ncnn).

The folder *CNNCache* is an Android demo of DeepCache, including the image matching algorithm in RenderScript, a real-time app, and the benchmark. Some configuration in CMake file needs to be updated according to your enviornment.


## Other notes
* The version of ncnn used currently is rather old. We plan to update it to newer one.

* Current implemention doesn't support neon in ncnn. Let's make it later.


# Preliminary

* Windows 10 (tested at 1903)

* Visual Studio 2019: C/C++ suite 

* Android Studio 3.5: 

![avatar](/img/SDK_Platforms.png)

![avatar](/img/SDK_Tools.png)

![avatar](/img/SDK_Update_Sites.png)

# Build process

## At desktop side

* Download DeepCache-master.zip and unzip.

* cd DeepCache-master, mkdir build-android, cd build-android.

* prepare android toolchain: at the directory of Android NDK, <Your_NDK_directory>\ndk\<Your_NDK_version>(tested at 20.0.5594570)\build\cmake\android.toochain.cmake

* cmake -G "Unix Makefiles" -DCMAKE_TOOLCHAIN_FILE=<Your_NDK_directory>/ndk/20.0.5594570/build/cmake/android.toolchain.cmake -DANDROID_ABI="armeabi-v7a" -DANDROID_ARM_NEON=OFF -DCMAKE_MAKE_PROGRAM="<Your_NDK_directory>/ndk/20.0.5594570/prebuilt/windows-x86_64/bin/make.exe" -DANDROID_PLATFORM=android-16(16 stands for Android 6.0, which is used in DeepCache paper) ..

* cmake --build .

* cmake --build . --target install

## At app side

* Import CNNCache to Android Studio

* Modify a few directory in NCNN.java, ClassifierActivity.java, BenchmarkActivity.java, search for /mnt/sdcard/data (locates in the internal storage of Honor A5), and change it to your own directory)

* Connect your cellphone to your desktop, copy squeezenet_v1.1.bin and squeezenet_v1.1.param into the directory /mnt/sdcard/data/ncnn/models in your cellphone (or change it to your own directory). 

* Build and Run CNNCache in Android Studio

* Further modification...

## Other notes

* The origin repo doesn't provide .cpp files for googlenet, alexnet or others mentioned in the paper, so we have to search them online or implement them ourselves.

* The ncnn version is some version between tag 20171017 or 20170919, and some of the code is modified by the DeepCache author.

