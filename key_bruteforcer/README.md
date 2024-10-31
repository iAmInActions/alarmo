# Key Bruteforcer
This project contains a payload intended to be loaded with openocd, which dumps necessary data to bruteforce the AES key.  
It also contains a x86 PC tool to bruteforce the key.  

The old payload which bruteforces the key on the Alarmo itself can be found [here](./old/README.md).

## Usage
- Update the `FIRMWARE_VERSION` define in the `main.c` to match the software version the Alarmo is on.
- Run `make` to compile the payload and the PC tool.
- Boot the Alarmo normally and wait until you can see the clock screen.
- Connect to the debug interface using openocd and run the `halt` command.
- Run `load_image payload.elf` to load the payload into memory.
- Run `resume 0x20000000` to execute the payload. The necessary data will now be stored to memory.  
  Once the payload is done a breakpoint will be triggered.  
- Run `dump_image aes_data.bin 0x24000000 0x50` to dump the data to a file.
- Run `./bruteforcer aes_data.bin` to start bruteforcing the key. This will take a few minutes.
