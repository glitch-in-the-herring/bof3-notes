The equipability byte determines who can use a piece of equipment. It is a bit switch:

| Bit    | User  |
| ------ | ----- |
| `0x01` | Ryu   |
| `0x02` | Nina  |
| `0x04` | Garr  |
| `0x08` | Teepo |
| `0x10` | Rei   |
| `0x20` | Momo  |
| `0x40` | Peco  |
| `0x80` | Whelp |
For example, a weapon that only Ryu and Teepo can use is indicated by `0x09`.