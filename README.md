# STM32 C code and Google Test Framework

[![Language](https://img.shields.io/badge/Made%20with-C-blue.svg)](https://shields.io/)
![License](https://camo.githubusercontent.com/890acbdcb87868b382af9a4b1fac507b9659d9bf/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f6c6963656e73652d4d49542d626c75652e737667)
[![Test](https://github.com/CharlesDias/stm32_gtest_c_code/actions/workflows/unit-test.yml/badge.svg)](https://github.com/CharlesDias/stm32_gtest_c_code/actions/workflows/unit-test.yml)
[![codecov](https://codecov.io/gh/CharlesDias/stm32_gtest_c_code/branch/main/graph/badge.svg)](https://codecov.io/gh/CharlesDias/stm32_gtest_c_code)
[![Lizard](https://github.com/CharlesDias/stm32_gtest_c_code/actions/workflows/lizard.yml/badge.svg)](https://github.com/CharlesDias/stm32_gtest_c_code/actions/workflows/lizard.yml)
[![Flawfinder](https://github.com/CharlesDias/stm32_gtest_c_code/actions/workflows/flawfinder.yml/badge.svg)](https://github.com/CharlesDias/stm32_gtest_c_code/actions/workflows/flawfinder.yml)

This is a sample project for testing C code for STM32 microcontrollers using the Google Test Framework. Some topics covered:

* Sample project using the NUCLEO-F446ZE board.
* Embedded system without RTOS (bare metal).
* Distinct folders for library, executable, and test code.
* Use of STM32CubeIDE for building and compiling the application project.
* Use of CMake for building the test code.
* Testing C code via Google Test Framework.
* Use GMock for mocking the STM32 HAL functions.
* Code coverage with Github Actions and [Codecov](https://codecov.io).
* Code quality analysis with Lizard and Flawfinder tools.
* Assert verification and prints the failures via huart3.
* Use of Docker container.

## Project structure

``` text
./
├── CMakeLists.txt
│
├── cmake
│   └── cmake modules
│
├── docker
│   └── Dockerfile
│
├── docs
│   └── Documentation files
│
├── .github
│   └── workflows
│       └── GitHub workflows
│
├── source
│   ├── CMakeLists.txt
│   │
│   ├── nucleo-f446ze-library
│   │   ├── CMakeLists.txt
│   │   ├── BuildArtifacts
│   │   │   └── Library artifacts
│   │   ├── Drivers 
│   │   │   └── Files generated by STM32CubeIDE
│   │   ├── Inc
│   │   │   └── Files generated by STM32CubeIDE
│   │   ├── Libraries
│   │   │   └── Header and source files
│   │   └── Src
│   │       └── Files generated by STM32CubeIDE
│   │
│   └── stm32-cube-ide
│       ├── Core (Files generated by STM32CubeIDE)
│       │   ├── Inc 
│       │   │   └── Files generated by STM32CubeIDE
│       │   ├── Src
│       │   │   ├── main.c (Sample code)
│       │   │   └── ...
│       │   └── Startup
│       │       └── Files generated by STM32CubeIDE
│       └── Drivers
│           └── Files generated by STM32CubeIDE
│
└── tests
    ├── CMakeLists.txt
    ├── header-overrides
    │   └── Overrides some header files copied from the STM32CubeIDE project that are needed by the mock
    ├── integration
    │   └── integration_hello_test.cpp
    ├── mock
    │   ├── fixture.h
    │   └── hal_gpio_mock.cpp
    └── unit
        ├── gpio_test.cpp
        └── unit_hello_test.cpp
```

## Building tests project via CMake

Clone this repo for your local machine

```console
git clone https://github.com/CharlesDias/stm32_gtest_c_code.git
```

Access the project folder **stm32_gtest_c_code**

```console
cd stm32_gtest_c_code
```

Pull the latest docker image used to build the project.

```console
docker pull charlesdias/stm32_gtest
```

Run the image docker.

```console
docker run --rm -it -v $(pwd):/home/project -w /home/project charlesdias/stm32_gtest
```

Run the command below inside the Docker container

```console
make clean && make build && make test
```

Access the `build/coverage/index.html` file to see the coverage report.

### Dependency graph

Dependency graph for test project.

![Dependency graph](docs/images/dependency_graph.png "Dependency graph")

## Building application project via STM32CubeIDE

Clone this repo for your local machine

```console
git clone https://github.com/CharlesDias/stm32_gtest_c_code.git
```

Open the STM32CubeIDE and import this project.

Build and load the firmware on NUCLEO-F446ZE board. See the expected output.

![STM32 project](docs/images/stm32_gtest.gif "STM32 project")

## Improvement suggestions

* Add some function example to increase the CCN (cyclomatic complexity number).
* Add some function example with security weaknesses to test the Flawfinder.
* Build the application project via CMake.
* Add Doxygen configuration.
