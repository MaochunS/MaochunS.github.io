# Blockchain related
CommandName | MCU/SE | CommandID | P1 | P2 | Data Length | Data | Response length | Response 
--| --| --| --| --| --| --| --| --|
Transaction prepare | 0x80 | 0xB8 | Transaction Input Index (Bitcoin) | 0x00 | 0x54 0x00 | Path 20-Byte, Balance 32-Byte (not in use, set to 0), Hash 32-Byte. (Indput data) | N/A
Transaction prepare new | 0x70 | 0xA0 | Transaction Input Index | 0x00 | Dynamic | Token 4-Byte 1 or 0, Path 20-Byte, hex raw data | N/A
Transaction prepare generic (use this one) | 0x70 | 0xA1 | input index (defulat 0x00) | 0x00 (SECP256K1) or 0x01 (ED2519) | Dynamic | Path 20 or 12 bytes, Balance 32-Byte (not in use, set to 0), Hash 32-byte | N/A
Transaction begin | 0x80 | 0x72 | 0(show confirmation) or 1(don't show) | 0x00 | 80 | amount: 32-byte, output address: 48-byte | 0x06 0x00 |  Not in use
Transaction sign | 0x80 | 0x74 | Transaction Input Index | 0x00 | 0x00 | N/A | 65-Byte | Signature
Transaction finish | 0x80 | 0x76 | 0x00 | 0x00 | 0x00 |0x00 | 0x00 | 0x00 | 0x00
Get public key | 0x80 | 0xC0 | 0x00 | 0x00 | Path length | Path (4, 8, 12, 16, 20) | 100 byte | key: 64-byte, chainCode: 32-byte, fingerPrint: 4-byte
Get public key generic (use this one) | 0x80 | 0xC1 | 0x00 (SECP256K1) or 0x01 (ED2519) | 0x00 | path length | Path (4, 8, 12, 16, 20) | SECP256K1 64-byte, ED2519: 32-byte

# Device releated

CommandName | MCU/SE | CommandID | P1 | P2 | Data Length | Data | Response length | Response 
--| --| --| --| --| --| --| --| --|
Back to init state | 0x70 | 0x11 | ...
Back to preloader | 0x80 | 0x78 | ...
Check update SE | 0x70 | 0x60 | 0x00 | 0x00 | 68 | anthmthrl: string (32-byte), encsmk: string (32-byte), blockTotal: number (4-byte) | N/A
Update SE | 0x70 | 0x61 | 0x00 | 0x00 | Dynamic | data, mac, block ID (4-byte) | N/A
Get FW Version | 0x80 | 0x11 | 0x00 | 0x00 | 0x00 | N/A | 32 | SE: 16-byte (6,7,8,9), MCU: 16-byte (6,7,8,9)
ModulaError | 0x80 | 0x13 | 0x00 | 0x00 | N/A | 6 | 
SE Mode & status | 0x80 | 0x10 | 0x00 | 0x00 | N/A | 2 | mode: 1-byte (7 is ready), status: 1-byte
Get Version | 0x70 | 0x13 | 0x00 | 0x00 | 0x00 | N/A | dynamic | Version total len: 1-byte, transport(len, data) , SE version(len, data), MCU(len, data), bootloader(len, data) 
Init device info. | 0x70 | 0x12 | N/A
Jump to cos. | 0x60 | 0x01 | N/A 
MCU back to preloader | 0x70 | 0x80 | N/A

# MCU releated
CommandName | MCU/SE | CommandID | P1 | P2 | Data Length | Data | Response length | Response 
--| --| --| --| --| --| --| --| --|
Address from device (for receive) | 0x70 | 0x86 | 0(uncompress) or 1(normal compressed) | 0 (confirm) or 1 (no confirm) | 20 | path | N/A
Delete Account | 0x70 | 0x84 | 0x00 | 0x00 | 58/16 | isToken 4-byte, path: 12-byte, contractAddress(for token): 42-byte
Create/update Account | 0x70 | 0x82 | 0x00 | 0x00 |  | isToken: 4-byte, path: 12-byte, balance: 32-byte, name: 16-bye, contractAddress (for token): 42-byte, decimal size(for token): token decimal 1-byte 
Get all display (old) | 0x70 | 0x83 | N/A
Get account size | 0x70 | 0x87 | 
Get display account | 0x70 | 0x83 | 0x01 | 0x00 | 4 | index | N/A
Wallet info. | 0x80 | 0xB2 | 0: status (1-byte reply), 1: name (32-byte), 2: account pointer(4-byte), 3: ALL(37-byte)
Init wallet | 0x70 | 0x30 | 0x00 | 0x00 | 32 | name: 32-byte | N/A



# Reply
CommandName | len | data |
Get all reply | Dynamic | [Account (107-byte), isToken: 4-byte, Purpose 44/49 level: 4-byte, coin type: 4-byte, Acount level: 4-byte, Balance: 32-byte, Account Name: 16-byte, opt contractAddress: 42-byte, opt token decimal: 1-byte] 
Get account size | 4 | total account number






