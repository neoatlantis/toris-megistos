Toris Megistos
==============

**Toris Megistos** is the legendary XM amplifier utilized by the ancient
Atlantis civilization. It's logic is presented in this project, so that when
loaded into a modern MCU board like Raspberry Pi as the logic core, a reduced
Toris Megistos may be reconstructed.

Toris Megistos is an important element in building a XM ampfifier(portal) from
scratch. It is compatible with Dr. Lyton Wolfe's module _Tecthulhu_, the latter
working as the primary source of XM.

# Configuration and Usage

Toris Megistos accepts a set of rules to finely tune its behaviour. After that
any updates in its source will result in changes at the outputs.

## Rules

Refer to [https://pinout.xyz](https://pinout.xyz) for Rasberry Pi GPIO
numbering.

```yaml
io:
    # GPIO aliases. Must be positive or negative integers, where, a positive
    # integer means the corresponding pin will be set to 1 on True, 0 on False,
    # and a negative integer reverses this behaviour.
    #
    # Internal pull-up/pull-down resistors will be configured accordingly.
    #

    16: LED.R       # channels for controlling LED colors
    18: LED.G
    22: LED.B

    24: E.8         # channels for resonator health info
    26: E.4
    36: E.2
    38: E.1

    19: LEVEL.4     # channels for resonator level numbers
    21: LEVEL.2
    23: LEVEL.1

    11: _BCD.4      # BCD selector for scanning mode
    13: _BCD.2
    15: _BCD.1


static:
    # List of static rules, each rule are defined with a set of tags. When
    # all tags match, change pin outputs inside a rule.

    - RES:
        # example: pin `LED.R`, `LED.G`, `LED.B` define control channels of
        # the main LED decoration.
        LED.B: True
        LED.R: False
        LED.G: False

    - ENL:
        LED.R: False
        LED.G: True
        LED.B: False

    - NEUTRAL:
        LED.R: True
        LED.G: True
        LED.B: True
        # if LED intensity increases, an additional channel for dimming may
        # be desired.


scan:
    # scan rules. Information will be output'ed continously. Each
    # BCD-combination represents a resonator in one location, thus outputs
    # will be set dynamically based on resonator location and matching rules.
    # 
    # Resonator     E    NE    N    NW    W    SW    S     SE
    # BCD-value     0     1    2    1+2   4    4+1   4+2   4+2+1
    #
    BCD:
        4: _BCD.4
        2: _BCD.2 
        1: _BCD.1 

    rules:
        RESO(1):
            LEVEL.4: False 
            LEVEL.2: False 
            LEVEL.1: False
        RESO(2):
            LEVEL.4: False 
            LEVEL.2: False 
            LEVEL.1: True 
        RESO(3):
            LEVEL.4: False 
            LEVEL.2: True
            LEVEL.1: False
        RESO(4):
            LEVEL.4: False 
            LEVEL.2: True
            LEVEL.1: True 
        RESO(5):
            LEVEL.4: True
            LEVEL.2: False 
            LEVEL.1: False 
        RESO(6):
            LEVEL.4: True
            LEVEL.2: False 
            LEVEL.1: True 
        RESO(7):
            LEVEL.4: True
            LEVEL.2: True
            LEVEL.1: False
        RESO(8):
            LEVEL.4: True
            LEVEL.2: True
            LEVEL.1: True

        HEALTH(0,10):
            E.1: False 
            E.2: False 
            E.4: False 
            E.8: False 
        HEALTH(10,20):
            E.1: True
            E.2: False 
            E.4: False 
            E.8: False 
        HEALTH(20,30):
            E.1: False 
            E.2: True 
            E.4: False 
            E.8: False 
        HEALTH(30,40):
            E.1: True
            E.2: True 
            E.4: False 
            E.8: False 
        HEALTH(40,50):
            E.1: False 
            E.2: False 
            E.4: True 
            E.8: False 
        HEALTH(50,60):
            E.1: True 
            E.2: False 
            E.4: True 
            E.8: False 
        HEALTH(60,70):
            E.1: False 
            E.2: True 
            E.4: True
            E.8: False 
        HEALTH(70,80):
            E.1: True
            E.2: True 
            E.4: True 
            E.8: False 
        HEALTH(80,90):
            E.1: False 
            E.2: False 
            E.4: False 
            E.8: True 
        HEALTH(90,100):
            E.1: True
            E.2: False 
            E.4: False 
            E.8: True 


```
