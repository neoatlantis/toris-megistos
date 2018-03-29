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

```yaml
io:
    # GPIO aliases. Must be positive or negative integers, where, a positive
    # integer means the corresponding pin will be set to 1 on True, 0 on False,
    # and a negative integer reverses this behaviour.
    #
    # Internal pull-up/pull-down resistors will be configured accordingly.
    #

    LED.R: 10   # channels for controlling LED colors
    LED.G: 11
    LED.B: 12

    ENERGY.0:   15      # channels for displaying portal energy levels
    ENERGY.1:   16
    ENERGY.2:   17
    ENERGY.3:   18
    ENERGY.4:   19
    ENERGY.5:   20
    ENERGY.6:   21
    ENERGY.7:   22
    ENERGY.8:   23
    ENERGY.9:   24

    LEVEL.4: 7      # BCD code for resonator level digital number display
    LEVEL.2: 8
    LEVEL.1: 9

    _BCD.4: 3
    _BCD.2: 4
    _BCD.1: 5

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
            ENERGEY.0: True
            ENERGEY.1: False 
            ENERGEY.2: False 
            ENERGEY.3: False 
            ENERGEY.4: False 
            ENERGEY.5: False 
            ENERGEY.6: False 
            ENERGEY.7: False 
            ENERGEY.8: False 
            ENERGEY.9: False 
        HEALTH(10,20):
            ENERGEY.0: True
            ENERGEY.1: True 
            ENERGEY.2: False 
            ENERGEY.3: False 
            ENERGEY.4: False 
            ENERGEY.5: False 
            ENERGEY.6: False 
            ENERGEY.7: False 
            ENERGEY.8: False 
            ENERGEY.9: False 


```
