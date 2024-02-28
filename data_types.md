## SystemVerilog Data Types

We can basically group SV data types as 4-state variable and 2-state variable.

4-State variables: integer, logic, reg

2-State variables: int, byte, longint, bit


### Arrays:

#### Fixed-Size Array:

```
int arr1 [0:31];            // 32 ints [0]...[31]
int arr2 [32];              // 32 ints [0]...[31] 
```

Declaring an array with parameters:

```
parameter MEM_SIZE    = 64;
parameter ADDR_WIDTH  = $clog2(MEM_SIZE);           // log2(64) = 6

bit [63:          0]  mem     [MEM_SIZE];
bit [ADDR_WIDTH-1:0]  addr;
```

##### 1-) Multi-dimensional Arrays

```
int array1 [0:7][0:3];  // verbose declaration
int array2 [8][4];      // compact declaration
array2[7][3] = 1;       // set last array element
```

If your code accidently tries to read from an out of bounds address, SV will return the default value for the array element type.

Default value for 4-State variables is "x".
Default value for 2-State variables is "0".

##### 2-) Unpacked Array:

```
bit [7:0]             b_unpack [3];
```

Why is it named as unpacked?

Because some of the parts in memory cannot be used.

![](images/unpacked_array.png)