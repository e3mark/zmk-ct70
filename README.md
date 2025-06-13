# Dactyl CT70

zmk-config/
└── config/
    └── boards/
        └── shields/
            ├── ct70_left/
            │   ├── ct70_left.keymap
            │   ├── shield.conf
            │   └── ct70_left.overlay (optional for matrix)
            └── ct70_right/
                ├── ct70_right.keymap
                ├── shield.conf
                └── ct70_right.overlay (optional for matrix)


## Build commands:

west build -s zmk/app -d build/left -b nice_nano_v2 -- -DSHIELD=ct70_left
west build -s zmk/app -d build/right -b nice_nano_v2 -- -DSHIELD=ct70_right