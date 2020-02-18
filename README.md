## EELXXXX - IoT LoRa

This branch contains the firmware of EELXXXX discipline. The LoRaWAN stack version used is the [1.0.3](https://lora-alliance.org/sites/default/files/2018-07/lorawan1.0.3.pdf), which can be obtained in the [LoRa-Mac node](https://github.com/Lora-net/LoRaMac-node/) project. The buid system is composed by CMake and the GNU ARM-Toolchain.

#### Folders structure

The folders structure used in the project is:

    .
    ├── cmake                   # CMAKE generation files.
        ├── stm32l0.cmake       # File that contains the compilation flags.
    ├── Docs                    # Boards schematics and usefull commands.
    ├── src
        ├── apps                # Main application files for different boards.
        ├── boards              # Boards peripherals and HAL drivers.
        ├── mac                 # LoRaWAN stack.
        ├── peripherals         # External and internal sensors drivers.
        ├── radio               # Semtech radios (SX127x) drivers.
        ├── system              # Peripherals abstraction functions, used in main application.
    └── ...

Each `src/` subfolder contains a `CMakeLists.txt` file, where it is specified what C files should be compiled and auxiliary directories paths are included. When adding a new file, it is necessary to update the correspondet CMake file.

#### Prerequisites

* **CMake >= 3.6**

```sh
$ sudo apt-get install cmake
```

* **GNU ARM-Toolchain**

```sh
$ sudo apt-get install gcc-arm-none-eabi
```

* **Make**

```sh
$ sudo apt-get install make
```

#### Available configuration options for generation files command

There is the possibility to choose the application, target board and more options using the provided configuration options.

These configuration options can be set through command line parameters.
    
##### Options available:

| Parameter          | Option values |
| -------------      | :-------------|
| `APPLICATION`      | **LoRaMac** |
| `SUB_PROJECT`      | **classA**, **classC** |
| `BOARD`            | **B-L072Z-LRWAN1** |

#### Compiling the code

Before compiling the code, it is necessary to generate the Makefile using the **cmake** tool. The example below considers the using of B-L072Z-LRWAN1 board:

```sh
$ cd ith/
$ mkdir build
$ cd build
$ cmake -DCMAKE_TOOLCHAIN_FILE="cmake/toolchain-arm-none-eabi.cmake" -DAPPLICATION="LoRaMac" -DSUB_PROJECT="classA" -DBOARD="B-L072Z-LRWAN1" ..
```

To compile:

```sh
$ make
```

The binary file will be located in ```src/apps/LoRaMac/LoRaMac-classA.bin```. To clean the build files, use: ```make clean```. To remove all files created by CMake, just delete the ```build/``` folder and start over.

#### Flashing the binary

#### Updating the code
