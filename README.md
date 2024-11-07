# Simple Bootloader

This project is a minimal bootloader written in x86 assembly language. A bootloader is a small program that runs when a computer starts and loads the operating system. This particular bootloader doesn't load an OS but serves as a fundamental example, containing just enough code to be recognized as bootable by the BIOS.

## Features

- Contains an infinite loop to halt execution, serving as a placeholder for additional boot code.
- Pads the code to 510 bytes, allowing space for the boot signature.
- Adds the `0x55AA` boot signature, which is required for the BIOS to recognize a bootable sector.

## Requirements

- **NASM** (Netwide Assembler) - Used to assemble the `.asm` file into a binary.
- **QEMU** - A virtual machine emulator used to run and test the bootloader binary.

## File Structure

- `boot.asm`: The assembly source code for the bootloader.
- `boot.bin`: The binary file generated after assembling `boot.asm`, which will be used for booting.

## How It Works

This bootloader is designed to demonstrate the minimum requirements for a bootable sector:
1. **Jump Instruction**: The `jmp $` instruction creates an infinite loop, which halts further execution.
2. **Padding**: The code uses padding to ensure it reaches exactly 510 bytes, leaving the last 2 bytes for the boot signature.
3. **Boot Signature**: The `0x55AA` signature is added as the final two bytes of the sector, marking it as a bootable sector for the BIOS.

## Usage Instructions

Follow these steps to assemble and test the bootloader using NASM and QEMU.

### Step 1: Create the Bootloader Code

Save the following code as `boot.asm`:

```asm
jmp $                       ; Infinite loop to halt execution

times 510 - ($ - $$) db 0   ; Pad to 510 bytes with zeros
db 0x55, 0xaa               ; Boot signature required by the BIOS
 Step 2: Assemble the Bootloader
Run the following command in your terminal to assemble the code into a binary file:


nasm -f bin -o boot.bin boot.asm
This command produces a 512-byte binary file called boot.bin from boot.asm.

Step 3: Run the Bootloader with QEMU
To test the bootloader, run it in a virtual machine using QEMU. This command will load boot.bin as a bootable image:


qemu-system-x86_64 -drive format=raw,file=boot.bin
qemu-system-x86_64: Launches QEMU for a 64-bit system. You can also use qemu-system-i386 for 32-bit mode.
-drive format=raw,file=boot.bin: Tells QEMU to treat boot.bin as a raw disk image.
QEMU will start and attempt to boot from boot.bin. Since the code contains an infinite loop (jmp $), the virtual machine will appear to "hang" after booting, which indicates that the bootloader is running correctly. You can exit QEMU by closing the window or pressing Ctrl + C in the terminal.

License
This project is licensed under the MIT License. See the LICENSE file for details.


---

This README file includes all the steps for creating, assembling, and testing the bootloader, alon
