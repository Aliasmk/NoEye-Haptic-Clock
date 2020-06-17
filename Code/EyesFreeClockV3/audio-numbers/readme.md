# Audio Source Files for HapticEye

This library contains all the original and converted audio files used in the project. The wav files are as-downloaded from [here](https://evolution.voxeo.com/library/). To create the converted files, I tightly trimmed the wav files in Audacity and exported them as raw headerless 8-bit unsigned PCM files (note that the "set" file was created by clipping and splicing other clips). I then went through each file and chopped off or extended it with 0x80 so that the file length was a multiple of 256 (the EEPROM writing had issues crossing page boundaries, and I haven't implemented a fix for that in my driver yet). I then renamed them alphabetically in the order I wanted them flashed, recorded their lengths into an excel spreadsheet, and ran a batch file to combine them into one file. 

To flash them to HapticEye, connect the TX and RX pins to an Arduino or other UART to USB converted. Connect with 19200 baud **and set the encoding to CP 437**. Power on HapticEye with the set and mode buttons pressed to enter the memory loader program. Open the combined file **with CP 437 encoding** in an editor such as Sublime, and copy the contents. Enter the size of the combined file, and the start address (such as 0) then paste the data into the serial terminal and wait for it to download.

The audio clips are enumerated and stored with their start addresses in audioclip.hpp. 