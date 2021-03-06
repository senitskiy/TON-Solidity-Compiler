# **TON Solidity API**

TON Solidity compiler expands Solidity language with different API
functions to facilitate TON contract development.

## Table of Contents

* [TON specific types](#ton-specific-types)
  * [TON units](#ton-units)
  * [TvmCell](#tvmcell)
    * [TvmCell.depth()](#tvmcelldepth)
    * [TvmCell.dataSize()](#tvmcelldatasize)
    * [TvmCell.dataSizeQ()](#tvmcelldatasizeq)
    * [TvmCell.toSlice()](#tvmcelltoslice)
  * [TvmSlice](#tvmslice)
    * [TvmSlice.size()](#tvmslicesize)
    * [TvmSlice.dataSize()](#tvmslicedatasize)
    * [TvmSlice.dataSizeQ()](#tvmslicedatasizeq)
    * [TvmSlice.bits()](#tvmslicebits)
    * [TvmSlice.refs()](#tvmslicerefs)
    * [TvmSlice.depth()](#tvmslicedepth)
    * [TvmSlice.decode()](#tvmslicedecode)
    * [TvmSlice.loadRef()](#tvmsliceloadref)
    * [TvmSlice.loadRefAsSlice()](#tvmsliceloadrefasslice)
    * [TvmSlice.loadSigned()](#tvmsliceloadsigned)
    * [TvmSlice.loadUnsigned()](#tvmsliceloadunsigned)
    * [TvmSlice.loadTons()](#tvmsliceloadtons)
    * [TvmSlice.decodeFunctionParams()](#tvmslicedecodefunctionparams)
  * [TvmBuilder](#tvmbuilder)
    * [TvmBuilder.toSlice()](#tvmbuildertoslice)
    * [TvmBuilder.toCell()](#tvmbuildertocell)
    * [TvmBuilder.bits()](#tvmbuilderbits)
    * [TvmBuilder.refs()](#tvmbuilderrefs)
    * [TvmBuilder.bitsAndRefs()](#tvmbuilderbitsandrefs)
    * [TvmBuilder.remBits()](#tvmbuilderrembits)
    * [TvmBuilder.remRefs()](#tvmbuilderremrefs)
    * [TvmBuilder.remBitsAndRefs()](#tvmbuilderrembitsandrefs)
    * [TvmBuilder.depth()](#tvmbuilderdepth)
    * [TvmBuilder.store()](#tvmbuilderstore)
    * [TvmBuilder.storeSigned()](#tvmbuilderstoresigned)
    * [TvmBuilder.storeUnsigned()](#tvmbuilderstoreunsigned)
    * [TvmBuilder.storeRef()](#tvmbuilderstoreref)
    * [TvmBuilder.storeTons()](#tvmbuilderstoretons)
  * [ExtraCurrencyCollection](#extracurrencycollection)
  * [optional&lt;Type&gt;](#optionaltype)
    * [optional&lt;Type&gt;.hasValue()](#optionaltypehasvalue)
    * [optional&lt;Type&gt;.get()](#optionaltypeget)
    * [optional&lt;Type&gt;.set()](#optionaltypeset)
    * [optional&lt;Type&gt;.reset()](#optionaltypereset)
* [TON specific control structures](#ton-specific-control-structures)
  * [repeat](#repeat)
* Changes and extensions in solidity types
  * [struct](#struct)
    * [struct.unpack()](#structunpack)
  * [string](#string)
    * [string.byteLength()](#stringbytelength)
    * [string.substr()](#stringsubstr)
    * [string(int)](#stringint)
    * [hexstring()](#hexstring)
    * [format()](#format)
    * [stoi()](#stoi)
  * [bytes](#bytes)
    * [operator[]](#operator)
    * [bytes.length](#byteslength)
    * [bytes.toSlice](#bytestoslice)
    * [bytes.dataSize()](#bytesdatasize)
    * [bytes.dataSizeQ()](#bytesdatasizeq)
  * [address](#address)
    * [Object creating](#object-creating)
      * [constructor()](#constructor)
      * [address.makeAddrStd()](#addressmakeaddrstd)
      * [address.makeAddrNone()](#addressmakeaddrnone)
      * [address.makeAddrExtern()](#addressmakeaddrextern)
    * [Members](#members)
      * [address.wid](#addresswid)
      * [address.value](#addressvalue)
      * [address.balance](#addressbalance)
      * [address.currencies](#addresscurrencies)
    * [Functions](#functions)
      * [address.getType()](#addressgettype)
      * [address.isStdZero()](#addressisstdzero)
      * [address.isStdAddrWithoutAnyCast()](#addressisstdaddrwithoutanycast)
      * [address.isExternZero()](#addressisexternzero)
      * [address.isNone()](#addressisnone)
      * [address.unpack()](#addressunpack)
      * [address.transfer()](#addresstransfer)
  * [mapping](#mapping)
    * [mapping.operator[]](#mappingoperator)
    * [mapping.at()](#mappingat)
    * [mapping.min() and mapping.max()](#mappingmin-and-mappingmax)
    * [mapping.next() and mapping.prev()](#mappingnext-and-mappingprev)
    * [mapping.nextOrEq() and mapping.prevOrEq()](#mappingnextoreq-and-mappingprevoreq)
    * [mapping.delMin() and mapping.delMax()](#mappingdelmin-and-mappingdelmax)
    * [mapping.fetch()](#mappingfetch)
    * [mapping.exists()](#mappingexists)
    * [mapping.empty()](#mappingempty)
    * [mapping.replace()](#mappingreplace)
    * [mapping.add()](#mappingadd)
    * [mapping.getSet()](#mappinggetset)
    * [mapping.getAdd()](#mappinggetadd)
    * [mapping.getReplace()](#mappinggetreplace)
  * [require, revert](#require-revert)
    * [require](#require)
    * [revert](#revert)
  * [Libraries](#libraries)
    * [Function call via library name](#function-call-via-library-name)
    * [Function call via object](#function-call-via-object)
* [Pragmas](#pragmas)
  * [pragma ignoreIntOverflow](#pragma-ignoreintoverflow)
  * [pragma AbiHeader](#pragma-abiheader)
  * [pragma msgValue](#pragma-msgvalue)
* [State variables](#state-variables)
  * [Keyword `static`](#keyword-static)
* [Special contract functions](#special-contract-functions)
  * [receive](#receive)
  * [fallback](#fallback)
  * [onBounce](#onbounce)
  * [onTickTock](#onticktock)
  * [onCodeUpgrade](#oncodeupgrade)
  * [afterSignatureCheck](#aftersignaturecheck)
* [Function specifiers](#function-specifiers)
  * [Function mutability: pure, view and default](#function-mutability-pure-view-and-default)
  * [Keyword inline](#keyword-inline)
  * [functionID()](#functionid)
* [Events and return](#events-and-return)
  * [extAddr](#extaddr)
  * [return](#return)
* [External function calls](#external-function-calls)
* [API functions and members](#api-functions-and-members)
  * [**msg** namespace](#msg-namespace)
    * [msg.value](#msgvalue)
    * [msg.currencies](#msgcurrencies)
    * [msg.pubkey()](#msgpubkey)
    * [msg.createdAt](#msgcreatedat)
    * [msg.data](#msgdata)
  * [**tvm** namespace](#tvm-namespace)
    * [TVM instructions](#tvm-instructions)
      * [tvm.accept()](#tvmaccept)
      * [tvm.commit()](#tvmcommit)
      * [tvm.log()](#tvmlog)
      * [tvm.setcode()](#tvmsetcode)
      * [tvm.transLT()](#tvmtranslt)
      * [tvm.configParam()](#tvmconfigparam)
      * [tvm.rawConfigParam()](#tvmrawconfigparam)
      * [tvm.rawReserve()](#tvmrawreserve)
    * [Hashing and cryptography](#hashing-and-cryptography)
      * [tvm.hash()](#tvmhash)
      * [tvm.checkSign()](#tvmchecksign)
    * [Deploy contract from contract](#deploy-contract-from-contract)
      * [tvm.insertPubkey()](#tvminsertpubkey)
      * [tvm.buildStateInit()](#tvmbuildstateinit)
      * [tvm.buildEmptyData()](#tvmbuildemptydata)
      * [tvm.deploy()](#tvmdeploy)
      * [Deploy via new](#deploy-via-new)
    * [Misc functions from `tvm`](#misc-functions-from-tvm)
      * [tvm.pubkey()](#tvmpubkey)
      * [tvm.setCurrentCode()](#tvmsetcurrentcode)
      * [tvm.resetStorage()](#tvmresetstorage)
      * [tvm.functionId()](#tvmfunctionid)
      * [tvm.encodeBody()](#tvmencodebody)
      * [tvm.exit() and tvm.exit1()](#tvmexit-and-tvmexit1)
  * [**math** namespace](#math-namespace)
    * [math.min() and math.max()](#mathmin-and-mathmax)
    * [math.minmax()](#mathminmax)
    * [math.abs()](#mathabs)
    * [math.modpow2()](#mathmodpow2)
    * [math.divr() math.divc()](#mathdivr-mathdivc)
    * [math.muldiv() math.muldivr() math.muldivc()](#mathmuldiv-mathmuldivr-mathmuldivc)
    * [math.muldivmod()](#mathmuldivmod)
  * [**tx** namespace](#tx-namespace)
    * [tx.timestamp](#txtimestamp)
  * [**block** namespace](#block-namespace)
    * [block.timestamp](#blocktimestamp)
  * [**rnd** namespace](#rnd-namespace)
    * [rnd.next](#rndnext)
    * [rnd.getSeed](#rndgetseed)
    * [rnd.setSeed](#rndsetseed)
    * [rnd.shuffle](#rndshuffle)
  * [selfdestruct](#selfdestruct)

## Detailed description

### TON specific types

TON Solidity compiler expands functionality of some existing types and adds several new TVM specific types: TvmCell, TvmSlice, TvmBuilder and ExtraCurrencyCollection. Full description of this types can be found in [TVM][1] and [TON Blockchain][2] specifications.

#### TON units

A literal number can take a suffix to specify a subdenomination of TON currency, where numbers without a postfix are assumed to be nanotons.

```TVMSolidity
require(1 nano == 1);
require(1 nanoton == 1);
require(1 nTon == 1);
require(1 ton == 1e9 nanoton);
require(1 Ton == 1e9 nanoton);
require(1 micro == 1e-6 ton);
require(1 microton == 1e-6 ton);
require(1 milli == 1e-3 ton);
require(1 milliton == 1e-3 ton);
require(1 kiloton == 1e3 ton);
require(1 kTon == 1e3 ton);
require(1 megaton == 1e6 ton);
require(1 MTon == 1e6 ton);
require(1 gigaton == 1e9 ton);
require(1 GTon == 1e9 ton);
```

#### TvmCell

TvmCell represents TVM type Cell. TON Solidity compiler defines the following functions to work with this type:

##### TvmCell.depth()

```TVMSolidity
TvmCell c;
uint64 d = c.depth();
```

Returns the depth of TvmCell **c**. If **c** has no references, then **d** = 0;
otherwise **d** is one plus the maximum of depths of cells referred to from **c**.
If **c** is a Null instead of a Cell, returns zero.

#### TvmCell.dataSize()

```TVMSolidity
TvmCell c = ...;
uint n = ...;
(uint cells, uint bits, uint refs) = c.dataSize(n);
```

Return the count of distinct cells, data bits in the distinct cells and
cell references in the distinct cells. If count of the distinct cells is
exceed `n+1` than a cell overflow exception (8) is thrown.  
This function is a wrapper for opcode "CDATASIZE" ([TVM][1] - A.11.7).

#### TvmCell.dataSizeQ()

```TVMSolidity
TvmSlice s = ...;
uint n = ...;
optional(uint, uint, uint) size = c.dataSizeQ(n);
if (size.hasValue()) {
    (uint cells, uint bits, uint refs) = size.get();
}
```

Return the count of distinct cells, data bits in the distinct cells and
cell references in the distinct cells. If count of the distinct cells is
exceed `n+1` than this function return `optional` that have no value.  
This function is a wrapper for opcode "CDATASIZEQ" ([TVM][1] - A.11.7).

##### TvmCell.toSlice()

```TVMSolidity
TvmCell cell;
TvmSlice slice = cell.toSlice();
```

This function converts cell to slice.

#### TvmSlice

TvmSlice represents TVM type Slice. TON Solidity compiler defines the following functions to work with this type:

##### TvmSlice.size()

```TVMSolidity
TvmSlice slice;
(uint16 bits, uint8 refs) = slice.size();
```

This function returns number of data bits and references in the slice.

#### TvmSlice.dataSize()

```TVMSolidity
TvmSlice s = ...;
uint n = ...;
(uint cells, uint bits, uint refs) = s.dataSize(n);
```

Return the count of distinct cells, data bits in the distinct cells and
cell references in the distinct cells. If count of the distinct cells is
exceed `n+1` than a cell overflow exception (8) is thrown.  
Note that the returned `count of distinct cells` does not take into
account the cell that contains the slice `s` itself.  
This function is a wrapper for opcode "SDATASIZE" ([TVM][1] - A.11.7).

#### TvmSlice.dataSizeQ()

```TVMSolidity
TvmSlice s = ...;
uint n = ...;
optional(uint, uint, uint) size = s.dataSizeQ(n);
if (size.hasValue()) {
    (uint cells, uint bits, uint refs) = size.get();
}
```

Return the count of distinct cells, data bits in the distinct cells and
cell references in the distinct cells. If count of the distinct cells is
exceed `n+1` than this function return `optional` that have no value.  
Note that the returned `count of distinct cells` does not take into
account the cell that contains the slice `s` itself.  
This function is a wrapper for opcode "SDATASIZEQ" ([TVM][1] - A.11.7).

##### TvmSlice.bits()

```TVMSolidity
TvmSlice slice;
uint16 bits = slice.bits();
```

This function returns number of data bits in the slice.

##### TvmSlice.refs()

```TVMSolidity
TvmSlice slice;
uint8 refs = slice.refs();
```

This function returns number of references in the slice.

##### TvmSlice.depth()

```TVMSolidity
TvmSlice s;
uint64 d = s.depth();
```

Returns the depth of TvmSlice **s**. If **s** has no references, then **d = 0**;
otherwise **d** is one plus the maximum of depths of cells referred to from **s**.

##### TvmSlice.decode()

```TVMSolidity
TvmSlice slice;
(TypeA a, TypeB b, ...) = slice.decode(TypeA, TypeB, ...);
```

This function loads given types from the slice.  
Example:

```TVMSolidity
TvmSlice slice;
(uint8 a, uint16 b) = slice.decode(uint8, uint16);
(uint16 num0, uint32 num1, address addr) = slice.decode(uint16, uint32, address);
```

##### TvmSlice.loadRef()

```TVMSolidity
TvmSlice slice;
TvmCell cell = slice.loadRef();
```

This function loads a cell from the slice reference.

##### TvmSlice.loadRefAsSlice()

```TVMSolidity
TvmSlice slice;
TvmSlice refSlice = slice.loadRefAsSlice();
```

This function loads a cell from the slice reference and converts it into a slice.

##### TvmSlice.loadSigned()

```TVMSolidity
TvmSlice slice;
uint16 bitSize;
int number = slice.loadSigned(bitSize)
```

This function loads a signed integer with the given **bitSize** from the slice.

##### TvmSlice.loadUnsigned()

```TVMSolidity
TvmSlice slice;
uint16 bitSize;
uint number = slice.loadUnsigned(bitSize);
```

This function loads an unsigned integer with the given **bitSize** from the slice.

##### TvmSlice.loadTons()

```TVMSolidity
TvmSlice slice;
// init slice
uint128 value = slice.loadTons();
```

This function loads (deserializes) **VarUInteger 16** and return unsigned 128-bit integer. See [TL-B scheme][3].

##### TvmSlice.decodeFunctionParams()

```TVMSolidity
// Decode public function parameters
TvmSlice slice = ...;
(TypeA a, TypeB b, ...) = slice.decodeFunctionParams(functionName);

// Decode public constructor parameters
TvmSlice slice = ...;
(TypeA a, TypeB b, ...) = slice.decodeFunctionParams(ContractName);
```

This function decodes parameters of function or constructor if
contract type is provided. It's very convenient if there are many params
and they don't fit in one cell. This function is usually used in
**[onBounce](#onbounce)** function.

See example of how to use **onBounce** function:

* [onBounceHandler](https://github.com/tonlabs/samples/blob/master/solidity/16_onBounceHandler.sol)

#### TvmBuilder

TvmBuilder represents TVM type Builder. TON Solidity compiler defines the following functions to work with this type:

##### TvmBuilder.toSlice()

```TVMSolidity
TvmBuilder builder;
TvmSlice slice = builder.toSlice();
```

This function converts the builder into a Slice.

##### TvmBuilder.toCell()

```TVMSolidity
TvmBuilder builder;
TvmCell cell = builder.toCell();
```

This function converts the builder into a Cell.

##### TvmBuilder.bits()

```TVMSolidity
TvmBuilder builder;
uint16 bits = builder.bits();
```

This function returns the number of data bits already stored in the builder.

##### TvmBuilder.refs()

```TVMSolidity
TvmBuilder builder;
uint8 refs = builder.refs();
```

This function returns the number of references already stored in the builder.

##### TvmBuilder.bitsAndRefs()

```TVMSolidity
TvmBuilder builder;
(uint16 bits, uint8 refs) = builder.bitsAndRefs();
```

This function returns the number of data bits and references already stored in the builder.

##### TvmBuilder.remBits()

```TVMSolidity
TvmBuilder builder;
uint16 remBits = builder.remBits();
```

This function returns the number of data bits that can still be stored in the builder.

##### TvmBuilder.remRefs()

```TVMSolidity
TvmBuilder builder;
uint8 refRefs = builder.remRefs();
```

This function returns the number of references that can still be stored in the builder.

##### TvmBuilder.remBitsAndRefs()

```TVMSolidity
TvmBuilder builder;
(uint16 remBits, uint8 remRefs) = builder.remBitsAndRefs();
```

This function returns the number of data bits and references that can still be stored in the builder.

##### TvmBuilder.depth()

```TVMSolidity
TvmBuilder b;
uint64 d = b.depth();
```

Returns the depth of TvmBuilder **b**. If no cell references are stored
in **b**, then **d = 0**; otherwise **d** is one plus the maximum of
depths of cells referred to from **b**.

##### TvmBuilder.store()

```TVMSolidity
TvmBuilder builder;
builder.store(/*list_of_variables*/);
```

This function stores variables in the builder. Available types:

* integer
* address
* TvmSlice
* TvmBuilder
* TvmCell
* mapping
* struct
* array

Example:

```TVMSolidity
uint8 a;
int16 b;
TvmBuilder builder;
builder.store(a, b, uint(123132));
```

##### TvmBuilder.storeSigned()

```TVMSolidity
TvmBuilder builder;
int256 value;
uint16 bitSize;
builder.storeSigned(value, bitSize);
```

This function stores a signed integer with given **bitSize** in the builder.

##### TvmBuilder.storeUnsigned()

```TVMSolidity
TvmBuilder builder;
uint256 value;
uint16 bitSize;
builder.storeUnsigned(value, bitSize);
```

This function stores an unsigned integer with given **bitSize** in the builder.

##### TvmBuilder.storeRef()

```TVMSolidity
TvmBuilder builder;
TvmBuilder builder2;
builder.storeRef(builder2)
```

This function converts the argument builder into a cell and stores it in a reference of the builder.

See example of how to work with TVM specific types:

* [Message_construction](https://github.com/tonlabs/samples/blob/master/solidity/15_MessageSender.sol)
* [Message_parsing](https://github.com/tonlabs/samples/blob/master/solidity/15_MessageReceiver.sol)

##### TvmBuilder.storeTons()

```TVMSolidity
uint128 value = 1234;
TvmBuilder b;
b.storeTons(value);
```

This function stores (serializes) an integer **value** into **TvmBuilder b**. In builder the value are stored as
**VarUInteger 16**. See [TL-B scheme][3].

#### ExtraCurrencyCollection

ExtraCurrencyCollection represents TVM type ExtraCurrencyCollection. It has the same functions as **mapping(uint32 => uint256)**:

```TVMSolidity
ExtraCurrencyCollection curCol;
uint32 key;
uint256 value;
optional(uint32, uint256) res = curCol.min();
optional(uint32, uint256) res = curCol.next(key);
optional(uint32, uint256) res = curCol.prev(key);
optional(uint32, uint256) res = curCol.nextOrEq(key);
optional(uint32, uint256) res = curCol.prevOrEq(key);
optional(uint32, uint256) res = curCol.delMin();
optional(uint32, uint256) res = curCol.delMax();
optional(uint256) value = curCol.fetch(key);
bool exists = curCol.exists(key);
bool isEmpty = curCol.empty();
bool success = curCol.replace(key, value);
bool success = curCol.add(key, value);
optional(uint256) res = curCol.getSet(key, value);
optional(uint256) res = curCol.getAdd(key, value);
optional(uint256) res = curCol.getReplace(key, value);
uint256 value = curCol[index];
```

#### optional&lt;Type&gt;

The template optional type manages an optional contained value, i.e. a value that may or may not be present.

##### optional&lt;Type&gt;.hasValue()

```TVMSolidity
optional(uint) opt;
require(!opt.hasValue(), 101);
```

Checks whether **opt** contains a value.

##### optional&lt;Type&gt;.get()

```TVMSolidity
optional(uint) opt;
opt.set(123456);
require(opt.get() == 123456, 102);
```

If **opt** contains a value, returns a reference to the contained value.
Otherwise, throws an exception.

##### optional&lt;Type&gt;.set()

```TVMSolidity
optional(uint) opt;
opt.set(123456);
require(opt.get() == 123456, 102);
```

Replaces contents of **opt** with the contents of other.

##### optional&lt;Type&gt;.reset()

```TVMSolidity
optional(uint) opt;
opt.set(123456);
// do something with opt
opt.reset();
require(!opt.hasValue());
```

Delete contents of **opt**.

### TON specific control structures

#### repeat

```TVMSolidity
uint a = 0;
repeat(10) {
    a ++;
}
require(a == 10, 101);

// Despite a is changed in the cycle, code block will be repeated 10 times (10 is initial value of a)
repeat(a) {     
    a += 2;
}
require(a == 30, 102);

a = 11;
repeat(a - 1) {
    a -= 1;
}
require(a == 1, 103);
```

Allows to repeat block of code several times.
A **repeat** loop evaluates the expression only one time.
This expression must have any unsigned integer type.

#### struct

##### struct.unpack()

```TVMSolidity
    struct MyStruct {
        uint a;
        int b;
        address c;
    }

    function f() pure public {
        MyStruct s = MyStruct(1, -1, address(2));
        (uint a, int b, address c) = s.unpack();
    }
```

This method **unpack** all values stored in the struct.

#### bytes

##### operator[]

```TVMSolidity
bytes byteArray = "abba";
int index = 0;
byte a0 = byteArray[index];
```

Operator **[]** returns a byte located at position **index**.  
Warning: **index** must be in range 0 to 126 include.

##### bytes.length

```TVMSolidity
bytes byteArray = "abba";
uint l = byteArray.length;
```

Member **length** returns length of byte array.  
Warning: if length of array is bigger than 127 than this function return 127.

##### bytes.toSlice

```TVMSolidity
bytes byteArray = "abba";
TvmSlice s = byteArray.toSlice();
require(s.decode(uint8) == 97);
```

Function **toSlice** convert **bytes** to **TvmSlice**.  
Warning: if length of array is bigger than 127 than another bytes are
 stored in the first reference of slice. Use
 [TvmSlice.loadRef()](#tvmsliceloadref) to load that another bytes.

##### bytes.dataSize()

```TVMSolidity
bytes b = ...;
uint n = ...;
(uint cells, uint bits, uint refs) = b.dataSize(n);
```

Same as [TvmCell.dataSize()](#tvmcelldatasize).

#### bytes.dataSizeQ()

```TVMSolidity
TvmSlice s = ...;
uint n = ...;
optional(uint, uint, uint) size = b.dataSizeQ(n);
if (size.hasValue()) {
    (uint cells, uint bits, uint refs) = size.get();
}
```

Same as [TvmCell.dataSizeQ()](#tvmcelldatasizeq).

#### string

TON Solidity compiler expands **string** type with the following functions:

##### string.byteLength()

```TVMSolidity
string str
uint8 len = str.byteLength();
```

This function returns byte length of the string data.  
Warning: if length of string is bigger than 127 than this function return 127.

##### string.substr()

```TVMSolidity
string str;
uint8 from;
uint8 count;
string substr = str.substr(from, count);
```

This function returns a substring starting from the byte with number **from** with byte length **count**.  
Warning: **from** must be in range 0 to 127 include and **from + count** must be in range 1 to 127 include.

#### string(int)

```TVMSolidity
uint n = 123;
string b = string(n);
require(a == b, 101);
require("6465321365465" == string(6465321365465), 102);
require("-1113" == string(-1113));
```

TVM Solidity compiler allows to convert integer to decimal string.

#### hexstring()

```TVMSolidity
require(hexstring(0x7fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff) == "7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF", 101);
require(hexstring(255) == "FF", 102);
require(hexstring(-65535) == "-FFFF", 103);
require(hexstring(address.makeAddrStd(127,0x7fffffffffffffffffffffffffffffffffffffffffffffffff123456789abcde)) == "7F:7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF123456789ABCDE", 104);
```

This function allows to convert integer or address into a hex string.

#### format()

```TVMSolidity
string str = format("Hello {} 0x{:x} {}  {}.{} tons", 123, 255, address.makeAddrStd(-33,0x7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF123456789ABCDE), 100500, 32);
require(str == "Hello 123 0xFF -21:7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF123456789ABCDE  100500.32 tons", 101);
require(format("Hello {}", 123) == "Hello 123", 102);
require(format("Hello 0x{:x}", 123) == "Hello 0x7B", 103);
```

This function allows to build string with arbitrary parameters. Empty placeholder {} can be filled with integer
(in decimal view) or address. The only specified format is {:x} to fill with integer in hexadecimal view.  
**Note**\: total length of the string shouldn't exceed 127.  
This function is experimental feature, it can consume lots of gas, so better use it only for offchain execution.

#### stoi()

```TVMSolidity
uint res;
bool status;
(res, status) = stoi("123");
require(status, 111);
require(res == 123, 101);
string hexstr = "0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF123456789ABCDE";
uint num = 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF123456789ABCDE;
(res, status) = stoi(hexstr);
require(status, 112);
require(res == num, 102);
(res, status) = stoi("0xag");
require(!status, 116);
```

This function allows to convert a string into an integer. String is meant to be number in decimal format, only
if string starts with '0x' it will be converted from hexadecimal format. Function returns the integer, that can
be converted from **uint** to **int** and boolean status, which is false in case of illegal characters in th string.

#### address

**address** represents different types of TVM addresses: **addr_none**, **addr_extern** and **addr_std**. TON Solidity compiler expands **address** type with the following members and functions:

##### Object creating

##### constructor()

```TVMSolidity
uint address_value;
address addrStd = address(address_value);
```

This function constructs **address** of type **addr_std** with zero workchain id and given address value.

##### address.makeAddrStd()

```TVMSolidity
int8 wid;
uint address;
address addrStd = address.makeAddrStd(wid, address);
```

This function constructs **address** of type **addr_std** with given workchain id **wid** and value **address_value**.

##### address.makeAddrNone()

```TVMSolidity
address addrNone = address.makeAddrNone();
```

This function constructs **address** of type **addr_none**.

##### address.makeAddrExtern()

```TVMSolidity
uint addrNumber;
uint bitCnt;
address addrExtern = address.makeAddrExtern(addrNumber, bitCnt);
```

This function constructs **address** of type **addr_extern** with given **value** with **bitCnt** bit length.

##### Members

##### address.wid

```TVMSolidity
address addr;
int8 workchain_id = addr.wid;
```

This member of **address** type allows to obtain the workchain id of **addr_std**.

##### address.value

```TVMSolidity
address addr;
uint address_value = addr.value;
```

This member of **address** type allows to obtain the address value of **addr_std**.

#####  address.balance

```TVMSolidity
uint128 b = address(this).balance;
```

This member returns the balance of **this** contract in nanotons.

##### address.currencies

```TVMSolidity
ExtraCurrencyCollection cur = address(this).currencies;
```

This member returns currencies on the balance of **this** contract.

##### Functions

##### address.getType()

```TVMSolidity
address addr;
uint8 address_type = addr.getType();
```

This function returns type of the **address**:  
0 - addr_none
1 - addr_extern
2 - addr_std

##### address.isStdZero()

```TVMSolidity
address addr;
bool status = addr.isStdZero();
```

This function compares **address** with zero **address** of type **addr_std**.

##### address.isStdAddrWithoutAnyCast()

```TVMSolidity
address addr;
bool status = addr.isStdAddrWithoutAnyCast();
```

This function check that **addr** is **addr_std** without any cast.

##### address.isExternZero()

```TVMSolidity
address addr;
bool status = addr.isExternZero();
```

This function compares **address** with zero **address** of type **addr_extern**.

##### address.isNone()

```TVMSolidity
address addr;
bool status = addr.isNone();
```

This function returns true for **address** of type **addr_none**, otherwise returns false.

##### address.unpack()

```TVMSolidity
address addr;
(int8 wid, uint256 value) = addr.unpack();
```

This function unpacks **addr_std** and returns workchain id **wid** and address **value**.

##### address.transfer()

`<address>.transfer(uint128 value, ExtraCurrencyCollection currencies, bool bounce, uint16 flag, TvmCell body)`

Sends a internal outbound message to defined address. Function parameters:  
`value` - amount of nanotons sent to the address;  
`currencies` - additional currencies sent to the address;  
`bounce` - if it's set and transaction (generated by the internal outbound message) falls (only at computing phase, not at action phase!) than funds will be returned. Otherwise (flag isn't set or transaction terminated successfully) the address accepts the funds even if the account doesn't exist or is frozen;  
`flag` - sets flag which used to send the internal outbound message. See [TVM A.11.10][1] for more details.  
`body` -  body (payload) attached to the the internal message.

All parameters can be omitted, except ``value``. Default values for omitted parameters:
``currencies`` = empty ExtraCurrencyCollection  
``bounce`` = true  
``flag`` = 1  
``body``  = empty TvmCell

Example:

```TVMSolidity
address addr = ...;
uint128 value = ...;
bool bounce = ...;
uint16 flag = ...;
TvmCell body = ...;
ExtraCurrencyCollection c = ...;
addr.transfer(value);
addr.transfer(value, bounce);
addr.transfer(value, bounce, flag);
addr.transfer(value, bounce, flag, body);
addr.transfer(value, bounce, flag, body, c);
```

Another example:

```TVMSolidity
TvmCell cell = ...;
ExtraCurrencyCollection c = ...;
address destination = msg.sender;
destination.transfer({value: 1 ton, bounce: false, flag: 128, body: cell, currencies: c});
destination.transfer({value: 1 ton, bounce: false, flag: 128, body: cell});
destination.transfer({flag: 128 + 32});
destination.transfer({});
```

See example of usage `address.transfer()`:

* [giver](https://github.com/tonlabs/samples/blob/master/solidity/7_Giver.sol)

#### mapping

See example of how to work with mappings:

* [database](https://github.com/tonlabs/samples/blob/master/solidity/13_BankCollector.sol)
* [client](https://github.com/tonlabs/samples/blob/master/solidity/13_BankCollectorClient.sol)

TON Solidity compiler expands **mapping** type with the following functions.
In code examples below identifier **map** defines the object of **mapping(KeyType => ValueType)** type.

##### mapping.operator[]

```TVMSolidity
mapping(KeyType => ValueType) map;
...
KeyType key = ...;
ValueType value = map[key];
```

Returns the item of **value** with **key** key or returns a default value
if key is not in the mapping.

##### mapping.at()

```TVMSolidity
mapping(KeyType => ValueType) map;
...
KeyType key = ...;
ValueType value = map.at(key);
```

Returns the item of **value** with **key** key. Throws an exception if key
is not in the mapping.

##### mapping.min() and mapping.max()

```TVMSolidity
optional(KeyType, ValueType) minPair = map.min();
optional(KeyType, ValueType) maxPair = map.max();
if (minPair.hasValue()) {
    (KeyType key, ValueType value) = minPair.get(); // unpack optional value
    // using key and value
}
```

This function computes the minimal (maximal) key in the mapping and returns an optional value containing that key and associated value. If mapping is empty, this function returns an empty optional.

##### mapping.next() and mapping.prev()

```TVMSolidity
KeyType key;
// init key
optional(KeyType, ValueType) nextPair = map.next(key);
optional(KeyType, ValueType) prevPair = map.prev(key);

if (nextPair.hasValue()) {
    (KeyType nextKey, ValueType nextValue) = nextPair.get(); // unpack optional value
    // using nextKey and nextValue
}

mapping(uint8 => uint) m;
optional(uint8, uint) = m.next(-1); // ok, param for next/prev can be negative 
optional(uint8, uint) = m.prev(65537); // ok, param for next/prev can not possibly fit to KeyType (uint8 in this case)
```

This function computes the minimal (maximal) key in the mapping that is lexicographically greater (less) than **key** and returns an optional value containing that key and associated value. Returns an empty optional if there is no such key. If KeyType is an integer type, argument for this functions can not possibly fit KeyType.

##### mapping.nextOrEq() and mapping.prevOrEq()

```TVMSolidity
KeyType key;
optional(KeyType, ValueType) pair0 = map.nextOrEq(key);
optional(KeyType, ValueType) pair1 = map.prevOrEq(key);

mapping(uint8 => uint) m;
optional(uint8, uint) pair2 = m.nextOrEq(-1);
optional(uint8, uint) pair3 = m.prevOrEq(65537);
```

This function computes the minimal (maximal) key in the mapping that is lexicographically greater than or equal to (less than or equal to) **key** and returns an optional value containing that key and associated value. Returns an empty optional if there is no such key. If KeyType is an integer type, argument for this functions can not possibly fit KeyType.

##### mapping.delMin() and mapping.delMax()

```TVMSolidity
optional(KeyType, ValueType) v = map.delMin();
optional(KeyType, ValueType) v = map.delMax();
```

 If mapping is not empty then this function computes the minimal (maximum) key of the mapping, deletes that key and associated value from the mapping and returns an optional value containing that key and associated value. Returns an empty optional if there is no such key.

##### mapping.fetch()

```TVMSolidity
KeyType key;
optional(ValueType) optValue = map.fetch(key);
if (optValue.hasValue()) {
    ValueType value = optValue.get();
}
```

This function checks whether **key** presents in the mapping and returns an optional with the associated value. Returns an empty optional if there is no such key.

##### mapping.exists()

```TVMSolidity
KeyType key;
bool exists = map.exists(key);
```

This function returns a status flag whether **key** presents in the mapping.

##### mapping.empty()

```TVMSolidity
bool isEmpty = map.empty();
```

This function returns a status flag whether the mapping is empty.

##### mapping.replace()

```TVMSolidity
KeyType key;
ValueType value;
bool success = map.replace(key, value);
```

This function sets the value associated with **key** only if the **key** is present in the mapping.

##### mapping.add()

```TVMSolidity
KeyType key;
ValueType value;
bool success = map.add(key, value);
```

This function sets the value associated with **key** only if the **key** is not present in the mapping.

##### mapping.getSet()

```TVMSolidity
KeyType key;
ValueType value;
optional(ValueType) oldValue = map.getSet(key, value);
```

This function sets the **value** associated with **key**, but also
returns an optional with the **oldValue** associated with the **key**, if present. Otherwise it returns an empty optional.

##### mapping.getAdd()

```TVMSolidity
KeyType key;
ValueType value;
optional(ValueType) oldValue = map.getAdd(key, value);
```

This function sets the **value** associated with **key**, but only if **key** is not present in mapping. Returns an optional with the **oldValue** without changing the dictionary if that value presents in the mapping, otherwise returns an empty optional.

##### mapping.getReplace()

```TVMSolidity
KeyType key;
ValueType value;
optional(ValueType) oldValue = map.getReplace(key, value);
```

This function sets the **value** associated with **key**, but only if **key** is present in mapping. On success, returns the an optional with the **oldValue** associated with the **key**. Otherwise, returns an empty optional.

#### require, revert

In case of exception state variables of the contract are reverted to the state before
[tvm.commit()](#tvmcommit) or to the state of the contract before it was called.  
Use error codes that are greater than 100 because another error codes are
[reserved](https://docs.ton.dev/86757ecb2/p/3874d1-error-reference).  
**Note**: if not constant error code is passed as function argument and the error code is less than 2 then the error code is set to 100.


##### require

```TVMSolidity
uint a = 5;

require(a == 5); // ok
require(a == 6); // throw exception 100
require(a == 6, 101); // throw exception 101
require(a == 6, 101, "a is not equal to six"); // throw exception 101 and string
require(a == 6, 101, a); // throw exception 101 and number a
```

The **require** function can be used to check the condition and throw an exception if the condition is not met. The function takes condition and optional parameters: error code (unsigned integer) and any object.

##### revert

```TVMSolidity
uint a = 5;
revert(); // throw exception 100
revert(101); // throw exception 101
revert(102, "We have a some problem"); // throw exception 102 and string
revert(101, a); // throw exception 101 and number a
```

The **revert** function are used to trigger exceptions. The function takes an optional error code (unsigned integer) and some object.

#### Libraries

Libraries are similar to contracts, but they cannot have state variables
they cannot inherit nor be inherited. Libraries can be seen as implicit
base contracts of the contracts that use them. They will not be
explicitly visible in the inheritance hierarchy, but calls to library
functions look just like calls to functions of explicit base contracts
(using qualified access like `LibName.func(a, b, c)`). There is also
another way to call library function: `obj.func(b, c)`.  
For now libraries is stored as a part of the code of the contact that
uses libraries. In future it can be changed.

##### Function call via library name

Example of using library like `LibName.func(a, b, c)`:
```TVMSolidity
// file MathHelper.sol
pragma solidity >=0.6.0;

// Library declaration 
library MathHelper {
    // State variables are forbidden in library but constants are not
    uint constant MAX_VALUE = 300;

    // Library function
    function sum(uint a, uint b) internal pure returns (uint) {
        uint c = a + b;
        require(c < MAX_VALUE);
        return c;
    }
}


// file MyContract.sol
pragma solidity >=0.6.0;

import "MathHelper.sol";

contract MyContract {
    uint s;

    function addValue(uint value) public returns (uint) {
        s = MathHelper.sum(s, value);
        return s;
    }
}


```

##### Function call via object

In TON solidity **the arguments in a function passed by value not by
reference**. It's effective for numbers and even for huge arrays.
See ([TVM][1] - A.2.3.2).
**But if a library function is called like `obj.func(b, c)` then only the
first argument  `obj` is passed by reference.**  It's similar to
the `self` variable in Python.
The directive `using A for B;` can be used to attach library functions
(from the library `A`) to any type (`B`) in the context of a contract.
These functions will receive the object they are called on as their
first parameter.
The effect of `using A for *;` is that the functions from the library
`A` are attached to any type.

Example of using library like `obj.func(b, c)`:
```TVMSolidity
// file ArrayHelper.sol
pragma solidity >=0.6.0;

library ArrayHelper {
    // Delete the value from `array` at position `index`
    function del(uint[] array, uint index) internal pure {
        for (uint i = index; i + 1 < array.length; ++i){
            array[i] = array[i + 1];
        }
        array.pop();
    }
}


// file MyContract.sol
pragma solidity >=0.6.0;

import "ArrayHelper.sol";

contract MyContract {
    // Attach library function `del` to type `uint[]` 
    using ArrayHelper for uint[];

    uint[] array;

    constructor() public {
        array = [uint(100), 200, 300];
    }

    function deleteElement(uint index) public {
        // Library function call via object.
        // Note function library function `del` have 2 arguments.
        // array is passed by reference and index is passed by value
        array.del(index);
    }
}

```

### Pragmas

The `pragma` keyword is used to enable certain compiler features or checks.
A pragma directive is always local to a source file, so you have to add
the pragma to all your files if you want enable it in your whole project.
If you import another file, the pragma from that file does not
automatically apply to the importing file.

#### pragma ignoreIntOverflow

```TVMSolidity
pragma ignoreIntOverflow;
```

This pragma turns off binary operation result overflow check.

#### pragma AbiHeader

```TVMSolidity
pragma AbiHeader time;
pragma AbiHeader pubkey;
pragma AbiHeader expire;
```

This pragmas force message forming utility to fill an appropriate fields in the header of message to be sent to this contract:

* **pubkey** - public key by which the message was signed;
* **time**   - local time at what message was created;
* **expire** - time at which message should be meant as expired.

**pubkey** field is necessary for the contract to be able to check message signature which was generated with
public key that is different from what is stored in this contract data.
**time** and **expire** fields can be used for replay protection and if set they should be read in [afterSignatureCheck](#aftersignaturecheck) in case of not default replay protection.
To read more about this and ABI follow this [link](https://docs.ton.dev/86757ecb2/p/40ba94-abi-specification-v2).
Here is example of [message expiration time](https://docs.ton.dev/86757ecb2/p/88321a-message-expiration-time) usage.

#### pragma msgValue

```TVMSolidity
pragma msgValue 123456789;
pragma msgValue 1e8;
pragma msgValue 10 ton;
pragma msgValue 10_000_000_123;
```

This pragma allows to specify default value in nanotons attached to the
internal messages that contract sends to call another contract. If not
specified this value is set to 10 000 000 nanotons.

### State variables

#### Keyword `static`

Static state variables are used in generation origin state of the
contract. Such variables can be set on deploying contract from contract
(onchain) or by tvm-linker (offchain).

```TVMSolidity
contract C {
    uint static a; // ok
    // uint static b = 123; // error
}
```

See also:  
[Option `code` usage](#option-code-usage)  
[New contract address problem](#new-contract-address-problem)


### Special contract functions

##### receive

```TVMSolidity
contract Sink {
    uint counter = 0;
    receive() external payable {
        ++counter;
    }
```

On plain value transfer **receive** function is
called. See [address.transfer()](#addresstransfer)
If there is no **receive** function and **fallback** function exists than
**fallback** function is called.
If there are no **receive** and **fallback** functions, contract
does nothing on plain value transfer.
If you don't want the contract to receive plain value transfers, define
 **receive** function and throw exception in that function.

##### fallback

```TVMSolidity
contract Contr {
    uint counter = 0;
    fallback() external {
        ++counter;
    }
```

**fallback** function is called when body of the inbound message has invalid
function id.
If no **receive** function is defined and **fallback** function exists,
**fallback** function is called on plain value transfer. See [address.transfer()](#addresstransfer).


#### onBounce

```TVMSolidity
onBounce(TvmSlice body) external {
    /*...*/
}
```

**onBounce** function is executed if inbound internal message has bounced flag set. Parameter slice of onBounce function contains truncated body of the message (it's truncated by the network). If this function it not defined than on inbound internal message contract do nothing.

See example of how to use **onBounce** function:

* [onBounceHandler](https://github.com/tonlabs/samples/blob/master/solidity/16_onBounceHandler.sol)


#### onTickTock

```TVMSolidity
onTickTock(bool isTock) external {
    /*...*/
}
```

**onTickTock** function is executed on tick and tock transactions.
That transactions are automatically invoked for certain special accounts.
See ([TBLKCH][2] - 4.2.4.)
For tick transactions **isTock** is false, for tock transactions - true.


#### onCodeUpgrade

```TVMSolidity
function onCodeUpgrade() private {
    /*...*/
}
```

**onCodeUpgrade** function can have arbitrary set of arguments and should be executed after [tvm.setcode()](#tvmsetcode) function call. In this function [tvm.resetStorage()](#tvmresetstorage) should be called if the set of state variables is changed in the new version of the contract. This function implicitly calls [tvm.commit()](#tvmcommit). After return from **onCodeUpgrade** TVM execution is finished with exit code 0.

See example of how to upgrade code:

* [old contract](https://github.com/tonlabs/samples/blob/master/solidity/12_BadContract.sol)
* [new contract](https://github.com/tonlabs/samples/blob/master/solidity/12_NewVersion.sol)

#### afterSignatureCheck

```TVMSolidity
function afterSignatureCheck(TvmSlice body, TvmCell message) private inline returns (TvmSlice) {
    /*...*/
}
```

Developer can define **afterSignatureCheck** function to create his own replay protection function instead of default one.

See example of how to define this function:

* [Custom replay protection](https://github.com/tonlabs/samples/blob/master/solidity/14_CustomReplayProtection.sol)

### Function specifiers

#### Function mutability: pure, view and default

Function mutability shows how this function treats state variables.
Possible value of function mutability:

* `pure` - function can't read and assign state variables;
* `view` - function can read but can't assign state variables;
* default - function can read and assign state variables.

```TVMSolidity
contract Test {

    uint a;

    event MyEvent(uint val);

    // pure mutability
    function f() public pure {
        emit MyEvent(123);
    }

    // view mutability
    function g() public view {
        emit MyEvent(a);
    }

    // default mutability (not set)
    function e(uint newA) public {
        a = newA;
    }
}
```

#### Keyword inline

```TVMSolidity
function getSum(uint a, uint b) public returns (uint) {
    return sum(a, b);
}

function sum(uint a, uint b) private inline returns (uint) {
    return a + b;
}
```
The **inline** specifiers instruct the compiler to insert a copy of the function body into each place where the function is called.
Keyword can be used only for private and internal functions.

#### functionID()

```TVMSolidity
function functionName() public pure functionID(123) {
    /*...*/
}
 ```

This keyword allows to set identifier of the function manually.
Each public function has unique 32-bit id. If `functionID` is not used
than function id is calculated as hash of function signature.

### Events and return

#### extAddr

```TVMSolidity
emit EventName(arguments).extAddr(address);
emit EventName(arguments);
```

TON Solidity compiler allows to specify destination address of the message sent via event emitting using suffix **extAddr**. If **extAddr** suffix is not used, external address is set to **addr_none**.

#### return

```TVMSolidity
function f(uint n) public pure {
    return n <= 1? 1 : n * f(n - 1);
}
```

Public or external functions (called by external message) send an external message on return. Destination address of that message is the source address of the inbound external message.
For example, if function **f**  above was called with **n** = 5 by external message, only one external message is sent. Internal call of public or external function doesn't generate external message.

### External function calls

```TVMSolidity
interface IContract {
    function f(uint a) external;
}

contract Caller {
    function callExt(address addr) public {
        IContract(addr).f{value: 10 ton}(123);
        IContract(addr).f{value: 10 ton, flag: 3}(123);
        IContract(addr).f{value: 10 ton, bounce: true}(123);
        IContract(addr).f{value: 1 micro, bounce: false, flag: 128}(123);
        ExtraCurrencyCollection cc;
        cc[12] = 1000;
        IContract(addr).f{value: 10 ton, currencies:cc}(123);
    }
}
```

TON Solidity compiler allows to specify different parameters of the outbound internal message which is sent via external function call. `value`, `currencies`, `bounce` or `flag` options can be set (NOT `body` option). See [address.transfer()](#addresstransfer) where this options are described.

### API functions and members

#### **msg** namespace

##### msg.value

```TVMSolidity
uint128 value = msg.value;
```

The balance of inbound message in nanograms.

##### msg.currencies

```TVMSolidity
ExtraCurrencyCollection c = msg.currencies;
```

The collections of arbitrary currencies contained in balance of
inbound message.

##### msg.pubkey()

```TVMSolidity
uint256 pubkey = msg.pubkey();
```

This function returns sender's public key, obtained from the body if the external inbound message. If message is not signed function returns 0. If message is signed and message header ([pragma AbiHeader](#pragma-abiheader)) does not contain pubkey than `msg.pubkey()` is equal to `tvm.pubkey()`.

##### msg.createdAt

```TVMSolidity
uint32 created_at = msg.createdAt;
```

This member is a field **created_at** of the external inbound message.

##### msg.data

```TVMSolidity
TvmSlice slice = msg.data;
```

This member is a payload of the inbound message.

#### **tvm** namespace

##### TVM instructions

##### tvm.accept()

```TVMSolidity
tvm.accept()
```

This function executes TVM instruction "ACCEPT" ([TVM][1] - A.11.2. - F800). This instruction sets current gas limit to its maximal allowed value. This action is required to process external messages, which bring no value.

See example of how to use this function:

* [accumulator](https://github.com/tonlabs/samples/blob/master/solidity/1_Accumulator.sol)

##### tvm.commit()

```TVMSolidity
tvm.commit()
```

This function executes TVM instruction "COMMIT" ([TVM][1] - A.11.2. - F80F). This instruction commits the current state of registers c4 and c5 so that the current execution is considered “successful” with the saved values even if an exception is thrown later.

##### tvm.log()

```TVMSolidity
tvm.log(string)
logtvm(string)
```

This function executes TVM instruction "PRINTSTR" ([TVM][1] - A.12.2. - FEFn01ssss).
This command may be ignored if --without-logstr flag is presented in command line for compiler.

**logtvm** is an alias for tvm.log(string).

##### tvm.setcode()

```TVMSolidity
tvm.setcode(TvmCell newCode)
```

This function executes TVM instruction "SETCODE" ([TVM][1] - A.11.9. - FB04). This command creates an output action that would change this smart contract code to that given by Cell **newCode** (this change will take effect only after the successful termination of the current run of the smart contract).

See example of how to use this function:

* [old contract](https://github.com/tonlabs/samples/blob/master/solidity/12_BadContract.sol)
* [new contract](https://github.com/tonlabs/samples/blob/master/solidity/12_NewVersion.sol)

##### tvm.transLT()

```TVMSolidity
uint64 time = tvm.transLT();
```

This function executes TVM instruction "LTIME" ([TVM][1] - A.11.4. - F825). This command returns the logical time of the current transaction.

##### tvm.configParam()

```TVMSolidity
(TypeA a, TypeB b, ...) = tvm.configParam(uint8(paramNumber));
```

This function executes TVM instruction "CONFIGPARAM" ([TVM][1] - A.11.4. - F832). This command returns the value of the global configuration parameter with integer index paramNumber. Argument should be an integer literal. Supported paramNumbers: 1, 15, 17, 34.

##### tvm.rawConfigParam()

```TVMSolidity
(TvmCell cell, bool status) = tvm.rawConfigParam(paramNumber);
```

This function executes TVM instruction "CONFIGPARAM" ([TVM][1] - A.11.4. - F832). This command returns the value of the global configuration parameter with integer index paramNumber as a cell and boolean status.

##### tvm.rawReserve()
```TVMSolidity
tvm.rawReserve(111, 0);

ExtraCurrencyCollection col;
tvm.rawReserve(10 ton, col, 1);

col[1] = 3;
tvm.rawReserve(12 * 1e9, col, 2);
```

This function is a wrapper function for TVM instruction "RAWRESERVE" and "RAWRESERVEX". See [TVM][1].

##### Hashing and cryptography

##### tvm.hash()

```TVMSolidity
uint256 hash = tvm.hash(TvmCell cellTree);
uint256 hash = tvm.hash(string);
uint256 hash = tvm.hash(bytes);
```

This function executes TVM instruction "HASHCU" ([TVM][1] - A.11.6. - F900). It computes the representation hash of a given argument and returns it as a 256-bit unsigned integer

##### tvm.checkSign()

```TVMSolidity
uint256 hash;
uint256 SignHighPart;
uint256 SignLowPart;
uint256 pubkey;
bool signatureIsValid = tvm.checkSign(hash, SignHighPart, SignLowPart, pubkey);  // 1 variant

uint256 hash;
TvmSlice signature;
uint256 pubkey;
bool signatureIsValid = tvm.checkSign(hash, signature, pubkey);  // 2 variant

TvmSlice data;
TvmSlice signature;
uint256 pubkey;
bool signatureIsValid = tvm.checkSign(hash, signature, pubkey);  // 3 variant
```

This function executes TVM instruction "CHKSIGNU" ([TVM][1] - A.11.6. - F910) for variants 1 and 2. This command checks the Ed25519-signature of a **hash** using public key **pubkey**. Signature is represented by two uint256 **SignHighPart** and **SignLowPart** in the first variant and by a slice **signature** in the second variant.
In the third variant this function executes TVM instruction "CHKSIGNS" ([TVM][1] - A.11.6. - F911). This command checks Ed25519-signature of **data** using public key **pubkey**. Signature is represented by a slice **signature**.

##### Deploy contract from contract

##### tvm.insertPubkey()

```TVMSolidity
TvmCell stateInit;
uint256 pubkey;
TvmCell stateInitWithKey = tvm.insertPubkey(stateInit, pubkey);
```

This function inserts a public key into contract's data field.

##### tvm.buildStateInit()

```TVMSolidity
TvmCell code;
TvmCell data;
TvmCell stateInit = tvm.buildStateInit(code, data);
```

This function generates a StateInit ([TBLKCH][2] - 3.1.7.) from code and data cells.

##### tvm.buildEmptyData()

```TVMSolidity
uint256 publicKey = 0x12345678;
TvmCell data = tvm.buildEmptyData(publicKey);
```

This function generates a persistent storage of the contract that
contains only public key. **data** can be used to generate StateInit
 ([TBLKCH][2] - 3.1.7.).

##### tvm.deploy()

```TVMSolidity
TvmCell stateInit;
address addr;
uint128 value;
TvmCell payload;
tvm.deploy(stateInit, addr, value, payload);
```

This function implements "Create smart contract by a smart contract" functionality. It generates and sends a constructor message to create a new contract.

Arguments:  
stateInit   - contract's StateInit;  
addr        - address of the contract;  
value       - amount of currency in nano tons that will be sent to the new contract address;  
payload     - encoded message of constructor call.

* [Contract_deployer](https://github.com/tonlabs/samples/blob/master/solidity/11_ContractDeployer.sol)


##### Deploy via new

When you deploy a contract from contract via keyword `new` than either
option `code` or option `stateInit` must be set. `stateInit` is a struct
that contains original state of contract. `stateInit` contains `data`,
`code` and another members. See also ([TBLKCH][2] - A.2.3.2) about
 `stateInit`.

Use option `stateInit` if you have created account state (maybe offchain
or onchain). And used `code` if want create account state in `new`
expression.

**Note**: Address of the new account is calculated as hash of the `stateInit`.
Constructor function parameters don't influence the address. See [New contract address problem](#new-contract-address-problem).

Detailed description can be found in [doc](https://github.com/tonlabs/samples/blob/master/solidity/17_ContractProducer.md).  
Example can be found in the samples repo [WalletProducer](https://github.com/tonlabs/samples/blob/master/solidity/17_ContractProducer.sol).

##### Option `stateInit` usage

```TVMSolidity
TvmCell stateInit = ...;
address newWallet = new SimpleWallet{value: 1 ton, stateInit: stateInit}(arg0, arg1, ...);
```

Option `stateInit` defines origin state of the new account.

##### Option `code` usage

```TVMSolidity
TvmCell code = ...;
address newWallet = new SimpleWallet{value: 1 ton, code: code}(arg0, arg1, ...);
```

Option `code` defines code of the new contract.

This options can be used only with `code` option:

* `pubkey` (`uint256`) - defines public key of the new contract
* `varInit` (`initializer list`) - used to set public variables of the new contract.

Example of using that options:

```TVMSolidity
TvmCell code = ...;
address newWallet = new SimpleWallet{
    value: 1 ton,
    code: code,
    pubkey: 0xe8b1d839abe27b2abb9d4a2943a9143a9c7e2ae06799bd24dec1d7a8891ae5dd,
    varInit: {m_owner: 111, m_value: 15}
}(arg0, arg1, ...);
```

##### Another deploy options

There are another deploy options:

* `value` (`uint128`) - funds attached to the outbound internal message, that
creates new account. This value must be set.
* `wid` (`uint8`) - workchain id of the new account address.
By default initialized to `0`.
* `flag` (`uint16`) - flag used to send the outbound internal message.
By default initialized to `1`. See opcode `SENDRAWMSG` ([TVM][1] -
A.11.10).
This options can be used with `stateInit` and `code` options.

```TVMSolidity
TvmCell stateInit = ...;
address newWallet = new SimpleWallet{
    stateInit: stateInit,
    value: 1 ton,
    wid: -1,
    flag: 0
}(arg0, arg1, ...);
```

##### New contract address problem

Address of the new account is calculated as hash of the `stateInit`.
Parameters of constructor don't influence the address. The problem
is that hacker can deploy the contract with your `stateInit` before you
with malicious constructor parameters.

Let's consider how to protect against this problem:

1. Constructor is called by external message.  
We must check that we didn't forget to set public key in the contract and the
inbound message is signed by that key. If hacker doesn't have your private
key than he can't sign message to call the constructor.  
See [constructor of WalletProducer](https://github.com/tonlabs/samples/blob/master/solidity/17_ContractProducer.sol).
2. Constructor is called by internal message.  
We should define static variable in the new contract that will contain
address of the creator. Address of the creator will be a part of the `stateInit`.
And in the constructor we must check address of the message sender.  
See [function `deployWallet` how to deploy contract](https://github.com/tonlabs/samples/blob/master/solidity/17_ContractProducer.sol).  
See [constructor of SimpleWallet](https://github.com/tonlabs/samples/blob/master/solidity/17_SimpleWallet.sol).  
If some contract should deploy plenty of contracts (with some contract's
public key) than it's a good idea to declare static variable in the deployed
contract. This variable can contain some sequence number. It will allow
each new contact to have unique `stateInit`.
See [SimpleWallet](https://github.com/tonlabs/samples/blob/master/solidity/17_SimpleWallet.sol).  
**Note**: contract's public key (`tvm.pubkey()`) is a part of `stateInit`.

##### Misc functions from `tvm`

##### tvm.pubkey()

```TVMSolidity
uint256 pubkey = tvm.pubkey();
```

This function returns contract's public key, stored in contract data. If key is not set function returns 0.

##### tvm.setCurrentCode()

```TVMSolidity
TvmCell newCode;
tvm.setCurrentCode(newCode);
```

This function changes this smart contract current code to that given by Cell **newCode**.

See example of how to use this function:

* [old contract](https://github.com/tonlabs/samples/blob/master/solidity/12_BadContract.sol)
* [new contract](https://github.com/tonlabs/samples/blob/master/solidity/12_NewVersion.sol)

##### tvm.resetStorage()

```TVMSolidity
tvm.resetStorage();
```

This function resets all state variables to their default values.

##### tvm.functionId()

```TVMSolidity
// id of public function
uint32 funcID = tvm.functionId(functionName);

// id of public constructor
uint32 funcID = tvm.functionId(ContractName);
```

This function returns function id (uint32) for public/external function
or constructor.  
Example:

```TVMSolidity
contract MyContract {
    constructor(uint a) public {
    }
        /*...*/
    }
    
    function f() public pure returns (uint) {
        /*...*/
    }
    
    function getConstructorID() public pure returns (uint32) {
        uint32 functionId = tvm.functionId(MyContract);
        return functionId;
    }
    
    function getFuncID() public pure returns (uint32) {
        uint32 functionId = tvm.functionId(f);
        return functionId;
    }
}
```

See example of how to use this function:

* [onBounceHandler](https://github.com/tonlabs/samples/blob/master/solidity/16_onBounceHandler.sol)

##### tvm.encodeBody()

```TVMSolidity
TvmCell body = tvm.encodeBody(function_name, arg0, arg1, arg2, ...);
```

This function constructs a function call message body that can be used
as the payload for [address.transfer()](#addresstransfer).  
Example:

```TVMSolidity
interface Remote {
    function func(uint256 num, address a, int64 num2) public pure;
}

contract Caller {
    function test() public pure {
        TvmCell body = tvm.encodeBody(Remote.func, 123, address.makeAddrStd(22, 333), -654);
        msg.sender.transfer({value:1e10, body:body});
    }
}
```

##### tvm.exit() and tvm.exit1()

```TVMSolidity
function g0(uint a) private {
    if (a == 0) {
        tvm.exit();
    }
    //...
}

function g1(uint a) private {
    if (a == 0) {
        tvm.exit1();
    }
    //...
}
```

That functions are used to save state variables and to quick terminate
execution of smart contract.  
Exit codes are equal to zero and one for `tvm.exit` and `tvm.exit1`
respectively.

#### **math** namespace

##### math.min() and math.max()

```TVMSolidity
int min = math.min(int a, int b, ...);
int max = math.max(int a, int b, ...);
uint min = math.min(uint a, uint b, ...);
uint max = math.max(uint a, uint b, ...);
```

This function returns the minimal (maximal) value of the passed arguments.

##### math.minmax()

```TVMSolidity
(uint a, uint b) = math.minmax(20, 10); // (10, 20)
```

Returns min and max value.

##### math.abs()

```TVMSolidity
int a = math.abs(-4123); // 4123
int b = -333;
int c = math.abs(b); // 333
```

This function computes the absolute value of given integer.

##### math.modpow2()

```TVMSolidity
uint constant pow = 12;
uint val = 12313;
uint a = math.modpow2(val, 10);
uint b = math.modpow2(val, pow);
```

This function computes the value modulo 2^(second argument). Note that second argument should be a constant integer.

##### math.divr() math.divc()

```TVMSolidity
int c = math.divc(10, 3); // 4
int c = math.divr(10, 3); // 3
```

This functions return result of dividing two integers.
The return value is rounded.  
Round mode "nearest integer" is used for `divr`.  
Round mode "ceiling" is used for `divc`.

##### math.muldiv() math.muldivr() math.muldivc()

```TVMSolidity
require(math.muldiv(3, 7, 2) == 10);
require(math.muldivr(3, 7, 2) == 11);
require(math.muldivc(3, 7, 2) == 11);
```

This functions multiplies two values and then divides the result by a third value. The return value is rounded.  
Round mode "floor" is used for `muldiv`.  
Round mode "nearest integer" is used for `muldivr`.  
Round mode "ceiling" is used for `muldivc`.  
See also ([TVM][1] - cf. 1.5.6) about the round modes.

##### math.muldivmod()

```TVMSolidity
uint a = 3;
uint b = 2;
uint c = 5;
(uint d, uint r) = math.muldivmod(a, b, c);
int e = -1;
int f = 3;
int g = 2;
(int h, int p) = math.muldivmod(e, f, g);
```

This function executes TVM instruction "MULDIVMOD" ([TVM][1] - A.5.2. - A98C). This instruction multiplies first two arguments, divides the result by third argument and returns the result and the remainder. Intermediate result is stored in 514 bit buffer, and final result is rounded to the floor.

##### **tx** namespace

##### tx.timestamp

```TVMSolidity
uin64 t = tx.timestamp;
```

Returns the logical time of the current transaction.

##### **block** namespace

##### block.timestamp

```TVMSolidity
uin64 t = block.timestamp;
```

Returns the starting logical time of the current block.

##### **rnd** namespace

The pseudorandom number generator uses the random seed. The
initial value of the random seed before a smart contract is executed in
TON Blockchain is a hash of the smart contract address and the global
block random seed. If there are several runs of the same smart contract
inside a block, then all of these runs will have the same random seed.
This can be fixed, for example, by running `rnd.shuffle()` (without
parameters) each time before using the pseudorandom number generator.

##### rnd.next

```TVMSolidity
// (1)
uint256 r0 = rnd.next(); // 0..2^256-1
// (2) 
uint8 r1 = rnd.next(100);  // 0..99
int8 r2 = rnd.next(int8(100));  // 0..99
int8 r3 = rnd.next(int8(-100)); // -100..-1
```

Generates a new pseudo-random number.  
(1) Returns `uint256` number.  
(2) If first function argument `x > 0` than it returns the value in the
range `0..x-1`. Else if `x < 0` than returned the value is in range
`x..-1`. Else if `x==0` than it returns `0`.

##### rnd.getSeed

```TVMSolidity
uint256 seed = rnd.getSeed();
```

Returns the current random seed.

##### rnd.setSeed

```TVMSolidity
uint256 x = ...;
rnd.setSeed(x);
```

Sets the random seed to `x`.

##### rnd.shuffle

```TVMSolidity
// (1)
uint256 someNumber = ...;
rnd.shuffle(someNumber);
// (2)
rnd.shuffle();
```

Randomizes the random seed.  
(1) Mixes the random seed and `someNumber`. The result is set as the
random seed.  
(2) Mixes the random seed and the logical time of the current transaction.
The result is set as the random seed.

##### selfdestruct

```TVMSolidity
address dest_addr = msg.sender;
selfdestruct(dest_addr);
```

Create and send the message that carry all the remaining balance
of the current smart contract and destroy the current account.

See example of how to use **selfdestruct** function:
* [Kamikaze](https://github.com/tonlabs/samples/blob/master/solidity/8_Kamikaze.sol)


[1]: https://ton.org/tvm.pdf        "TVM"
[2]: https://ton.org/tblkch.pdf     "TBLKCH"
[3]: https://github.com/ton-blockchain/ton/blob/master/crypto/block/block.tlb "TL-B scheme"
