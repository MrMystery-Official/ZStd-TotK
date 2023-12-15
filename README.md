# ZStd de/compressor for The Legend of Zelda: Tears of the Kingdom

A  C++ library to read and write files compressed with ZStd.
## Usage
First of all, include the `ZStdFile.h` header file. You have to create the required dictionaries, to do this, call the `Initialize` function and pass the path to the RomFS of TotK and add `/Pack/ZsDic.pack.zs` to it:
```cpp
#include "ZStdFile.h"

int main()
{
    ZStdFile::Initialize("C:/Path/to/dump/Pack/ZsDic.pack.zs");
    return 0;
}
```
To decompress a file, use the `Decompress` function. Then you can write it to a new file or get the bytes:
```cpp
#include "ZStdFile.h"

int main()
{
    ZStdFile::Initialize("C:/Path/to/dump/Pack/ZsDic.pack.zs");
    ZStdFile::Result Result = ZStdFile::Decompress("DgnObj_Small_CandlePoleC_04.pack.zs", ZStdFile::Dictionary::Pack);
    Result.WriteToFile("DgnObj_Small_CandlePoleC_04.pack"); //Decompressed file
    std::vector<unsigned char> Data = Result.Data; //Get the bytes of the decompressed file
    return 0;
}
```
To compress a file, call the `Compress` function.
```cpp
int main()
{
    ZStdFile::Initialize("C:/Path/to/dump/Pack/ZsDic.pack.zs");
    ZStdFile::Compress(DecompressedBytes, ZStdFile::Dictionary::Pack).WriteToFile("DgnObj_Small_CandlePoleC_04.pack.zs");
    return 0;
}
```
You can use the following dictionaries:
- None (hardly ever used)
- Pack (for archive files)
- BcettByaml (for all map files)
- Base (for everything else)
