Lua t-digest library
====================
The [t-digest construction algorithm](https://github.com/tdunning/t-digest/blob/master/docs/t-digest-paper/histo.pdf) uses a variant of 1-dimensional k-means clustering to product a data structure that is related to the Q-digest, which can be used to estimate quantiles. The error bound of t-digest is relative to the quantile and has higher accuracy when computing quantiles for very small *q* or for *q* near 1. The accuracy/size tradeoff is controlled by a single parameter.

## Installation

### Prerequisites
* C compiler (GCC 4.7+, Visual Studio 2013, MinGW (Lua 5.1))
* Lua 5.1, Lua 5.2, or LuaJIT
* [CMake (2.8.7+)](http://cmake.org/cmake/resources/software.html)

### CMake Build Instructions
    git clone https://github.com/vitillo/lua_tdigest.git
    cd lua_tdigest
    cmake -DCMAKE_BUILD_TYPE=release .
    make
    ctest
    cpack

### Example Usage
```lua
local tdigest = require "tdigest"

local td = tdigest.new()
td:add(1)
td:add(2)
td:add(1.5)
local median = td:quantile(0.5)

```

## API Functions
#### new
```lua
local tdigest = require "tdigest"
local td = tdigest.new(0.01)
```

Returns a new tdigest userdata object

*Arguments*
- accuracy (double) The accuracy of t-digest

#### add
```lua
td:add(12.3)
```

Adds a value to the distribution to be estimated.

*Arguments*
- value (double) a value of a distribution

#### quantile
```lua
td:quantile(0.5)
```

Returns the estimated quantile of the underlying distribution.

*Arguments*
- quantile (double)
