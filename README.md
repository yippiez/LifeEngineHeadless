
# Life Engine Headless

> [!CAUTION]
> This is not the original, but a fork of the Life-Engine Project. [See here](https://github.com/MaxRobinsonTheGreat/LifeEngine) for the original.


This project is a fork of the original life-engine, it aims to achive a headless and "faster" execution with added feature of recording runs in a custom format.

# Format & Compression

If we were to save the state of the entire grid, cell by cell for a window of size $1024*1024$ with 3 color channels (r, g, b) each; we would need **3.145728 MB** per frame. In order to aliveate this a custom format/compression scheme is used to store the recordings.

This section explains the format and compression scheme used to store the recordings.

### Map

Only the "food" information is stored in a frame by frame basis. This is done using a basic RLE+XOR scheme where the 1 in the binary is where food is and 0 is where a void is placed.

### Entities

Since entities are usually sparse but multiple, it makes more sense to store them seperately. Then for each instance of an entity a position (x, y) is stored. 


So a **mock** of this format will be:

```json
{
    "map": [
        "0xaef...", // First frame
        "0x0a0...", // First Frame xor Second Frame
        ...
    ]
    "entities": [
        {
            "cells": [...]
            "instances": [
                (4, 5),
                (6, 7),
                ...
            ]
        }
    ]
}
```

# Roadmap
- [ ] Headless Running
- [ ] Option to start from a random collection of cells and entities
- [ ] Compressed Recording
- [ ] Bun/Other easy options tested for speed
- [ ] Basic Benchmarking 