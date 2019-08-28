# Programming AVR with USBasp on Linux | manual + Makefile

please refer to [this video](https://www.youtube.com/channel/UCf0Tn4u0rSX6TUrCnSJQjbw) __in arabic__

## Table of contents  
- [USBasp-AVR Connection](#usoasp-avr-connection)
- [Installing Tools](#installing-tools)
- [Uploading code manually](#uploading-code-manually)
- [Using Makefile](#using-makefile)

<p></p>

## USBasp-AVR connection
If the image below is not clear enough, please refer to the first section of [this video](https://youtu.be/ncqy6eEY1yc?t=43).

<p align="center">
  <img width="800" height="512" src="https://raw.githubusercontent.com/AlphaArslan/USBasp-AVR-on-linux-GUIDE/master/images/USBasp_AVR_connection.png">
</p>

<p></p>



## Installing Tools
The following tools need to be installed
* __gcc-avr__ : to compile our code and generate executable files.
* __avr-libc__: which is our C library for AVR.
* __avrdude__: for uploading HEX file to the micro-controller.

You install them all with this command:

```bash
    sudo apt-get install gcc-avr avr-libc avrdude
```

you will also need to update your path variable to avoid problems when using makefile

```bash
    export PATH=$PATH:/usr/lib/gcc/avr/5.4.0/
```

And that's it. We are ready.

<p></p>



## Uploading code manually
To actually upload your code to AVR, you basically need three commands.

* Compile and get binary file:

    ```bash
    avr-gcc -Wall -g -Os -mmcu=atmega32 -o main.bin main.c
    ```

    note here that I'm using __atmega32__. You change it to whatever you use (i.e. atmega16, attiny13).

* Convert binary file to HEX:

    ```bash
    avr-objcopy -j .text -j .data -O ihex main.bin main.hex
    ```

* Upload to the micro-controller:

    ```bash
    avrdude -p atmega32 -c usbasp -U flash:w:main.hex:i -F
    ```

    Again, note that you need to change __atmage32__ to whatever you use.


<p></p>

## Using Makefile
Now, of course it would be pain below your back to write all these commands every time you want to upload your code, rather than confusing. Specially to a newcomer, this can give you a bit of HELL!!

So, I came with a better solution. Using [this Makefile](https://github.com/AlphaArslan/USBasp-AVR-on-linux-GUIDE/blob/master/Makefile) can make it really easy.

##### You just need so little steps to get started
* Put the file in the same folder where __main.c__ is.
* change __atmega32__ in the very first line to whatever you use.

##### now every time you want to upload
* generate binary and HEX files

    ```bash
    make
    ```

* upload the code

    ```bash
    make flash
    ```

and that's it XD.


<p></p>
