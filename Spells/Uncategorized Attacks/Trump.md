| 8Spell ID         | Targeting        | Power | AP  | Element | Battle Spell Call |
| ----------------- | ---------------- | ----- | --- | ------- | ----------------- |
| `0x8c`<br>140<br> | `0xe`*<br>Self\* | 0<br> | 0   | None    | `0x80`            |
|                   |                  |       |     |         |                   |

\* actual targeting depends on the randomly selected spell
Trump is identical to [[MagicShuffle]], but it is only usable when the caster's AP is exactly 0. This is controlled by the following if-else branch that is executed when printing the spell list:
```
801af768 li     $v0, 0x008c ; the currently printed spell is Trump
```
This can be found at the following location:
```
BIN/ETC/GAME.EMI: 0001a784
```