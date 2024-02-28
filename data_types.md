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

Initializing arrays:
```
initial begin
  static int arr[4]   = '{0,1,2,3,4};            // Initialize 4 elements
  
  arr[0:2]            = '{1,2,3};         // Set just first 3 elements
  arr                 = '{4{8}};          // All elements will become 8
  arr                 = '{default:8};     // All elements will become 8
end
```

:memo: **Note**: Notice that, the declaration of the array includes an initial value. When we don't use initial value, we must not declare the array with static. The 2009 LRM states that these variables must be declared either in a static block, or have the static keyword. Since this experts recommends always declaring your test modules and programs as automatic , you need to add the static keyword to a declaration plus initialization when it is inside an initial block.

##### 1-) Multi-dimensional Arrays

```
int array1 [0:7][0:3];  // verbose declaration
int array2 [8][4];      // compact declaration
array2[7][3] = 1;       // set last array element
```

:memo: **Note**: If your code accidently tries to read from an out of bounds address, SV will return the default value for the array element type.

Default value for 4-State variables is "x".
Default value for 2-State variables is "0".

##### 2-) Unpacked Array:

```
bit [7:0] b_unpack [3];
```

Why is it named as unpacked?

Because some of the parts in memory cannot be used.

![](images/unpacked_array.png)

