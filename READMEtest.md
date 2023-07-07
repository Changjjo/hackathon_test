# CommonAPI vSomeIP QT Setup 

## Contents
- [Step 1: Install OpenJDK Java 8](#step-1-install-openjdk-java-8)
- [Step 2: Install Boost.Asio library](#step-2-install-boostasio-library)
- [Step 3: Build the CommonAPI Runtime Library](#step-3-build-the-commonapi-runtime-library)
- [Step 4: Build the vsomeip Library](#step-4-build-the-vsomeip-library)
- [Step 5: Build the CommonAPI SOME/IP Runtime Library](#step-5-build-the-commonapi-someip-runtime-library)
- [Step 6: Write the Franca file and generate code](#step-6-Write-the-Franca-file-and-generate-code)
- [Step 7: Install Qt](#step-7-install-qt)
---
<br/>

## Step 1: Install OpenJDK Java 8
```bash
sudo apt update
sudo apt install openjdk-8-jdk
```

You can check installation

```bash
java --version
```

If you have installed both OpenJDK 8 and 11, your default version will OpenJDK 11.
![스크린샷, 2023-07-07 21-12-10](https://github.com/AveesLab/sea-me-hackathon-2023/assets/96398568/82db3734-5118-43cd-a31d-73ef9796c786)

To manually set a Java version, start by running the following command

```bash
sudo update-alternatives --config java
```

Select number and set OpenJDK 8 as the system default
![스크린샷, 2023-07-07 21-11-46](https://github.com/AveesLab/sea-me-hackathon-2023/assets/96398568/17fe2b05-43fd-4877-a5dc-8143cdaac17d)
```bash
java -version
```
![스크린샷, 2023-07-07 21-11-11](https://github.com/AveesLab/sea-me-hackathon-2023/assets/96398568/ddce9df6-0907-4aa8-bb33-914214bebbba)


<br/>

## Step 2: Install Boost.Asio library
Install Boost-dev
```bash
sudo apt-get install libboost-all-dev
```

<br/>

## Step 3: Build the CommonAPI Runtime Library

Make working directory. In my case `build-commonapi`

```bash
cd ~
mkdir build-commonapi && cd build-commonapi
```

Start with fetching the source code of CommonAPI:

```bash
git clone https://github.com/GENIVI/capicxx-core-runtime.git
cd capicxx-core-runtime/
git checkout 3.2.0
mkdir build
cd build
cmake ..
make -j6
sudo make install
```

Result:

```bash
[100%] Linking C shared library libCommonAPI.so
[100%] Built target CommonAPI
```

<br/>

## Step 4: Build the vsomeip Library


```bash
sudo apt-get install asciidoc source-highlight doxygen graphviz libgtest-dev
```
Before download SOME/IP Runtime library, you should download vsomeip. Because CommonAPI C++ SOME/IP need vsomeip.

```bash
cd ~
cd build-commonapi
git clone https://github.com/COVESA/vsomeip.git
cd vsomeip
git checkout 3.1.20.3
mkdir build
cd build
cmake -DENABLE_SIGNAL_HANDLING=1 -DDIAGNOSIS_ADDRESS=0x10 ..
make -j6
sudo make install
```


Result:

```bash
[100%] Linking CXX executable vsomeipd
[100%] Built target vsomeipd
```

<br/>

## Step 5: Build the CommonAPI SOME/IP Runtime Library

Download CommonAPI SOME/IP Runtime Library and change version

```bash
cd ~
cd build-commonapi
git clone https://github.com/GENIVI/capicxx-someip-runtime.git
cd capicxx-someip-runtime/
git checkout 3.2.0
mkdir build
cd build
cmake -DUSE_INSTALLED_COMMONAPI=OFF ..
make -j6
sudo make install
```

Result:

```bash
[100%] Linking CXX shared library libCommonAPI-SomeIP.so
[100%] Built target CommonAPI-SomeIP
```

<br/>

## Step 6: Write the Franca file and generate code

Unfortunately, code generator doesn’t support arm architecture. So if you want to use this generator, I recommend that you use the code generator on your laptop and then download the generated code via Git. The code generator automatically generates codes according to fidl and fdepl files. In the case of vsomeip, you have to run it twice with core-generator and some-generator to complete it.

Create commonapi project directory and open Franca IDL
```bash
cd ~
mkdir fidl
cd fidl
```
Cluster.fdepl
Cluster.fidl


## Step 7: Install Qt


```bash
sudo apt-get install qt5-default
sudo apt-get install qtcreator
sudo apt-get install qtdeclarative5-dev
```

You must install Qt module
```bash
sudo apt-get install qtmultimedia5-dev
sudo apt-get install qml-module-qtquick-controls2
sudo apt-get install libqt5multimediawidgets5 libqt5multimedia5
sudo apt-get install libqt5multimedia5-plugins qml-module-qtmultimedia

```
