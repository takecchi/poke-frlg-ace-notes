# FRLG Game Constants Reference (pret/pokefirered)

Source: pret/pokefirered decompilation (master branch)

## 目次

1. [Move IDs](#move-ids)
2. [Map IDs](#map-ids)
3. [Heal Location IDs](#heal-location-ids)

---

## Move IDs

`include/constants/moves.h` より。355技 (MOVE_NONE〜MOVE_PSYCHO_BOOST)。

書式: `MOVE_NAME = decimal (0xHex)`

```
MOVE_NONE            =   0 (0x000)
MOVE_POUND           =   1 (0x001)
MOVE_KARATE_CHOP     =   2 (0x002)
MOVE_DOUBLE_SLAP     =   3 (0x003)
MOVE_COMET_PUNCH     =   4 (0x004)
MOVE_MEGA_PUNCH      =   5 (0x005)
MOVE_PAY_DAY         =   6 (0x006)
MOVE_FIRE_PUNCH      =   7 (0x007)
MOVE_ICE_PUNCH       =   8 (0x008)
MOVE_THUNDER_PUNCH   =   9 (0x009)
MOVE_SCRATCH         =  10 (0x00A)
MOVE_VICE_GRIP       =  11 (0x00B)
MOVE_GUILLOTINE      =  12 (0x00C)
MOVE_RAZOR_WIND      =  13 (0x00D)
MOVE_SWORDS_DANCE    =  14 (0x00E)
MOVE_CUT             =  15 (0x00F)
MOVE_GUST            =  16 (0x010)
MOVE_WING_ATTACK     =  17 (0x011)
MOVE_WHIRLWIND       =  18 (0x012)
MOVE_FLY             =  19 (0x013)
MOVE_BIND            =  20 (0x014)
MOVE_SLAM            =  21 (0x015)
MOVE_VINE_WHIP       =  22 (0x016)
MOVE_STOMP           =  23 (0x017)
MOVE_DOUBLE_KICK     =  24 (0x018)
MOVE_MEGA_KICK       =  25 (0x019)
MOVE_JUMP_KICK       =  26 (0x01A)
MOVE_ROLLING_KICK    =  27 (0x01B)
MOVE_SAND_ATTACK     =  28 (0x01C)
MOVE_HEADBUTT        =  29 (0x01D)
MOVE_HORN_ATTACK     =  30 (0x01E)
MOVE_FURY_ATTACK     =  31 (0x01F)
MOVE_HORN_DRILL      =  32 (0x020)
MOVE_TACKLE          =  33 (0x021)
MOVE_BODY_SLAM       =  34 (0x022)
MOVE_WRAP            =  35 (0x023)
MOVE_TAKE_DOWN       =  36 (0x024)
MOVE_THRASH          =  37 (0x025)
MOVE_DOUBLE_EDGE     =  38 (0x026)
MOVE_TAIL_WHIP       =  39 (0x027)
MOVE_POISON_STING    =  40 (0x028)
MOVE_TWINEEDLE       =  41 (0x029)
MOVE_PIN_MISSILE     =  42 (0x02A)
MOVE_LEER            =  43 (0x02B)
MOVE_BITE            =  44 (0x02C)
MOVE_GROWL           =  45 (0x02D)
MOVE_ROAR            =  46 (0x02E)
MOVE_SING            =  47 (0x02F)
MOVE_SUPERSONIC      =  48 (0x030)
MOVE_SONIC_BOOM      =  49 (0x031)
MOVE_DISABLE         =  50 (0x032)
MOVE_ACID            =  51 (0x033)
MOVE_EMBER           =  52 (0x034)
MOVE_FLAMETHROWER    =  53 (0x035)
MOVE_MIST            =  54 (0x036)
MOVE_WATER_GUN       =  55 (0x037)
MOVE_HYDRO_PUMP      =  56 (0x038)
MOVE_SURF            =  57 (0x039)
MOVE_ICE_BEAM        =  58 (0x03A)
MOVE_BLIZZARD        =  59 (0x03B)
MOVE_PSYBEAM         =  60 (0x03C)
MOVE_BUBBLE_BEAM     =  61 (0x03D)
MOVE_AURORA_BEAM     =  62 (0x03E)
MOVE_HYPER_BEAM      =  63 (0x03F)
MOVE_PECK            =  64 (0x040)
MOVE_DRILL_PECK      =  65 (0x041)
MOVE_SUBMISSION      =  66 (0x042)
MOVE_LOW_KICK        =  67 (0x043)
MOVE_COUNTER         =  68 (0x044)
MOVE_SEISMIC_TOSS    =  69 (0x045)
MOVE_STRENGTH        =  70 (0x046)
MOVE_ABSORB          =  71 (0x047)
MOVE_MEGA_DRAIN      =  72 (0x048)
MOVE_LEECH_SEED      =  73 (0x049)
MOVE_GROWTH          =  74 (0x04A)
MOVE_RAZOR_LEAF      =  75 (0x04B)
MOVE_SOLAR_BEAM      =  76 (0x04C)
MOVE_POISON_POWDER   =  77 (0x04D)
MOVE_STUN_SPORE      =  78 (0x04E)
MOVE_SLEEP_POWDER    =  79 (0x04F)
MOVE_PETAL_DANCE     =  80 (0x050)
MOVE_STRING_SHOT     =  81 (0x051)
MOVE_DRAGON_RAGE     =  82 (0x052)
MOVE_FIRE_SPIN       =  83 (0x053)
MOVE_THUNDER_SHOCK   =  84 (0x054)
MOVE_THUNDERBOLT     =  85 (0x055)
MOVE_THUNDER_WAVE    =  86 (0x056)
MOVE_THUNDER         =  87 (0x057)
MOVE_ROCK_THROW      =  88 (0x058)
MOVE_EARTHQUAKE      =  89 (0x059)
MOVE_FISSURE         =  90 (0x05A)
MOVE_DIG             =  91 (0x05B)
MOVE_TOXIC           =  92 (0x05C)
MOVE_CONFUSION       =  93 (0x05D)
MOVE_PSYCHIC         =  94 (0x05E)
MOVE_HYPNOSIS        =  95 (0x05F)
MOVE_MEDITATE        =  96 (0x060)
MOVE_AGILITY         =  97 (0x061)
MOVE_QUICK_ATTACK    =  98 (0x062)
MOVE_RAGE            =  99 (0x063)
MOVE_TELEPORT        = 100 (0x064)
MOVE_NIGHT_SHADE     = 101 (0x065)
MOVE_MIMIC           = 102 (0x066)
MOVE_SCREECH         = 103 (0x067)
MOVE_DOUBLE_TEAM     = 104 (0x068)
MOVE_RECOVER         = 105 (0x069)
MOVE_HARDEN          = 106 (0x06A)
MOVE_MINIMIZE        = 107 (0x06B)
MOVE_SMOKESCREEN     = 108 (0x06C)
MOVE_CONFUSE_RAY     = 109 (0x06D)
MOVE_WITHDRAW        = 110 (0x06E)
MOVE_DEFENSE_CURL    = 111 (0x06F)
MOVE_BARRIER         = 112 (0x070)
MOVE_LIGHT_SCREEN    = 113 (0x071)
MOVE_HAZE            = 114 (0x072)
MOVE_REFLECT         = 115 (0x073)
MOVE_FOCUS_ENERGY    = 116 (0x074)
MOVE_BIDE            = 117 (0x075)
MOVE_METRONOME       = 118 (0x076)
MOVE_MIRROR_MOVE     = 119 (0x077)
MOVE_SELF_DESTRUCT   = 120 (0x078)
MOVE_EGG_BOMB        = 121 (0x079)
MOVE_LICK            = 122 (0x07A)
MOVE_SMOG            = 123 (0x07B)
MOVE_SLUDGE          = 124 (0x07C)
MOVE_BONE_CLUB       = 125 (0x07D)
MOVE_FIRE_BLAST      = 126 (0x07E)
MOVE_WATERFALL       = 127 (0x07F)
MOVE_CLAMP           = 128 (0x080)
MOVE_SWIFT           = 129 (0x081)
MOVE_SKULL_BASH      = 130 (0x082)
MOVE_SPIKE_CANNON    = 131 (0x083)
MOVE_CONSTRICT       = 132 (0x084)
MOVE_AMNESIA         = 133 (0x085)
MOVE_KINESIS         = 134 (0x086)
MOVE_SOFT_BOILED     = 135 (0x087)
MOVE_HI_JUMP_KICK    = 136 (0x088)
MOVE_GLARE           = 137 (0x089)
MOVE_DREAM_EATER     = 138 (0x08A)
MOVE_POISON_GAS      = 139 (0x08B)
MOVE_BARRAGE         = 140 (0x08C)
MOVE_LEECH_LIFE      = 141 (0x08D)
MOVE_LOVELY_KISS     = 142 (0x08E)
MOVE_SKY_ATTACK      = 143 (0x08F)
MOVE_TRANSFORM       = 144 (0x090)
MOVE_BUBBLE          = 145 (0x091)
MOVE_DIZZY_PUNCH     = 146 (0x092)
MOVE_SPORE           = 147 (0x093)
MOVE_FLASH           = 148 (0x094)
MOVE_PSYWAVE         = 149 (0x095)
MOVE_SPLASH          = 150 (0x096)
MOVE_ACID_ARMOR      = 151 (0x097)
MOVE_CRABHAMMER      = 152 (0x098)
MOVE_EXPLOSION       = 153 (0x099)
MOVE_FURY_SWIPES     = 154 (0x09A)
MOVE_BONEMERANG      = 155 (0x09B)
MOVE_REST            = 156 (0x09C)
MOVE_ROCK_SLIDE      = 157 (0x09D)
MOVE_HYPER_FANG      = 158 (0x09E)
MOVE_SHARPEN         = 159 (0x09F)
MOVE_CONVERSION      = 160 (0x0A0)
MOVE_TRI_ATTACK      = 161 (0x0A1)
MOVE_SUPER_FANG      = 162 (0x0A2)
MOVE_SLASH           = 163 (0x0A3)
MOVE_SUBSTITUTE      = 164 (0x0A4)
MOVE_STRUGGLE        = 165 (0x0A5)
MOVE_SKETCH          = 166 (0x0A6)
MOVE_TRIPLE_KICK     = 167 (0x0A7)
MOVE_THIEF           = 168 (0x0A8)
MOVE_SPIDER_WEB      = 169 (0x0A9)
MOVE_MIND_READER     = 170 (0x0AA)
MOVE_NIGHTMARE       = 171 (0x0AB)
MOVE_FLAME_WHEEL     = 172 (0x0AC)
MOVE_SNORE           = 173 (0x0AD)
MOVE_CURSE           = 174 (0x0AE)
MOVE_FLAIL           = 175 (0x0AF)
MOVE_CONVERSION_2    = 176 (0x0B0)
MOVE_AEROBLAST       = 177 (0x0B1)
MOVE_COTTON_SPORE    = 178 (0x0B2)
MOVE_REVERSAL        = 179 (0x0B3)
MOVE_SPITE           = 180 (0x0B4)
MOVE_POWDER_SNOW     = 181 (0x0B5)
MOVE_PROTECT         = 182 (0x0B6)
MOVE_MACH_PUNCH      = 183 (0x0B7)
MOVE_SCARY_FACE      = 184 (0x0B8)
MOVE_FAINT_ATTACK    = 185 (0x0B9)
MOVE_SWEET_KISS      = 186 (0x0BA)
MOVE_BELLY_DRUM      = 187 (0x0BB)
MOVE_SLUDGE_BOMB     = 188 (0x0BC)
MOVE_MUD_SLAP        = 189 (0x0BD)
MOVE_OCTAZOOKA       = 190 (0x0BE)
MOVE_SPIKES          = 191 (0x0BF)
MOVE_ZAP_CANNON      = 192 (0x0C0)
MOVE_FORESIGHT       = 193 (0x0C1)
MOVE_DESTINY_BOND    = 194 (0x0C2)
MOVE_PERISH_SONG     = 195 (0x0C3)
MOVE_ICY_WIND        = 196 (0x0C4)
MOVE_DETECT          = 197 (0x0C5)
MOVE_BONE_RUSH       = 198 (0x0C6)
MOVE_LOCK_ON         = 199 (0x0C7)
MOVE_OUTRAGE         = 200 (0x0C8)
MOVE_SANDSTORM       = 201 (0x0C9)
MOVE_GIGA_DRAIN      = 202 (0x0CA)
MOVE_ENDURE          = 203 (0x0CB)
MOVE_CHARM           = 204 (0x0CC)
MOVE_ROLLOUT         = 205 (0x0CD)
MOVE_FALSE_SWIPE     = 206 (0x0CE)
MOVE_SWAGGER         = 207 (0x0CF)
MOVE_MILK_DRINK      = 208 (0x0D0)
MOVE_SPARK           = 209 (0x0D1)
MOVE_FURY_CUTTER     = 210 (0x0D2)
MOVE_STEEL_WING      = 211 (0x0D3)
MOVE_MEAN_LOOK       = 212 (0x0D4)
MOVE_ATTRACT         = 213 (0x0D5)
MOVE_SLEEP_TALK      = 214 (0x0D6)
MOVE_HEAL_BELL       = 215 (0x0D7)
MOVE_RETURN          = 216 (0x0D8)
MOVE_PRESENT         = 217 (0x0D9)
MOVE_FRUSTRATION     = 218 (0x0DA)
MOVE_SAFEGUARD       = 219 (0x0DB)
MOVE_PAIN_SPLIT      = 220 (0x0DC)
MOVE_SACRED_FIRE     = 221 (0x0DD)
MOVE_MAGNITUDE       = 222 (0x0DE)
MOVE_DYNAMIC_PUNCH   = 223 (0x0DF)
MOVE_MEGAHORN        = 224 (0x0E0)
MOVE_DRAGON_BREATH   = 225 (0x0E1)
MOVE_BATON_PASS      = 226 (0x0E2)
MOVE_ENCORE          = 227 (0x0E3)
MOVE_PURSUIT         = 228 (0x0E4)
MOVE_RAPID_SPIN      = 229 (0x0E5)
MOVE_SWEET_SCENT     = 230 (0x0E6)
MOVE_IRON_TAIL       = 231 (0x0E7)
MOVE_METAL_CLAW      = 232 (0x0E8)
MOVE_VITAL_THROW     = 233 (0x0E9)
MOVE_MORNING_SUN     = 234 (0x0EA)
MOVE_SYNTHESIS       = 235 (0x0EB)
MOVE_MOONLIGHT       = 236 (0x0EC)
MOVE_HIDDEN_POWER    = 237 (0x0ED)
MOVE_CROSS_CHOP      = 238 (0x0EE)
MOVE_TWISTER         = 239 (0x0EF)
MOVE_RAIN_DANCE      = 240 (0x0F0)
MOVE_SUNNY_DAY       = 241 (0x0F1)
MOVE_CRUNCH          = 242 (0x0F2)
MOVE_MIRROR_COAT     = 243 (0x0F3)
MOVE_PSYCH_UP        = 244 (0x0F4)
MOVE_EXTREME_SPEED   = 245 (0x0F5)
MOVE_ANCIENT_POWER   = 246 (0x0F6)
MOVE_SHADOW_BALL     = 247 (0x0F7)
MOVE_FUTURE_SIGHT    = 248 (0x0F8)
MOVE_ROCK_SMASH      = 249 (0x0F9)
MOVE_WHIRLPOOL       = 250 (0x0FA)
MOVE_BEAT_UP         = 251 (0x0FB)
MOVE_FAKE_OUT        = 252 (0x0FC)
MOVE_UPROAR          = 253 (0x0FD)
MOVE_STOCKPILE       = 254 (0x0FE)
MOVE_SPIT_UP         = 255 (0x0FF)
MOVE_SWALLOW         = 256 (0x100)
MOVE_HEAT_WAVE       = 257 (0x101)
MOVE_HAIL            = 258 (0x102)
MOVE_TORMENT         = 259 (0x103)
MOVE_FLATTER         = 260 (0x104)
MOVE_WILL_O_WISP     = 261 (0x105)
MOVE_MEMENTO         = 262 (0x106)
MOVE_FACADE          = 263 (0x107)
MOVE_FOCUS_PUNCH     = 264 (0x108)
MOVE_SMELLING_SALT   = 265 (0x109)
MOVE_FOLLOW_ME       = 266 (0x10A)
MOVE_NATURE_POWER    = 267 (0x10B)
MOVE_CHARGE          = 268 (0x10C)
MOVE_TAUNT           = 269 (0x10D)
MOVE_HELPING_HAND    = 270 (0x10E)
MOVE_TRICK           = 271 (0x10F)
MOVE_ROLE_PLAY       = 272 (0x110)
MOVE_WISH            = 273 (0x111)
MOVE_ASSIST          = 274 (0x112)
MOVE_INGRAIN         = 275 (0x113)
MOVE_SUPERPOWER      = 276 (0x114)
MOVE_MAGIC_COAT      = 277 (0x115)
MOVE_RECYCLE         = 278 (0x116)
MOVE_REVENGE         = 279 (0x117)
MOVE_BRICK_BREAK     = 280 (0x118)
MOVE_YAWN            = 281 (0x119)
MOVE_KNOCK_OFF       = 282 (0x11A)
MOVE_ENDEAVOR        = 283 (0x11B)
MOVE_ERUPTION        = 284 (0x11C)
MOVE_SKILL_SWAP      = 285 (0x11D)
MOVE_IMPRISON        = 286 (0x11E)
MOVE_REFRESH         = 287 (0x11F)
MOVE_GRUDGE          = 288 (0x120)
MOVE_SNATCH          = 289 (0x121)
MOVE_SECRET_POWER    = 290 (0x122)
MOVE_DIVE            = 291 (0x123)
MOVE_ARM_THRUST      = 292 (0x124)
MOVE_CAMOUFLAGE      = 293 (0x125)
MOVE_TAIL_GLOW       = 294 (0x126)
MOVE_LUSTER_PURGE    = 295 (0x127)
MOVE_MIST_BALL       = 296 (0x128)
MOVE_FEATHER_DANCE   = 297 (0x129)
MOVE_TEETER_DANCE    = 298 (0x12A)
MOVE_BLAZE_KICK      = 299 (0x12B)
MOVE_MUD_SPORT       = 300 (0x12C)
MOVE_ICE_BALL        = 301 (0x12D)
MOVE_NEEDLE_ARM      = 302 (0x12E)
MOVE_SLACK_OFF       = 303 (0x12F)
MOVE_HYPER_VOICE     = 304 (0x130)
MOVE_POISON_FANG     = 305 (0x131)
MOVE_CRUSH_CLAW      = 306 (0x132)
MOVE_BLAST_BURN      = 307 (0x133)
MOVE_HYDRO_CANNON    = 308 (0x134)
MOVE_METEOR_MASH     = 309 (0x135)
MOVE_ASTONISH        = 310 (0x136)
MOVE_WEATHER_BALL    = 311 (0x137)
MOVE_AROMATHERAPY    = 312 (0x138)
MOVE_FAKE_TEARS      = 313 (0x139)
MOVE_AIR_CUTTER      = 314 (0x13A)
MOVE_OVERHEAT        = 315 (0x13B)
MOVE_ODOR_SLEUTH     = 316 (0x13C)
MOVE_ROCK_TOMB       = 317 (0x13D)
MOVE_SILVER_WIND     = 318 (0x13E)
MOVE_METAL_SOUND     = 319 (0x13F)
MOVE_GRASS_WHISTLE   = 320 (0x140)
MOVE_TICKLE          = 321 (0x141)
MOVE_COSMIC_POWER    = 322 (0x142)
MOVE_WATER_SPOUT     = 323 (0x143)
MOVE_SIGNAL_BEAM     = 324 (0x144)
MOVE_SHADOW_PUNCH    = 325 (0x145)
MOVE_EXTRASENSORY    = 326 (0x146)
MOVE_SKY_UPPERCUT    = 327 (0x147)
MOVE_SAND_TOMB       = 328 (0x148)
MOVE_SHEER_COLD      = 329 (0x149)
MOVE_MUDDY_WATER     = 330 (0x14A)
MOVE_BULLET_SEED     = 331 (0x14B)
MOVE_AERIAL_ACE      = 332 (0x14C)
MOVE_ICICLE_SPEAR    = 333 (0x14D)
MOVE_IRON_DEFENSE    = 334 (0x14E)
MOVE_BLOCK           = 335 (0x14F)
MOVE_HOWL            = 336 (0x150)
MOVE_DRAGON_CLAW     = 337 (0x151)
MOVE_FRENZY_PLANT    = 338 (0x152)
MOVE_BULK_UP         = 339 (0x153)
MOVE_BOUNCE          = 340 (0x154)
MOVE_MUD_SHOT        = 341 (0x155)
MOVE_POISON_TAIL     = 342 (0x156)
MOVE_COVET           = 343 (0x157)
MOVE_VOLT_TACKLE     = 344 (0x158)
MOVE_MAGICAL_LEAF    = 345 (0x159)
MOVE_WATER_SPORT     = 346 (0x15A)
MOVE_CALM_MIND       = 347 (0x15B)
MOVE_LEAF_BLADE      = 348 (0x15C)
MOVE_DRAGON_DANCE    = 349 (0x15D)
MOVE_ROCK_BLAST      = 350 (0x15E)
MOVE_SHOCK_WAVE      = 351 (0x15F)
MOVE_WATER_PULSE     = 352 (0x160)
MOVE_DOOM_DESIRE     = 353 (0x161)
MOVE_PSYCHO_BOOST    = 354 (0x162)

MOVES_COUNT          = 355 (0x163)
MOVE_UNAVAILABLE     = 65535 (0xFFFF)
```

### Move Tutor IDs (MOVETUTOR_*)

```
MOVETUTOR_MEGA_PUNCH       =  0
MOVETUTOR_FIRE_PUNCH       =  1
MOVETUTOR_ICE_PUNCH        =  2
MOVETUTOR_THUNDER_PUNCH    =  3
MOVETUTOR_MEGA_KICK        =  4
MOVETUTOR_BODY_SLAM        =  5
MOVETUTOR_ROCK_SLIDE       =  6
MOVETUTOR_COUNTER          =  7
MOVETUTOR_SEISMIC_TOSS     =  8
MOVETUTOR_MIMIC            =  9
MOVETUTOR_DREAM_EATER      = 10
MOVETUTOR_THUNDER_WAVE     = 11
MOVETUTOR_EXPLOSION        = 12
MOVETUTOR_SOFT_BOILED      = 13
MOVETUTOR_SWORDS_DANCE     = 14
MOVETUTOR_SUBSTITUTE       = 15
MOVETUTOR_FRENZY_PLANT     = 16  (FR only)
MOVETUTOR_BLAST_BURN       = 17  (FR only, actually index 16 in LG)
MOVETUTOR_HYDRO_CANNON     = 17  (last index)
```

---

## Map IDs

`data/maps/map_groups.json` より。

### エンコード方式

```
MAP_GROUP(map) = map >> 8        // 上位バイト = グループ番号
MAP_NUM(map)   = map & 0xFF      // 下位バイト = グループ内番号
```

warpコマンドでの指定: `MAP_GROUP:MAP_NUM` (両方0始まり)

書式: `MAP_NAME = group:num (0xGG:0xNN)`

### Group 0: gMapGroup_Link

```
MAP_BATTLE_COLOSSEUM_2P     = 0:0 (0x00:0x00)
MAP_TRADE_CENTER            = 0:1 (0x00:0x01)
MAP_RECORD_CORNER           = 0:2 (0x00:0x02)
MAP_BATTLE_COLOSSEUM_4P     = 0:3 (0x00:0x03)
MAP_UNION_ROOM              = 0:4 (0x00:0x04)
```

### Group 1: gMapGroup_Dungeons

```
MAP_VIRIDIAN_FOREST                         = 1:0  (0x01:0x00)
MAP_MT_MOON_1F                              = 1:1  (0x01:0x01)
MAP_MT_MOON_B1F                             = 1:2  (0x01:0x02)
MAP_MT_MOON_B2F                             = 1:3  (0x01:0x03)
MAP_SS_ANNE_EXTERIOR                        = 1:4  (0x01:0x04)
MAP_SS_ANNE_1F_CORRIDOR                     = 1:5  (0x01:0x05)
MAP_SS_ANNE_2F_CORRIDOR                     = 1:6  (0x01:0x06)
MAP_SS_ANNE_3F_CORRIDOR                     = 1:7  (0x01:0x07)
MAP_SS_ANNE_B1F_CORRIDOR                    = 1:8  (0x01:0x08)
MAP_SS_ANNE_DECK                            = 1:9  (0x01:0x09)
MAP_SS_ANNE_KITCHEN                         = 1:10 (0x01:0x0A)
MAP_SS_ANNE_CAPTAINS_OFFICE                 = 1:11 (0x01:0x0B)
MAP_SS_ANNE_1F_ROOM1                        = 1:12 (0x01:0x0C)
MAP_SS_ANNE_1F_ROOM2                        = 1:13 (0x01:0x0D)
MAP_SS_ANNE_1F_ROOM3                        = 1:14 (0x01:0x0E)
MAP_SS_ANNE_1F_ROOM4                        = 1:15 (0x01:0x0F)
MAP_SS_ANNE_1F_ROOM5                        = 1:16 (0x01:0x10)
MAP_SS_ANNE_1F_ROOM7                        = 1:17 (0x01:0x11)
MAP_SS_ANNE_2F_ROOM1                        = 1:18 (0x01:0x12)
MAP_SS_ANNE_2F_ROOM2                        = 1:19 (0x01:0x13)
MAP_SS_ANNE_2F_ROOM3                        = 1:20 (0x01:0x14)
MAP_SS_ANNE_2F_ROOM4                        = 1:21 (0x01:0x15)
MAP_SS_ANNE_2F_ROOM5                        = 1:22 (0x01:0x16)
MAP_SS_ANNE_2F_ROOM6                        = 1:23 (0x01:0x17)
MAP_SS_ANNE_B1F_ROOM1                       = 1:24 (0x01:0x18)
MAP_SS_ANNE_B1F_ROOM2                       = 1:25 (0x01:0x19)
MAP_SS_ANNE_B1F_ROOM3                       = 1:26 (0x01:0x1A)
MAP_SS_ANNE_B1F_ROOM4                       = 1:27 (0x01:0x1B)
MAP_SS_ANNE_B1F_ROOM5                       = 1:28 (0x01:0x1C)
MAP_SS_ANNE_1F_ROOM6                        = 1:29 (0x01:0x1D)
MAP_UNDERGROUND_PATH_NORTH_ENTRANCE         = 1:30 (0x01:0x1E)
MAP_UNDERGROUND_PATH_NORTH_SOUTH_TUNNEL     = 1:31 (0x01:0x1F)
MAP_UNDERGROUND_PATH_SOUTH_ENTRANCE         = 1:32 (0x01:0x20)
MAP_UNDERGROUND_PATH_WEST_ENTRANCE          = 1:33 (0x01:0x21)
MAP_UNDERGROUND_PATH_EAST_WEST_TUNNEL       = 1:34 (0x01:0x22)
MAP_UNDERGROUND_PATH_EAST_ENTRANCE          = 1:35 (0x01:0x23)
MAP_DIGLETTS_CAVE_NORTH_ENTRANCE            = 1:36 (0x01:0x24)
MAP_DIGLETTS_CAVE_B1F                       = 1:37 (0x01:0x25)
MAP_DIGLETTS_CAVE_SOUTH_ENTRANCE            = 1:38 (0x01:0x26)
MAP_VICTORY_ROAD_1F                         = 1:39 (0x01:0x27)
MAP_VICTORY_ROAD_2F                         = 1:40 (0x01:0x28)
MAP_VICTORY_ROAD_3F                         = 1:41 (0x01:0x29)
MAP_ROCKET_HIDEOUT_B1F                      = 1:42 (0x01:0x2A)
MAP_ROCKET_HIDEOUT_B2F                      = 1:43 (0x01:0x2B)
MAP_ROCKET_HIDEOUT_B3F                      = 1:44 (0x01:0x2C)
MAP_ROCKET_HIDEOUT_B4F                      = 1:45 (0x01:0x2D)
MAP_ROCKET_HIDEOUT_ELEVATOR                 = 1:46 (0x01:0x2E)
MAP_SILPH_CO_1F                             = 1:47 (0x01:0x2F)
MAP_SILPH_CO_2F                             = 1:48 (0x01:0x30)
MAP_SILPH_CO_3F                             = 1:49 (0x01:0x31)
MAP_SILPH_CO_4F                             = 1:50 (0x01:0x32)
MAP_SILPH_CO_5F                             = 1:51 (0x01:0x33)
MAP_SILPH_CO_6F                             = 1:52 (0x01:0x34)
MAP_SILPH_CO_7F                             = 1:53 (0x01:0x35)
MAP_SILPH_CO_8F                             = 1:54 (0x01:0x36)
MAP_SILPH_CO_9F                             = 1:55 (0x01:0x37)
MAP_SILPH_CO_10F                            = 1:56 (0x01:0x38)
MAP_SILPH_CO_11F                            = 1:57 (0x01:0x39)
MAP_SILPH_CO_ELEVATOR                       = 1:58 (0x01:0x3A)
MAP_POKEMON_MANSION_1F                      = 1:59 (0x01:0x3B)
MAP_POKEMON_MANSION_2F                      = 1:60 (0x01:0x3C)
MAP_POKEMON_MANSION_3F                      = 1:61 (0x01:0x3D)
MAP_POKEMON_MANSION_B1F                     = 1:62 (0x01:0x3E)
MAP_SAFARI_ZONE_CENTER                      = 1:63 (0x01:0x3F)
MAP_SAFARI_ZONE_EAST                        = 1:64 (0x01:0x40)
MAP_SAFARI_ZONE_NORTH                       = 1:65 (0x01:0x41)
MAP_SAFARI_ZONE_WEST                        = 1:66 (0x01:0x42)
MAP_SAFARI_ZONE_CENTER_REST_HOUSE           = 1:67 (0x01:0x43)
MAP_SAFARI_ZONE_EAST_REST_HOUSE             = 1:68 (0x01:0x44)
MAP_SAFARI_ZONE_NORTH_REST_HOUSE            = 1:69 (0x01:0x45)
MAP_SAFARI_ZONE_WEST_REST_HOUSE             = 1:70 (0x01:0x46)
MAP_SAFARI_ZONE_SECRET_HOUSE                = 1:71 (0x01:0x47)
MAP_CERULEAN_CAVE_1F                        = 1:72 (0x01:0x48)
MAP_CERULEAN_CAVE_2F                        = 1:73 (0x01:0x49)
MAP_CERULEAN_CAVE_B1F                       = 1:74 (0x01:0x4A)
MAP_POKEMON_LEAGUE_LORELEIS_ROOM            = 1:75 (0x01:0x4B)
MAP_POKEMON_LEAGUE_BRUNOS_ROOM              = 1:76 (0x01:0x4C)
MAP_POKEMON_LEAGUE_AGATHAS_ROOM             = 1:77 (0x01:0x4D)
MAP_POKEMON_LEAGUE_LANCES_ROOM              = 1:78 (0x01:0x4E)
MAP_POKEMON_LEAGUE_CHAMPIONS_ROOM           = 1:79 (0x01:0x4F)
MAP_POKEMON_LEAGUE_HALL_OF_FAME             = 1:80 (0x01:0x50)
MAP_ROCK_TUNNEL_1F                          = 1:81 (0x01:0x51)
MAP_ROCK_TUNNEL_B1F                         = 1:82 (0x01:0x52)
MAP_SEAFOAM_ISLANDS_1F                      = 1:83 (0x01:0x53)
MAP_SEAFOAM_ISLANDS_B1F                     = 1:84 (0x01:0x54)
MAP_SEAFOAM_ISLANDS_B2F                     = 1:85 (0x01:0x55)
MAP_SEAFOAM_ISLANDS_B3F                     = 1:86 (0x01:0x56)
MAP_SEAFOAM_ISLANDS_B4F                     = 1:87 (0x01:0x57)
MAP_POKEMON_TOWER_1F                        = 1:88 (0x01:0x58)
MAP_POKEMON_TOWER_2F                        = 1:89 (0x01:0x59)
MAP_POKEMON_TOWER_3F                        = 1:90 (0x01:0x5A)
MAP_POKEMON_TOWER_4F                        = 1:91 (0x01:0x5B)
MAP_POKEMON_TOWER_5F                        = 1:92 (0x01:0x5C)
MAP_POKEMON_TOWER_6F                        = 1:93 (0x01:0x5D)
MAP_POKEMON_TOWER_7F                        = 1:94 (0x01:0x5E)
MAP_POWER_PLANT                             = 1:95 (0x01:0x5F)
MAP_MT_EMBER_RUBY_PATH_B4F                  = 1:96 (0x01:0x60)
MAP_MT_EMBER_EXTERIOR                       = 1:97 (0x01:0x61)
MAP_MT_EMBER_SUMMIT_PATH_1F                 = 1:98 (0x01:0x62)
MAP_MT_EMBER_SUMMIT_PATH_2F                 = 1:99 (0x01:0x63)
MAP_MT_EMBER_SUMMIT_PATH_3F                 = 1:100 (0x01:0x64)
MAP_MT_EMBER_SUMMIT                         = 1:101 (0x01:0x65)
MAP_MT_EMBER_RUBY_PATH_B5F                  = 1:102 (0x01:0x66)
MAP_MT_EMBER_RUBY_PATH_1F                   = 1:103 (0x01:0x67)
MAP_MT_EMBER_RUBY_PATH_B1F                  = 1:104 (0x01:0x68)
MAP_MT_EMBER_RUBY_PATH_B2F                  = 1:105 (0x01:0x69)
MAP_MT_EMBER_RUBY_PATH_B3F                  = 1:106 (0x01:0x6A)
MAP_MT_EMBER_RUBY_PATH_B1F_STAIRS           = 1:107 (0x01:0x6B)
MAP_MT_EMBER_RUBY_PATH_B2F_STAIRS           = 1:108 (0x01:0x6C)
MAP_THREE_ISLAND_BERRY_FOREST               = 1:109 (0x01:0x6D)
MAP_FOUR_ISLAND_ICEFALL_CAVE_ENTRANCE       = 1:110 (0x01:0x6E)
MAP_FOUR_ISLAND_ICEFALL_CAVE_1F             = 1:111 (0x01:0x6F)
MAP_FOUR_ISLAND_ICEFALL_CAVE_B1F            = 1:112 (0x01:0x70)
MAP_FOUR_ISLAND_ICEFALL_CAVE_BACK           = 1:113 (0x01:0x71)
MAP_FIVE_ISLAND_ROCKET_WAREHOUSE            = 1:114 (0x01:0x72)
MAP_SIX_ISLAND_DOTTED_HOLE_1F              = 1:115 (0x01:0x73)
MAP_SIX_ISLAND_DOTTED_HOLE_B1F             = 1:116 (0x01:0x74)
MAP_SIX_ISLAND_DOTTED_HOLE_B2F             = 1:117 (0x01:0x75)
MAP_SIX_ISLAND_DOTTED_HOLE_B3F             = 1:118 (0x01:0x76)
MAP_SIX_ISLAND_DOTTED_HOLE_B4F             = 1:119 (0x01:0x77)
MAP_SIX_ISLAND_DOTTED_HOLE_SAPPHIRE_ROOM   = 1:120 (0x01:0x78)
MAP_SIX_ISLAND_PATTERN_BUSH                = 1:121 (0x01:0x79)
MAP_SIX_ISLAND_ALTERING_CAVE               = 1:122 (0x01:0x7A)
```

### Group 2: gMapGroup_SpecialArea

```
MAP_NAVEL_ROCK_EXTERIOR                         = 2:0  (0x02:0x00)
MAP_TRAINER_TOWER_1F                            = 2:1  (0x02:0x01)
MAP_TRAINER_TOWER_2F                            = 2:2  (0x02:0x02)
MAP_TRAINER_TOWER_3F                            = 2:3  (0x02:0x03)
MAP_TRAINER_TOWER_4F                            = 2:4  (0x02:0x04)
MAP_TRAINER_TOWER_5F                            = 2:5  (0x02:0x05)
MAP_TRAINER_TOWER_6F                            = 2:6  (0x02:0x06)
MAP_TRAINER_TOWER_7F                            = 2:7  (0x02:0x07)
MAP_TRAINER_TOWER_8F                            = 2:8  (0x02:0x08)
MAP_TRAINER_TOWER_ROOF                          = 2:9  (0x02:0x09)
MAP_TRAINER_TOWER_LOBBY                         = 2:10 (0x02:0x0A)
MAP_TRAINER_TOWER_ELEVATOR                      = 2:11 (0x02:0x0B)
MAP_FIVE_ISLAND_LOST_CAVE_ENTRANCE              = 2:12 (0x02:0x0C)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM1                 = 2:13 (0x02:0x0D)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM2                 = 2:14 (0x02:0x0E)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM3                 = 2:15 (0x02:0x0F)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM4                 = 2:16 (0x02:0x10)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM5                 = 2:17 (0x02:0x11)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM6                 = 2:18 (0x02:0x12)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM7                 = 2:19 (0x02:0x13)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM8                 = 2:20 (0x02:0x14)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM9                 = 2:21 (0x02:0x15)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM10                = 2:22 (0x02:0x16)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM11                = 2:23 (0x02:0x17)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM12                = 2:24 (0x02:0x18)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM13                = 2:25 (0x02:0x19)
MAP_FIVE_ISLAND_LOST_CAVE_ROOM14                = 2:26 (0x02:0x1A)
MAP_SEVEN_ISLAND_TANOBY_RUINS_MONEAN_CHAMBER    = 2:27 (0x02:0x1B)
MAP_SEVEN_ISLAND_TANOBY_RUINS_LIPTOO_CHAMBER    = 2:28 (0x02:0x1C)
MAP_SEVEN_ISLAND_TANOBY_RUINS_WEEPTH_CHAMBER    = 2:29 (0x02:0x1D)
MAP_SEVEN_ISLAND_TANOBY_RUINS_DILFORD_CHAMBER   = 2:30 (0x02:0x1E)
MAP_SEVEN_ISLAND_TANOBY_RUINS_SCUFIB_CHAMBER    = 2:31 (0x02:0x1F)
MAP_SEVEN_ISLAND_TANOBY_RUINS_RIXY_CHAMBER      = 2:32 (0x02:0x20)
MAP_SEVEN_ISLAND_TANOBY_RUINS_VIAPOIS_CHAMBER   = 2:33 (0x02:0x21)
MAP_THREE_ISLAND_DUNSPARCE_TUNNEL               = 2:34 (0x02:0x22)
MAP_SEVEN_ISLAND_SEVAULT_CANYON_TANOBY_KEY      = 2:35 (0x02:0x23)
MAP_NAVEL_ROCK_1F                               = 2:36 (0x02:0x24)
MAP_NAVEL_ROCK_SUMMIT                           = 2:37 (0x02:0x25)
MAP_NAVEL_ROCK_BASE                             = 2:38 (0x02:0x26)
MAP_NAVEL_ROCK_SUMMIT_PATH_2F                   = 2:39 (0x02:0x27)
MAP_NAVEL_ROCK_SUMMIT_PATH_3F                   = 2:40 (0x02:0x28)
MAP_NAVEL_ROCK_SUMMIT_PATH_4F                   = 2:41 (0x02:0x29)
MAP_NAVEL_ROCK_SUMMIT_PATH_5F                   = 2:42 (0x02:0x2A)
MAP_NAVEL_ROCK_BASE_PATH_B1F                    = 2:43 (0x02:0x2B)
MAP_NAVEL_ROCK_BASE_PATH_B2F                    = 2:44 (0x02:0x2C)
MAP_NAVEL_ROCK_BASE_PATH_B3F                    = 2:45 (0x02:0x2D)
MAP_NAVEL_ROCK_BASE_PATH_B4F                    = 2:46 (0x02:0x2E)
MAP_NAVEL_ROCK_BASE_PATH_B5F                    = 2:47 (0x02:0x2F)
MAP_NAVEL_ROCK_BASE_PATH_B6F                    = 2:48 (0x02:0x30)
MAP_NAVEL_ROCK_BASE_PATH_B7F                    = 2:49 (0x02:0x31)
MAP_NAVEL_ROCK_BASE_PATH_B8F                    = 2:50 (0x02:0x32)
MAP_NAVEL_ROCK_BASE_PATH_B9F                    = 2:51 (0x02:0x33)
MAP_NAVEL_ROCK_BASE_PATH_B10F                   = 2:52 (0x02:0x34)
MAP_NAVEL_ROCK_BASE_PATH_B11F                   = 2:53 (0x02:0x35)
MAP_NAVEL_ROCK_B1F                              = 2:54 (0x02:0x36)
MAP_NAVEL_ROCK_FORK                             = 2:55 (0x02:0x37)
MAP_BIRTH_ISLAND_EXTERIOR                       = 2:56 (0x02:0x38)
MAP_ONE_ISLAND_KINDLE_ROAD_EMBER_SPA            = 2:57 (0x02:0x39)
MAP_BIRTH_ISLAND_HARBOR                         = 2:58 (0x02:0x3A)
MAP_NAVEL_ROCK_HARBOR                           = 2:59 (0x02:0x3B)
```

### Group 3: gMapGroup_TownsAndRoutes

```
MAP_PALLET_TOWN                             = 3:0  (0x03:0x00)
MAP_VIRIDIAN_CITY                           = 3:1  (0x03:0x01)
MAP_PEWTER_CITY                             = 3:2  (0x03:0x02)
MAP_CERULEAN_CITY                           = 3:3  (0x03:0x03)
MAP_LAVENDER_TOWN                           = 3:4  (0x03:0x04)
MAP_VERMILION_CITY                          = 3:5  (0x03:0x05)
MAP_CELADON_CITY                            = 3:6  (0x03:0x06)
MAP_FUCHSIA_CITY                            = 3:7  (0x03:0x07)
MAP_CINNABAR_ISLAND                         = 3:8  (0x03:0x08)
MAP_INDIGO_PLATEAU_EXTERIOR                 = 3:9  (0x03:0x09)
MAP_SAFFRON_CITY                            = 3:10 (0x03:0x0A)
MAP_SAFFRON_CITY_CONNECTION                 = 3:11 (0x03:0x0B)
MAP_ONE_ISLAND                              = 3:12 (0x03:0x0C)
MAP_TWO_ISLAND                              = 3:13 (0x03:0x0D)
MAP_THREE_ISLAND                            = 3:14 (0x03:0x0E)
MAP_FOUR_ISLAND                             = 3:15 (0x03:0x0F)
MAP_FIVE_ISLAND                             = 3:16 (0x03:0x10)
MAP_SEVEN_ISLAND                            = 3:17 (0x03:0x11)
MAP_SIX_ISLAND                              = 3:18 (0x03:0x12)
MAP_ROUTE1                                  = 3:19 (0x03:0x13)
MAP_ROUTE2                                  = 3:20 (0x03:0x14)
MAP_ROUTE3                                  = 3:21 (0x03:0x15)
MAP_ROUTE4                                  = 3:22 (0x03:0x16)
MAP_ROUTE5                                  = 3:23 (0x03:0x17)
MAP_ROUTE6                                  = 3:24 (0x03:0x18)
MAP_ROUTE7                                  = 3:25 (0x03:0x19)
MAP_ROUTE8                                  = 3:26 (0x03:0x1A)
MAP_ROUTE9                                  = 3:27 (0x03:0x1B)
MAP_ROUTE10                                 = 3:28 (0x03:0x1C)
MAP_ROUTE11                                 = 3:29 (0x03:0x1D)
MAP_ROUTE12                                 = 3:30 (0x03:0x1E)
MAP_ROUTE13                                 = 3:31 (0x03:0x1F)
MAP_ROUTE14                                 = 3:32 (0x03:0x20)
MAP_ROUTE15                                 = 3:33 (0x03:0x21)
MAP_ROUTE16                                 = 3:34 (0x03:0x22)
MAP_ROUTE17                                 = 3:35 (0x03:0x23)
MAP_ROUTE18                                 = 3:36 (0x03:0x24)
MAP_ROUTE19                                 = 3:37 (0x03:0x25)
MAP_ROUTE20                                 = 3:38 (0x03:0x26)
MAP_ROUTE21_NORTH                           = 3:39 (0x03:0x27)
MAP_ROUTE21_SOUTH                           = 3:40 (0x03:0x28)
MAP_ROUTE22                                 = 3:41 (0x03:0x29)
MAP_ROUTE23                                 = 3:42 (0x03:0x2A)
MAP_ROUTE24                                 = 3:43 (0x03:0x2B)
MAP_ROUTE25                                 = 3:44 (0x03:0x2C)
MAP_ONE_ISLAND_KINDLE_ROAD                  = 3:45 (0x03:0x2D)
MAP_ONE_ISLAND_TREASURE_BEACH               = 3:46 (0x03:0x2E)
MAP_TWO_ISLAND_CAPE_BRINK                   = 3:47 (0x03:0x2F)
MAP_THREE_ISLAND_BOND_BRIDGE                = 3:48 (0x03:0x30)
MAP_THREE_ISLAND_PORT                       = 3:49 (0x03:0x31)
MAP_PROTOTYPE_SEVII_ISLE_6                  = 3:50 (0x03:0x32)
MAP_PROTOTYPE_SEVII_ISLE_7                  = 3:51 (0x03:0x33)
MAP_PROTOTYPE_SEVII_ISLE_8                  = 3:52 (0x03:0x34)
MAP_PROTOTYPE_SEVII_ISLE_9                  = 3:53 (0x03:0x35)
MAP_FIVE_ISLAND_RESORT_GORGEOUS             = 3:54 (0x03:0x36)
MAP_FIVE_ISLAND_WATER_LABYRINTH             = 3:55 (0x03:0x37)
MAP_FIVE_ISLAND_MEADOW                      = 3:56 (0x03:0x38)
MAP_FIVE_ISLAND_MEMORIAL_PILLAR             = 3:57 (0x03:0x39)
MAP_SIX_ISLAND_OUTCAST_ISLAND               = 3:58 (0x03:0x3A)
MAP_SIX_ISLAND_GREEN_PATH                   = 3:59 (0x03:0x3B)
MAP_SIX_ISLAND_WATER_PATH                   = 3:60 (0x03:0x3C)
MAP_SIX_ISLAND_RUIN_VALLEY                  = 3:61 (0x03:0x3D)
MAP_SEVEN_ISLAND_TRAINER_TOWER              = 3:62 (0x03:0x3E)
MAP_SEVEN_ISLAND_SEVAULT_CANYON_ENTRANCE    = 3:63 (0x03:0x3F)
MAP_SEVEN_ISLAND_SEVAULT_CANYON             = 3:64 (0x03:0x40)
MAP_SEVEN_ISLAND_TANOBY_RUINS               = 3:65 (0x03:0x41)
```

### Group 4: gMapGroup_IndoorPallet

```
MAP_PALLET_TOWN_PLAYERS_HOUSE_1F    = 4:0 (0x04:0x00)
MAP_PALLET_TOWN_PLAYERS_HOUSE_2F    = 4:1 (0x04:0x01)
MAP_PALLET_TOWN_RIVALS_HOUSE        = 4:2 (0x04:0x02)
MAP_PALLET_TOWN_PROFESSOR_OAKS_LAB  = 4:3 (0x04:0x03)
```

### Group 5: gMapGroup_IndoorViridian

```
MAP_VIRIDIAN_CITY_HOUSE             = 5:0 (0x05:0x00)
MAP_VIRIDIAN_CITY_GYM               = 5:1 (0x05:0x01)
MAP_VIRIDIAN_CITY_SCHOOL            = 5:2 (0x05:0x02)
MAP_VIRIDIAN_CITY_MART              = 5:3 (0x05:0x03)
MAP_VIRIDIAN_CITY_POKEMON_CENTER_1F = 5:4 (0x05:0x04)
MAP_VIRIDIAN_CITY_POKEMON_CENTER_2F = 5:5 (0x05:0x05)
```

### Group 6: gMapGroup_IndoorPewter

```
MAP_PEWTER_CITY_MUSEUM_1F           = 6:0 (0x06:0x00)
MAP_PEWTER_CITY_MUSEUM_2F           = 6:1 (0x06:0x01)
MAP_PEWTER_CITY_GYM                 = 6:2 (0x06:0x02)
MAP_PEWTER_CITY_MART                = 6:3 (0x06:0x03)
MAP_PEWTER_CITY_HOUSE1              = 6:4 (0x06:0x04)
MAP_PEWTER_CITY_POKEMON_CENTER_1F   = 6:5 (0x06:0x05)
MAP_PEWTER_CITY_POKEMON_CENTER_2F   = 6:6 (0x06:0x06)
MAP_PEWTER_CITY_HOUSE2              = 6:7 (0x06:0x07)
```

### Group 7: gMapGroup_IndoorCerulean

```
MAP_CERULEAN_CITY_HOUSE1            = 7:0 (0x07:0x00)
MAP_CERULEAN_CITY_HOUSE2            = 7:1 (0x07:0x01)
MAP_CERULEAN_CITY_HOUSE3            = 7:2 (0x07:0x02)
MAP_CERULEAN_CITY_POKEMON_CENTER_1F = 7:3 (0x07:0x03)
MAP_CERULEAN_CITY_POKEMON_CENTER_2F = 7:4 (0x07:0x04)
MAP_CERULEAN_CITY_GYM               = 7:5 (0x07:0x05)
MAP_CERULEAN_CITY_BIKE_SHOP         = 7:6 (0x07:0x06)
MAP_CERULEAN_CITY_MART              = 7:7 (0x07:0x07)
MAP_CERULEAN_CITY_HOUSE4            = 7:8 (0x07:0x08)
MAP_CERULEAN_CITY_HOUSE5            = 7:9 (0x07:0x09)
```

### Group 8: gMapGroup_IndoorLavender

```
MAP_LAVENDER_TOWN_POKEMON_CENTER_1F     = 8:0 (0x08:0x00)
MAP_LAVENDER_TOWN_POKEMON_CENTER_2F     = 8:1 (0x08:0x01)
MAP_LAVENDER_TOWN_VOLUNTEER_POKEMON_HOUSE = 8:2 (0x08:0x02)
MAP_LAVENDER_TOWN_HOUSE1                = 8:3 (0x08:0x03)
MAP_LAVENDER_TOWN_HOUSE2                = 8:4 (0x08:0x04)
MAP_LAVENDER_TOWN_MART                  = 8:5 (0x08:0x05)
```

### Group 9: gMapGroup_IndoorVermilion

```
MAP_VERMILION_CITY_HOUSE1               = 9:0 (0x09:0x00)
MAP_VERMILION_CITY_POKEMON_CENTER_1F    = 9:1 (0x09:0x01)
MAP_VERMILION_CITY_POKEMON_CENTER_2F    = 9:2 (0x09:0x02)
MAP_VERMILION_CITY_POKEMON_FAN_CLUB     = 9:3 (0x09:0x03)
MAP_VERMILION_CITY_HOUSE2               = 9:4 (0x09:0x04)
MAP_VERMILION_CITY_MART                 = 9:5 (0x09:0x05)
MAP_VERMILION_CITY_GYM                  = 9:6 (0x09:0x06)
MAP_VERMILION_CITY_HOUSE3               = 9:7 (0x09:0x07)
```

### Group 10 (0x0A): gMapGroup_IndoorCeladon

```
MAP_CELADON_CITY_DEPARTMENT_STORE_1F    = 10:0  (0x0A:0x00)
MAP_CELADON_CITY_DEPARTMENT_STORE_2F    = 10:1  (0x0A:0x01)
MAP_CELADON_CITY_DEPARTMENT_STORE_3F    = 10:2  (0x0A:0x02)
MAP_CELADON_CITY_DEPARTMENT_STORE_4F    = 10:3  (0x0A:0x03)
MAP_CELADON_CITY_DEPARTMENT_STORE_5F    = 10:4  (0x0A:0x04)
MAP_CELADON_CITY_DEPARTMENT_STORE_ROOF  = 10:5  (0x0A:0x05)
MAP_CELADON_CITY_DEPARTMENT_STORE_ELEVATOR = 10:6 (0x0A:0x06)
MAP_CELADON_CITY_CONDOMINIUMS_1F        = 10:7  (0x0A:0x07)
MAP_CELADON_CITY_CONDOMINIUMS_2F        = 10:8  (0x0A:0x08)
MAP_CELADON_CITY_CONDOMINIUMS_3F        = 10:9  (0x0A:0x09)
MAP_CELADON_CITY_CONDOMINIUMS_ROOF      = 10:10 (0x0A:0x0A)
MAP_CELADON_CITY_CONDOMINIUMS_ROOF_ROOM = 10:11 (0x0A:0x0B)
MAP_CELADON_CITY_POKEMON_CENTER_1F      = 10:12 (0x0A:0x0C)
MAP_CELADON_CITY_POKEMON_CENTER_2F      = 10:13 (0x0A:0x0D)
MAP_CELADON_CITY_GAME_CORNER            = 10:14 (0x0A:0x0E)
MAP_CELADON_CITY_GAME_CORNER_PRIZE_ROOM = 10:15 (0x0A:0x0F)
MAP_CELADON_CITY_GYM                    = 10:16 (0x0A:0x10)
MAP_CELADON_CITY_RESTAURANT             = 10:17 (0x0A:0x11)
MAP_CELADON_CITY_HOUSE1                 = 10:18 (0x0A:0x12)
MAP_CELADON_CITY_HOTEL                  = 10:19 (0x0A:0x13)
```

### Group 11 (0x0B): gMapGroup_IndoorFuchsia

```
MAP_FUCHSIA_CITY_SAFARI_ZONE_ENTRANCE   = 11:0 (0x0B:0x00)
MAP_FUCHSIA_CITY_MART                   = 11:1 (0x0B:0x01)
MAP_FUCHSIA_CITY_SAFARI_ZONE_OFFICE     = 11:2 (0x0B:0x02)
MAP_FUCHSIA_CITY_GYM                    = 11:3 (0x0B:0x03)
MAP_FUCHSIA_CITY_HOUSE1                 = 11:4 (0x0B:0x04)
MAP_FUCHSIA_CITY_POKEMON_CENTER_1F      = 11:5 (0x0B:0x05)
MAP_FUCHSIA_CITY_POKEMON_CENTER_2F      = 11:6 (0x0B:0x06)
MAP_FUCHSIA_CITY_WARDENS_HOUSE          = 11:7 (0x0B:0x07)
MAP_FUCHSIA_CITY_HOUSE2                 = 11:8 (0x0B:0x08)
MAP_FUCHSIA_CITY_HOUSE3                 = 11:9 (0x0B:0x09)
```

### Group 12 (0x0C): gMapGroup_IndoorCinnabar

```
MAP_CINNABAR_ISLAND_GYM                         = 12:0 (0x0C:0x00)
MAP_CINNABAR_ISLAND_POKEMON_LAB_ENTRANCE        = 12:1 (0x0C:0x01)
MAP_CINNABAR_ISLAND_POKEMON_LAB_LOUNGE          = 12:2 (0x0C:0x02)
MAP_CINNABAR_ISLAND_POKEMON_LAB_RESEARCH_ROOM   = 12:3 (0x0C:0x03)
MAP_CINNABAR_ISLAND_POKEMON_LAB_EXPERIMENT_ROOM = 12:4 (0x0C:0x04)
MAP_CINNABAR_ISLAND_POKEMON_CENTER_1F           = 12:5 (0x0C:0x05)
MAP_CINNABAR_ISLAND_POKEMON_CENTER_2F           = 12:6 (0x0C:0x06)
MAP_CINNABAR_ISLAND_MART                        = 12:7 (0x0C:0x07)
```

### Group 13 (0x0D): gMapGroup_IndoorIndigoPlateau

```
MAP_INDIGO_PLATEAU_POKEMON_CENTER_1F    = 13:0 (0x0D:0x00)
MAP_INDIGO_PLATEAU_POKEMON_CENTER_2F    = 13:1 (0x0D:0x01)
```

### Group 14 (0x0E): gMapGroup_IndoorSaffron

```
MAP_SAFFRON_CITY_COPYCATS_HOUSE_1F          = 14:0 (0x0E:0x00)
MAP_SAFFRON_CITY_COPYCATS_HOUSE_2F          = 14:1 (0x0E:0x01)
MAP_SAFFRON_CITY_DOJO                       = 14:2 (0x0E:0x02)
MAP_SAFFRON_CITY_GYM                        = 14:3 (0x0E:0x03)
MAP_SAFFRON_CITY_HOUSE                      = 14:4 (0x0E:0x04)
MAP_SAFFRON_CITY_MART                       = 14:5 (0x0E:0x05)
MAP_SAFFRON_CITY_POKEMON_CENTER_1F          = 14:6 (0x0E:0x06)
MAP_SAFFRON_CITY_POKEMON_CENTER_2F          = 14:7 (0x0E:0x07)
MAP_SAFFRON_CITY_MR_PSYCHICS_HOUSE          = 14:8 (0x0E:0x08)
MAP_SAFFRON_CITY_POKEMON_TRAINER_FAN_CLUB   = 14:9 (0x0E:0x09)
```

### Group 15 (0x0F): gMapGroup_IndoorRoute2

```
MAP_ROUTE2_VIRIDIAN_FOREST_SOUTH_ENTRANCE   = 15:0 (0x0F:0x00)
MAP_ROUTE2_HOUSE                            = 15:1 (0x0F:0x01)
MAP_ROUTE2_EAST_BUILDING                    = 15:2 (0x0F:0x02)
MAP_ROUTE2_VIRIDIAN_FOREST_NORTH_ENTRANCE   = 15:3 (0x0F:0x03)
```

### Group 16 (0x10): gMapGroup_IndoorRoute4

```
MAP_ROUTE4_POKEMON_CENTER_1F    = 16:0 (0x10:0x00)
MAP_ROUTE4_POKEMON_CENTER_2F    = 16:1 (0x10:0x01)
```

### Group 17 (0x11): gMapGroup_IndoorRoute5

```
MAP_ROUTE5_POKEMON_DAY_CARE     = 17:0 (0x11:0x00)
MAP_ROUTE5_SOUTH_ENTRANCE       = 17:1 (0x11:0x01)
```

### Group 18 (0x12): gMapGroup_IndoorRoute6

```
MAP_ROUTE6_NORTH_ENTRANCE       = 18:0 (0x12:0x00)
MAP_ROUTE6_UNUSED_HOUSE         = 18:1 (0x12:0x01)
```

### Group 19 (0x13): gMapGroup_IndoorRoute7

```
MAP_ROUTE7_EAST_ENTRANCE        = 19:0 (0x13:0x00)
```

### Group 20 (0x14): gMapGroup_IndoorRoute8

```
MAP_ROUTE8_WEST_ENTRANCE        = 20:0 (0x14:0x00)
```

### Group 21 (0x15): gMapGroup_IndoorRoute10

```
MAP_ROUTE10_POKEMON_CENTER_1F   = 21:0 (0x15:0x00)
MAP_ROUTE10_POKEMON_CENTER_2F   = 21:1 (0x15:0x01)
```

### Group 22 (0x16): gMapGroup_IndoorRoute11

```
MAP_ROUTE11_EAST_ENTRANCE_1F    = 22:0 (0x16:0x00)
MAP_ROUTE11_EAST_ENTRANCE_2F    = 22:1 (0x16:0x01)
```

### Group 23 (0x17): gMapGroup_IndoorRoute12

```
MAP_ROUTE12_NORTH_ENTRANCE_1F   = 23:0 (0x17:0x00)
MAP_ROUTE12_NORTH_ENTRANCE_2F   = 23:1 (0x17:0x01)
MAP_ROUTE12_FISHING_HOUSE       = 23:2 (0x17:0x02)
```

### Group 24 (0x18): gMapGroup_IndoorRoute15

```
MAP_ROUTE15_WEST_ENTRANCE_1F    = 24:0 (0x18:0x00)
MAP_ROUTE15_WEST_ENTRANCE_2F    = 24:1 (0x18:0x01)
```

### Group 25 (0x19): gMapGroup_IndoorRoute16

```
MAP_ROUTE16_HOUSE               = 25:0 (0x19:0x00)
MAP_ROUTE16_NORTH_ENTRANCE_1F   = 25:1 (0x19:0x01)
MAP_ROUTE16_NORTH_ENTRANCE_2F   = 25:2 (0x19:0x02)
```

### Group 26 (0x1A): gMapGroup_IndoorRoute18

```
MAP_ROUTE18_EAST_ENTRANCE_1F    = 26:0 (0x1A:0x00)
MAP_ROUTE18_EAST_ENTRANCE_2F    = 26:1 (0x1A:0x01)
```

### Group 27 (0x1B): gMapGroup_IndoorRoute19

```
MAP_ROUTE19_UNUSED_HOUSE        = 27:0 (0x1B:0x00)
```

### Group 28 (0x1C): gMapGroup_IndoorRoute22

```
MAP_ROUTE22_NORTH_ENTRANCE      = 28:0 (0x1C:0x00)
```

### Group 29 (0x1D): gMapGroup_IndoorRoute23

```
MAP_ROUTE23_UNUSED_HOUSE        = 29:0 (0x1D:0x00)
```

### Group 30 (0x1E): gMapGroup_IndoorRoute25

```
MAP_ROUTE25_SEA_COTTAGE         = 30:0 (0x1E:0x00)
```

### Group 31 (0x1F): gMapGroup_IndoorSevenIsland

```
MAP_SEVEN_ISLAND_HOUSE_ROOM1        = 31:0 (0x1F:0x00)
MAP_SEVEN_ISLAND_HOUSE_ROOM2        = 31:1 (0x1F:0x01)
MAP_SEVEN_ISLAND_MART               = 31:2 (0x1F:0x02)
MAP_SEVEN_ISLAND_POKEMON_CENTER_1F  = 31:3 (0x1F:0x03)
MAP_SEVEN_ISLAND_POKEMON_CENTER_2F  = 31:4 (0x1F:0x04)
MAP_SEVEN_ISLAND_UNUSED_HOUSE       = 31:5 (0x1F:0x05)
MAP_SEVEN_ISLAND_HARBOR             = 31:6 (0x1F:0x06)
```

### Group 32 (0x20): gMapGroup_IndoorOneIsland

```
MAP_ONE_ISLAND_POKEMON_CENTER_1F    = 32:0 (0x20:0x00)
MAP_ONE_ISLAND_POKEMON_CENTER_2F    = 32:1 (0x20:0x01)
MAP_ONE_ISLAND_HOUSE1               = 32:2 (0x20:0x02)
MAP_ONE_ISLAND_HOUSE2               = 32:3 (0x20:0x03)
MAP_ONE_ISLAND_HARBOR               = 32:4 (0x20:0x04)
```

### Group 33 (0x21): gMapGroup_IndoorTwoIsland

```
MAP_TWO_ISLAND_JOYFUL_GAME_CORNER   = 33:0 (0x21:0x00)
MAP_TWO_ISLAND_HOUSE                = 33:1 (0x21:0x01)
MAP_TWO_ISLAND_POKEMON_CENTER_1F    = 33:2 (0x21:0x02)
MAP_TWO_ISLAND_POKEMON_CENTER_2F    = 33:3 (0x21:0x03)
MAP_TWO_ISLAND_HARBOR               = 33:4 (0x21:0x04)
```

### Group 34 (0x22): gMapGroup_IndoorThreeIsland

```
MAP_THREE_ISLAND_HOUSE1             = 34:0 (0x22:0x00)
MAP_THREE_ISLAND_POKEMON_CENTER_1F  = 34:1 (0x22:0x01)
MAP_THREE_ISLAND_POKEMON_CENTER_2F  = 34:2 (0x22:0x02)
MAP_THREE_ISLAND_MART               = 34:3 (0x22:0x03)
MAP_THREE_ISLAND_HOUSE2             = 34:4 (0x22:0x04)
MAP_THREE_ISLAND_HOUSE3             = 34:5 (0x22:0x05)
MAP_THREE_ISLAND_HOUSE4             = 34:6 (0x22:0x06)
MAP_THREE_ISLAND_HOUSE5             = 34:7 (0x22:0x07)
```

### Group 35 (0x23): gMapGroup_IndoorFourIsland

```
MAP_FOUR_ISLAND_POKEMON_DAY_CARE    = 35:0 (0x23:0x00)
MAP_FOUR_ISLAND_POKEMON_CENTER_1F   = 35:1 (0x23:0x01)
MAP_FOUR_ISLAND_POKEMON_CENTER_2F   = 35:2 (0x23:0x02)
MAP_FOUR_ISLAND_HOUSE1              = 35:3 (0x23:0x03)
MAP_FOUR_ISLAND_LORELEIS_HOUSE      = 35:4 (0x23:0x04)
MAP_FOUR_ISLAND_HARBOR              = 35:5 (0x23:0x05)
MAP_FOUR_ISLAND_HOUSE2              = 35:6 (0x23:0x06)
MAP_FOUR_ISLAND_MART                = 35:7 (0x23:0x07)
```

### Group 36 (0x24): gMapGroup_IndoorFiveIsland

```
MAP_FIVE_ISLAND_POKEMON_CENTER_1F   = 36:0 (0x24:0x00)
MAP_FIVE_ISLAND_POKEMON_CENTER_2F   = 36:1 (0x24:0x01)
MAP_FIVE_ISLAND_HARBOR              = 36:2 (0x24:0x02)
MAP_FIVE_ISLAND_HOUSE1              = 36:3 (0x24:0x03)
MAP_FIVE_ISLAND_HOUSE2              = 36:4 (0x24:0x04)
```

### Group 37 (0x25): gMapGroup_IndoorSixIsland

```
MAP_SIX_ISLAND_POKEMON_CENTER_1F    = 37:0 (0x25:0x00)
MAP_SIX_ISLAND_POKEMON_CENTER_2F    = 37:1 (0x25:0x01)
MAP_SIX_ISLAND_HARBOR               = 37:2 (0x25:0x02)
MAP_SIX_ISLAND_HOUSE                = 37:3 (0x25:0x03)
MAP_SIX_ISLAND_MART                 = 37:4 (0x25:0x04)
```

### Group 38 (0x26): gMapGroup_IndoorThreeIslandRoute

```
MAP_THREE_ISLAND_HARBOR             = 38:0 (0x26:0x00)
```

### Group 39 (0x27): gMapGroup_IndoorFiveIslandRoute

```
MAP_FIVE_ISLAND_RESORT_GORGEOUS_HOUSE = 39:0 (0x27:0x00)
```

### Group 40 (0x28): gMapGroup_IndoorTwoIslandRoute

```
MAP_TWO_ISLAND_CAPE_BRINK_HOUSE     = 40:0 (0x28:0x00)
```

### Group 41 (0x29): gMapGroup_IndoorSixIslandRoute

```
MAP_SIX_ISLAND_WATER_PATH_HOUSE1    = 41:0 (0x29:0x00)
MAP_SIX_ISLAND_WATER_PATH_HOUSE2    = 41:1 (0x29:0x01)
```

### Group 42 (0x2A): gMapGroup_IndoorSevenIslandRoute

```
MAP_SEVEN_ISLAND_SEVAULT_CANYON_HOUSE = 42:0 (0x2A:0x00)
```

### Special Map Values

```
MAP_DYNAMIC   = 0x7F7F  (動的ワープ用)
MAP_UNDEFINED = 0xFFFF  (無効マップ)
```

---

## Heal Location IDs

`src/data/heal_locations.json` より。ID は enum で HEAL_LOCATION_NONE=0 から始まり、以下が1始まりで順番に割り当てられる。

書式: `HEAL_LOCATION_NAME = decimal (0xHex)`

ヒールポイントの座標はフィールドマップ上のポケモンセンター前 (またはパレットタウンの自宅前) の位置。

```
HEAL_LOCATION_NONE          =  0 (0x00)   -- 無効値

HEAL_LOCATION_PALLET_TOWN   =  1 (0x01)   -- MAP_PALLET_TOWN (6,8)
HEAL_LOCATION_VIRIDIAN_CITY =  2 (0x02)   -- MAP_VIRIDIAN_CITY (26,27)
HEAL_LOCATION_PEWTER_CITY   =  3 (0x03)   -- MAP_PEWTER_CITY (17,26)
HEAL_LOCATION_CERULEAN_CITY =  4 (0x04)   -- MAP_CERULEAN_CITY (22,20)
HEAL_LOCATION_LAVENDER_TOWN =  5 (0x05)   -- MAP_LAVENDER_TOWN (6,6)
HEAL_LOCATION_VERMILION_CITY =  6 (0x06)  -- MAP_VERMILION_CITY (15,7)
HEAL_LOCATION_CELADON_CITY  =  7 (0x07)   -- MAP_CELADON_CITY (48,12)
HEAL_LOCATION_FUCHSIA_CITY  =  8 (0x08)   -- MAP_FUCHSIA_CITY (25,32)
HEAL_LOCATION_CINNABAR_ISLAND =  9 (0x09) -- MAP_CINNABAR_ISLAND (14,12)
HEAL_LOCATION_INDIGO_PLATEAU = 10 (0x0A)  -- MAP_INDIGO_PLATEAU_EXTERIOR (11,7)
HEAL_LOCATION_SAFFRON_CITY  = 11 (0x0B)   -- MAP_SAFFRON_CITY (24,39)
HEAL_LOCATION_ROUTE4        = 12 (0x0C)   -- MAP_ROUTE4 (12,6)
HEAL_LOCATION_ROUTE10       = 13 (0x0D)   -- MAP_ROUTE10 (13,21)
HEAL_LOCATION_ONE_ISLAND    = 14 (0x0E)   -- MAP_ONE_ISLAND (14,6)
HEAL_LOCATION_TWO_ISLAND    = 15 (0x0F)   -- MAP_TWO_ISLAND (21,8)
HEAL_LOCATION_THREE_ISLAND  = 16 (0x10)   -- MAP_THREE_ISLAND (14,28)
HEAL_LOCATION_FOUR_ISLAND   = 17 (0x11)   -- MAP_FOUR_ISLAND (18,21)
HEAL_LOCATION_FIVE_ISLAND   = 18 (0x12)   -- MAP_FIVE_ISLAND (18,7)
HEAL_LOCATION_SEVEN_ISLAND  = 19 (0x13)   -- MAP_SEVEN_ISLAND (12,4)
HEAL_LOCATION_SIX_ISLAND    = 20 (0x14)   -- MAP_SIX_ISLAND (11,12)

NUM_HEAL_LOCATIONS          = 21 (0x15)
```

### Respawnマップ対応表

| Heal Location | Respawnマップ |
|---|---|
| PALLET_TOWN | MAP_PALLET_TOWN_PLAYERS_HOUSE_1F (4:0) |
| VIRIDIAN_CITY | MAP_VIRIDIAN_CITY_POKEMON_CENTER_1F (5:4) |
| PEWTER_CITY | MAP_PEWTER_CITY_POKEMON_CENTER_1F (6:5) |
| CERULEAN_CITY | MAP_CERULEAN_CITY_POKEMON_CENTER_1F (7:3) |
| LAVENDER_TOWN | MAP_LAVENDER_TOWN_POKEMON_CENTER_1F (8:0) |
| VERMILION_CITY | MAP_VERMILION_CITY_POKEMON_CENTER_1F (9:1) |
| CELADON_CITY | MAP_CELADON_CITY_POKEMON_CENTER_1F (10:12) |
| FUCHSIA_CITY | MAP_FUCHSIA_CITY_POKEMON_CENTER_1F (11:5) |
| CINNABAR_ISLAND | MAP_CINNABAR_ISLAND_POKEMON_CENTER_1F (12:5) |
| INDIGO_PLATEAU | MAP_INDIGO_PLATEAU_POKEMON_CENTER_1F (13:0) |
| SAFFRON_CITY | MAP_SAFFRON_CITY_POKEMON_CENTER_1F (14:6) |
| ROUTE4 | MAP_ROUTE4_POKEMON_CENTER_1F (16:0) |
| ROUTE10 | MAP_ROUTE10_POKEMON_CENTER_1F (21:0) |
| ONE_ISLAND | MAP_ONE_ISLAND_POKEMON_CENTER_1F (32:0) |
| TWO_ISLAND | MAP_TWO_ISLAND_POKEMON_CENTER_1F (33:2) |
| THREE_ISLAND | MAP_THREE_ISLAND_POKEMON_CENTER_1F (34:1) |
| FOUR_ISLAND | MAP_FOUR_ISLAND_POKEMON_CENTER_1F (35:1) |
| FIVE_ISLAND | MAP_FIVE_ISLAND_POKEMON_CENTER_1F (36:0) |
| SEVEN_ISLAND | MAP_SEVEN_ISLAND_POKEMON_CENTER_1F (31:3) |
| SIX_ISLAND | MAP_SIX_ISLAND_POKEMON_CENTER_1F (37:0) |

---

## 備考

- **GBA版のみ**: 上記アドレス・IDはすべてGBA版 (pret/pokefirered) のもの。Switch版NSO (Pokemon FireRed) は内部構造が異なる可能性がある。
- **warpコマンドでの使用**: `warp MAP_GROUP MAP_NUM WARP_ID X Y` の形式。通常 WARP_ID は -1 (WARP_ID_NONE) を指定し、座標で直接指定する。
- **setrespawnコマンド**: 引数は HEAL_LOCATION_* の値 (1〜20)。
