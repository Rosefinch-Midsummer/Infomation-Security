# Solidity基础

<!-- toc -->

## Remix，Solidity编译器和开源协议

- [开源软件许可协议简介](https://developer.aliyun.com/article/25089)
- [EVM（以太坊虚拟机） 介绍](https://ethereum.org/zh/developers/docs/evm)
    - [EVM 版本](https://docs.soliditylang.org/en/v0.8.21/using-the-compiler.html)
- [Solidity 编译器介绍](https://docs.soliditylang.org/zh/v0.8.16/using-the-compiler.html)
- [Solidity 官方文档](https://docs.soliditylang.org/zh/v0.8.16/index.html)

### [开源协议网站spdx](https://spdx.dev/)

An open standard capable of representing systems with software components in as SBOMs (Software Bill of Materials) and other AI, data and security references supporting a range of risk management use cases.

The SPDX specification is a freely available international open standard (ISO/IEC 5692:2021).

### Remix

Remix编译器是一个基于Web的以太坊智能合约开发工具，提供了在线编辑、编译、调试和部署智能合约的功能。Remix编译器有几个版本，每个版本提供了不同的功能和特性，以下是关于几个常见版本的介绍：

1. Remix IDE：Remix IDE是最常见的版本，是一个功能齐全的在线IDE，包括编辑器、编译器、调试器和部署者等功能。Remix IDE支持Solidity智能合约的编写和编译，同时还提供了交互式调试和测试合约的功能。

2. Remix Alpha：Remix Alpha是一个基于JavaScript的轻量级编辑器，专注于提供简单的合约编辑和快速编译的功能。Remix Alpha适用于快速原型开发和简单合约编写。

3. Remixd：Remixd是一个独立的后端服务，用于在本地编写智能合约并与Remix IDE进行交互。通过Remixd，用户可以在本地编辑器中编写合约，并将更改同步到Remix IDE中进行编译和调试。

4. Remix Desktop：Remix Desktop是一个基于Electron框架构建的桌面应用程序，集成了Remix IDE的功能，并支持通过本地文件系统访问和编辑智能合约。Remix Desktop提供了更好的性能和用户体验，适合于在本地环境中进行智能合约开发。

不同版本的Remix编译器适用于不同的开发需求和环境，用户可以根据自己的需求选择合适的版本进行智能合约开发和调试。

### 基本代码

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract HelloWorld {
    string strVar = "Hello World";
    function sayHello() public view returns(string memory){
        return addInfo(strVar);
    }
    function sayHelloWorld(string memory newString) public {
        strVar = newString;
    }
    function addInfo(string memory helloWorldStr) internal pure returns(string memory){
        return string.concat(helloWorldStr, " from Trump's contact.");
    }
}
```


## Solidity 基础数据类型

- [Solidity 类型官方文档](https://docs.soliditylang.org/zh/v0.8.16/types.html#)
- [Bytes vs bytes32](https://ethereum.stackexchange.com/questions/11770/what-is-the-difference-between-bytes-and-bytes32)


Solidity 是一种高级智能合约编程语言，适用于以太坊平台上的智能合约开发。Solidity 支持多种基本数据类型，以下是 Solidity 中常用的基础数据类型及其详细介绍：

1. 布尔类型（bool）：布尔类型表示 true 或 false 值，只有两个可能的取值。

2. 整数类型：Solidity 支持有符号和无符号的整数类型，包括 int、uint、uint8 到 uint256（步长为 8，即 uint8、uint16、uint24 等）及 int8 到 int256。int 类型表示带符号整数，uint 类型表示无符号整数。

3. 固定点数类型：Solidity 支持固定点数类型用以表示小数值，包括 fixed 和 ufixed 类型。例如 fixed128x18 表示带符号固定点数，共有 128 位，小数点后有 18 位。

4. 地址类型（address）：地址类型用于存储以太坊账户地址。在合约中，可以使用 address 类型来处理以太坊地址。

5. 字符串类型（string）：字符串类型用于存储 UTF-8 编码的字符串数据。

6. 字节类型（bytes）：字节类型是一个动态大小的字节数组，可以用来存储二进制数据。

7. 数组类型：Solidity 支持多种数组类型，如定长数组（如 uint[5]），动态数组（如 uint[]）和多维数组。

8. 枚举类型（enum）：枚举类型用于定义一组有限的命名常数。

9. 其他特殊类型：还包括合约类型（contract）用于实例化合约对象、元组类型（tuple）、映射类型（mapping）用于键值对存储等。

以上是 Solidity 中常用的基础数据类型，了解这些数据类型将有助于开发人员正确声明和使用在智能合约中的变量和函数。

bool、unit、int、bytes32、address，基础数据类型不需要指定存储方式。

string需要指定存储方式。

array默认是storage。
## Solidity 函数


- [智能合约结构](https://docs.soliditylang.org/zh/v0.8.17/layout-of-source-files.html)
- [如何拼接两个string变量（英文）](https://medium.com/@jamaltheatlantean/how-to-concatenate-two-strings-using-solidity-fada6051b1a6)

下面是一个简单的 Solidity 合约示例，展示了如何声明和定义函数，以及如何在函数中处理数据：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleContract {
    // 状态变量
    uint public data;

    // 构造函数
    constructor() {
        data = 0;
    }

    // 函数：增加数据
    function addData(uint _value) public {
        data += _value;
    }

    // 函数：获取数据
    function getData() public view returns (uint) {
        return data;
    }

    // 函数：重置数据
    function resetData() public {
        data = 0;
    }
}
```

在上述示例中，我们定义了一个简单的 Solidity 合约 SimpleContract。该合约包含了以下几个部分：

1. **状态变量**：在合约中声明了一个 `uint` 类型的状态变量 `data`，用于存储数据。

2. **构造函数**：合约的构造函数在合约创建时会自动执行，用于初始化合约的状态变量。在本例中，构造函数将 `data` 初始化为 `0`。

3. **函数**：合约中包含了三个函数，分别实现了增加数据、获取数据和重置数据的功能。
   - `addData(uint _value)`：接受一个 `uint` 类型的参数 `_value`，并将其加到 `data` 上。
   - `getData()`：返回当前 `data` 的值，使用 `view` 关键字表示该函数只读取合约状态而不改变它。
   - `resetData()`：重置 `data` 为 `0`。

通过这些函数，可以实现对合约中状态变量 `data` 的修改和查询。在 Solidity 合约中，函数的定义可以包括访问修饰符、参数列表、返回值、函数体等内容，开发人员根据需求定义不同功能的函数以实现智能合约的逻辑。

## Solidity 存储模式：memory, storage, calldata


这一节知识是底层原理，不需要完全理解也可以继续学习，这部分英文文档会更加清晰。

- [EVM底层数据存储原理（英文）](https://www.netspi.com/blog/technical/blockchain-penetration-testing/ethereum-virtual-machine-internals-part-2/)
    - [storage存储方式](https://docs.soliditylang.org/en/v0.8.24/internals/layout_in_storage.html)
    - [memory存储方式](https://docs.soliditylang.org/en/v0.8.24/internals/layout_in_memory.html)
    - [calldata存储方式](https://docs.soliditylang.org/en/v0.8.24/internals/layout_in_calldata.html)


Solidity 存储模式是指 Solidity 合约中数据的存储和布局方式。了解 Solidity 存储模式对于理解智能合约的内部工作原理和有效管理合约中的数据非常重要。以下是 Solidity 存储模式的详细介绍：

1. **状态变量存储模式**：
   - Solidity 合约中声明的状态变量默认存储在以太坊区块链中。
   - 每个状态变量都有自己的存储位置，可以通过变量名来访问。
   - 存储的数据占用以太坊网络的存储空间，需要消耗一定的 Gas（燃料）费用。
   - 状态变量的存储位置在合约的存储空间中是持久化的，即数据会保存在区块链中。

2. **内部变量存储模式**：
   - 在函数内声明的变量是内部变量，存储在内存中而不是区块链上。
   - 内部变量的生存周期仅限于函数的执行过程，函数执行完毕后变量的值会被销毁。
   - 内部变量不会产生永久性存储开销，因此 Gas 消耗较低。

3. **引用类型存储模式**：
   - 引用类型（数组、结构体、映射等）的存储方式涉及到数据复制或引用操作。
   - 对于数组和结构体等复杂数据类型，其存储方式取决于类型的大小和复杂程度。
   - 大型数组或结构体的存储操作可能引起 Gas 成本增加，因为复制或引用操作会占用更多资源。

4. **存储和内存关键字**：
   - Solidity 提供了 `storage` 和 `memory` 关键字，可以用来指定变量是存储在区块链上还是内存中。
   - `storage` 关键字用于表示将数据存储在区块链中（状态变量）。
   - `memory` 关键字用于表示将数据存储在内存中（函数内部变量）。

总的来说，Solidity 存储模式需要根据合约的具体需求和数据大小来选择合适的存储方式。合理使用状态变量、内部变量和引用类型，并正确管理存储位置，有助于优化合约的 Gas 消耗和合约性能。对 Solidity 存储模式的理解是 Solidity 开发人员必备的基础知识之一。

**storage、memory、calldata、stack、codes、logs，前三种是重点**

类型|特点
-|-
storage|永久，默认
memory|暂时，充当函数可修改参数
calldata|暂时，充当函数不可修改参数，修改报错


## Solidity 基础数据结构：结构体，数组和映射


Solidity 官方文档中，关于数据和结构体，英文文档比中文文档在定义上表述更清晰。

- [数据结构 - 数组（英文）](https://docs.soliditylang.org/en/v0.8.24/types.html#arrays)
    - [数据结构 - 数组（中文对照）](https://docs.soliditylang.org/zh/v0.8.17/types.html#arrays)
- [数据结构 - 结构体（英文）](https://docs.soliditylang.org/en/v0.8.24/types.html#structs)
    - [数据结构 - 结构体（中文对照）](https://docs.soliditylang.org/zh/v0.8.17/types.html#structs)

### 基本数据结构

Solidity 中的基础数据结构包括结构体（struct）、数组（array）和映射（mapping），它们用于组织和存储数据。以下是对这些数据结构的详细介绍：

1. **结构体（struct）**：
   - 结构体是一种用户定义的数据结构，用于存储多个不同类型的数据。
   - 结构体可以包含多个成员变量，每个成员变量可以是不同的数据类型。
   - 结构体的定义使用 `struct` 关键字，类似于面向对象编程中的类。
   - 示例：
     ```solidity
     struct Person {
         string name;
         uint age;
     }
     ```
   - 在合约中可以实例化结构体，并访问结构体的成员变量。

2. **数组（array）**：
   - 数组是一组相同类型的数据元素的集合。
   - 数组可以是定长数组或动态数组。定长数组在声明时指定长度，动态数组可以动态增加或减少其长度。
   - 数组的元素可以通过索引来访问。
   - Solidity 支持单维和多维数组。
   - 示例：
     ```solidity
     uint[] public numbers; // 动态数组
     uint[3] public fixedNumbers; // 定长数组
     ```
   - 数组在合约中常用于存储列表、集合或序列的数据。

3. **映射（mapping）**：
   - 映射是一种键值对的数据结构，类似于字典或哈希表。
   - 映射在 Solidity 中用于快速查找和存储键值对数据。
   - 映射的键和值可以是任意数据类型。
   - 映射的定义使用 `mapping` 关键字。
   - 示例：
     ```solidity
     mapping(address => uint) public balances; // 地址到 uint 的映射
     ```
   - 映射常用于存储账户余额、数据索引等键值对数据。

结构体、数组和映射是 Solidity 中常用的基础数据结构，它们可以灵活应用于智能合约的数据组织和存储需求。合约开发者可以根据实际情况选择合适的数据结构，设计出高效和清晰的智能合约。对这些基础数据结构的深入了解和灵活运用是 Solidity 开发过程中的关键之一。

### 基本代码

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract HelloWorld {
    string strVar = "Hello World";
    function sayHello() public view returns(string memory){
        return addInfo(strVar);
    }
    function sayHelloWorld(string memory newString) public {
        strVar = newString;
    }
    function addInfo(string memory helloWorldStr) internal pure returns(string memory){
        return string.concat(helloWorldStr, " from Trump's contract.");
    }
}
```

msg 环境变量，有msg.value、msg.sender


结构体和数组的使用

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract HelloWorld {
    string strVar = "Hello World";

    struct Info {
        string phrase;
        uint256 id;
        address addr;
    }

    Info[] infos;

    function sayHello(uint256 _id) public view returns(string memory){
        for(uint256 i = 0; i < infos.length; i++){
            if(infos[i].id == _id){
                return addInfo(infos[i].phrase);
            }
        }
        return addInfo(strVar);
    }
    function setHelloWorld(string memory newString, uint256 _id) public {
        Info memory info = Info(newString,_id,msg.sender);
        infos.push(info);
    }
    function addInfo(string memory helloWorldStr) internal pure returns(string memory){
        return string.concat(helloWorldStr, " from Trump's contract.");
    }
}
```

mapping和struct的使用

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract HelloWorld {
    string strVar = "Hello World";

    struct Info {
        string phrase;
        uint256 id;
        address addr;
    }
    
    // mapping(uint256 => Info) infoMapping;
    mapping(uint256 id => Info infos) infoMapping;

    function sayHello(uint256 _id) public view returns(string memory){
        if(infoMapping[_id].addr == address(0x0)){
            return addInfo(strVar);
        }else{
            return addInfo(infoMapping[_id].phrase);
        }
    }
    function setHelloWorld(string memory newString, uint256 _id) public {
        Info memory info = Info(newString,_id,msg.sender);
        infoMapping[_id] = info;
    }
    function addInfo(string memory helloWorldStr) internal pure returns(string memory){
        return string.concat(helloWorldStr, " from Trump's contract.");
    }
}
```



## 合约间交互：工厂模式


- [Solidity 工厂模式介绍](https://learnblockchain.cn/article/1952)
- [如何使用工厂模式（英文）](https://betterprogramming.pub/learn-solidity-the-factory-pattern-75d11c3e7d29)
- [Solidity中的工厂模式（英文）](https://medium.com/@solidity101/demystifying-the-factory-pattern-in-solidity-efficient-contract-deployment-with-factory-pattern-e233ea6d1ec0#:~:text=Understanding%20the%20Factory%20Pattern&text=In%20the%20context%20of%20Ethereum,with%20predefined%20functionalities%20and%20structures.)


### 合约引入

在 Solidity 中，可以通过引入（import）其他合约来重用已有的代码逻辑和功能。

Solidity 引入在线合约。

以下是一个使用引入合约的简单示例：

假设有两个 Solidity 合约：`ContractA.sol` 和 `ContractB.sol`，现在我们想在 `ContractA.sol` 中引入 `ContractB.sol`。

1. **ContractB.sol**：
```solidity
// ContractB.sol
pragma solidity ^0.8.0;

contract ContractB {
    uint public data;

    function setData(uint _value) public {
        data = _value;
    }

    function getData() public view returns (uint) {
        return data;
    }
}
```

2. **ContractA.sol**：
```solidity
// ContractA.sol
pragma solidity ^0.8.0;

// 引入ContractB.sol
import "./ContractB.sol";

contract ContractA {
    ContractB contractBInstance;

    constructor() {
        contractBInstance = new ContractB();
    }

    function setDataInB(uint _value) public {
        contractBInstance.setData(_value);
    }

    function getDataFromB() public view returns (uint) {
        return contractBInstance.getData();
    }
}
```

在上述示例中，我们做了如下操作：
- 在 `ContractA.sol` 中使用 `import "./ContractB.sol";` 引入了 `ContractB.sol`，使得 `ContractA.sol` 可以访问 `ContractB.sol` 中的合约定义。
- 在 `ContractA` 合约的构造函数中创建了一个 `ContractB` 的实例 `contractBInstance`。
- 在 `setDataInB` 函数中，调用了 `ContractB` 实例的 `setData` 函数，设置了数据。
- 在 `getDataFromB` 函数中，调用了 `ContractB` 实例的 `getData` 函数，获取了数据。

通过引入合约的方式，可以将代码逻辑模块化，提高代码的可读性和可维护性。在 Solidity 中，引入合约是一种常见的代码复用技术，有助于降低代码重复度并提高开发效率。在 Solidity 中，可以通过引入（import）其他合约来重用已有的代码逻辑和功能。以下是一个使用引入合约的简单示例：

假设有两个 Solidity 合约：`ContractA.sol` 和 `ContractB.sol`，现在我们想在 `ContractA.sol` 中引入 `ContractB.sol`。

1. **ContractB.sol**：
```solidity
// ContractB.sol
pragma solidity ^0.8.0;

contract ContractB {
    uint public data;

    function setData(uint _value) public {
        data = _value;
    }

    function getData() public view returns (uint) {
        return data;
    }
}
```

2. **ContractA.sol**：
```solidity
// ContractA.sol
pragma solidity ^0.8.0;

// 引入ContractB.sol
import "./ContractB.sol";

contract ContractA {
    ContractB contractBInstance;

    constructor() {
        contractBInstance = new ContractB();
    }

    function setDataInB(uint _value) public {
        contractBInstance.setData(_value);
    }

    function getDataFromB() public view returns (uint) {
        return contractBInstance.getData();
    }
}
```

在上述示例中，我们做了如下操作：
- 在 `ContractA.sol` 中使用 `import "./ContractB.sol";` 引入了 `ContractB.sol`，使得 `ContractA.sol` 可以访问 `ContractB.sol` 中的合约定义。
- 在 `ContractA` 合约的构造函数中创建了一个 `ContractB` 的实例 `contractBInstance`。
- 在 `setDataInB` 函数中，调用了 `ContractB` 实例的 `setData` 函数，设置了数据。
- 在 `getDataFromB` 函数中，调用了 `ContractB` 实例的 `getData` 函数，获取了数据。

通过引入合约的方式，可以将代码逻辑模块化，提高代码的可读性和可维护性。在 Solidity 中，引入合约是一种常见的代码复用技术，有助于降低代码重复度并提高开发效率。

### 工厂模式

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import { HelloWorld } from "./test.sol";

contract HelloWorldFactory {
    HelloWorld hw;
    HelloWorld[] hws;

    function createHelloWorld() public  {
        hw = new HelloWorld();
        hws.push(hw);
    }

    function getHelloWorldByIndex(uint256 _index) public view returns (HelloWorld) {
        return hws[_index];
    }

    function callSayHelloFromFactory(uint256 _index, uint256 _id) public view returns (string memory) {
        return hws[_index].sayHello(_id);
    }

    function callSetHelloWorldFromFactory(uint256 _index, uint256 _id, string memory newString) public {
        hws[_index].setHelloWorld(newString, _id);
    }
}
```

## `address(0)` 

`address(0)` 在 Solidity 中是一个特殊的地址，表示 "零地址" 或 "空地址"。它是一个没有有效以太坊地址的存在，其值为 `0x0000000000000000000000000000000000000000`。在智能合约编程中，`address(0)` 通常用于执行以下几种主要目的：

### 1. **检查状态或初始化**

在智能合约中，使用 `address(0)` 可以用来检查某个地址是否未被设置或未分配。例如，在您的合约中，通过检查 `owners[petId]` 是否等于 `address(0)` 来判断某个宠物（`petId`）是否尚未被购买（即无有效拥有者）。

```solidity
require(owners[petId] == address(0), "This pet has already been purchased.");
```
如果 `owners[petId]` 为 `address(0)`，这意味着该宠物尚未有业主，购买请求是有效的。

### 2. **指示空值**

在以太坊和智能合约的上下文中，`address(0)` 通常用作“空值”或“无效值”的指示。比如，在某些情况下，如果智能合约需要表示一个没有实际存在的地址，使用 `address(0)` 是一种标准做法。

### 3. **防止重入攻击**

在某些模式中，合约可以使用 `address(0)` 来记录状态，以确保函数调用不能被重入。例如，当一个合约在执行某个重要操作时，可以暂时将某些状态变量设置为 `address(0)`，以防止由于重入导致意外的结果。

### 4. **代币和分配机制**

在代币合约中，`address(0)` 通常被用作销毁代币的地址。将代币发送到 `address(0)` 可以表明这些代币已被销毁，而不是被转移到另一个账户。这样可以在代币的总供给中减去这些代币。

### 总结

总的来说，`address(0)` 是 Solidity 中用于表示空地址或未设置状态的强有力工具，广泛用于状态检查、合约逻辑管理和安全性增强。使用 `address(0)` 可以简化合约逻辑，降低出错带来的风险。 

## 简单智能合约示例

### 如何在Remix上部署和运行这些合约

1. **访问Remix**：在浏览器中打开[Remix IDE](https://remix.ethereum.org/)。

2. **新建文件**：
   - 在“File Explorers”中，点击“新建文件”图标。
   - 输入文件名，如`SimpleStorage.sol`，然后点击“Enter”。

3. **粘贴合约代码**：
   - 在新建的文件中，粘贴上面的合约代码。

4. **编译合约**：
   - 转到“Solidity编译器”选项卡。
   - 选择编译的Solidity版本（例如：0.8.0，确保用到的版本和代码中的`pragma`声明的版本匹配）。
   - 点击“编译`SimpleStorage.sol`”。

5. **部署合约**：
   - 转到“部署&运行交易”选项卡。
   - 在“环境”下拉列表中，选择“JavaScript VM”。
   - 点击“部署”按钮。

6. **运行合约**：
   - 部署后，在“已部署合约”下，你将看到合约实例。
   - 可以展开合约实例，查看并与合约中的函数交互（如调用`set`及`get`函数）。

对于每个合约，重复创建文件、粘贴代码、编译和部署的步骤即可。

### 1. 简单存储合约

这个合约允许用户存储和检索一个整数。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleStorage {
    uint256 private data;

    function set(uint256 x) public {
        data = x;
    }

    function get() public view returns (uint256) {
        return data;
    }
}
```

### 2. 数字代币合约

这是一个简单的代币合约，允许用户转账代币。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract BasicToken {
    mapping(address => uint256) private balances;

    constructor() {
        balances[msg.sender] = 10000; // 初始供应给合约部署者
    }

    function transfer(address to, uint256 amount) public {
        require(balances[msg.sender] >= amount, "Not enough tokens");
        balances[msg.sender] -= amount;
        balances[to] += amount;
    }

    function balanceOf(address account) public view returns (uint256) {
        return balances[account];
    }
}
```

### 3. 简单拍卖合约

一个简单的拍卖合约，允许人们出价，并将最高出价者设置为赢家。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleAuction {
    address public highestBidder;
    uint256 public highestBid;

    function bid() public payable {
        require(msg.value > highestBid, "There already is a higher bid.");

        if (highestBidder != address(0)) {
            payable(highestBidder).transfer(highestBid);
        }

        highestBidder = msg.sender;
        highestBid = msg.value;
    }
}
```

### 4. 一次性合约

一个合约只允许接收一次Ether的简单实现。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract OneTimeSend {
    bool private received;

    function receiveEther() public payable {
        require(!received, "Ether has already been received.");
        received = true;
    }

    function withdraw() public {
        require(received, "No Ether to withdraw.");
        payable(msg.sender).transfer(address(this).balance);
    }
}
```

### 5. 投票合约

一个投票合约，允许用户为不同的候选人投票。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Voting {
    mapping(string => uint256) private votes;

    function vote(string memory candidate) public {
        votes[candidate] += 1;
    }

    function getVotes(string memory candidate) public view returns (uint256) {
        return votes[candidate];
    }
}
```

### 6. 简单投票简单安全合约

这个合约允许用户为一个选项进行投票，同时为保证安全性，只有合约创建者可以结束投票。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SecureVoting {
    address public owner;
    mapping(string => uint256) private voteCounts;
    bool public votingEnded;

    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can call this function.");
        _;
    }

    constructor() {
        owner = msg.sender;
        votingEnded = false;
    }

    function vote(string memory candidate) public {
        require(!votingEnded, "Voting has ended.");
        voteCounts[candidate] += 1;
    }

    function getVotes(string memory candidate) public view returns (uint256) {
        return voteCounts[candidate];
    }

    function endVoting() public onlyOwner {
        votingEnded = true;
    }
}
```

### 7. 简单拍卖合约与拍卖时间限制

一个简单的拍卖合约，增加了拍卖的时间限制。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract TimedAuction {
    address public highestBidder;
    uint256 public highestBid;
    uint256 public auctionEndTime;

    constructor(uint256 _biddingTime) {
        auctionEndTime = block.timestamp + _biddingTime;
    }

    function bid() public payable {
        require(block.timestamp < auctionEndTime, "Auction already ended.");
        require(msg.value > highestBid, "There already is a higher bid.");

        if (highestBidder != address(0)) {
            payable(highestBidder).transfer(highestBid);
        }

        highestBidder = msg.sender;
        highestBid = msg.value;
    }

    function auctionEnded() public view returns (bool) {
        return block.timestamp >= auctionEndTime;
    }
}
```

### 8. 基本存储为数组合约

该合约允许用户将值存入一个数组，并检索这些值。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract ArrayStorage {
    uint256[] private data;

    function addValue(uint256 value) public {
        data.push(value);
    }

    function getValue(uint256 index) public view returns (uint256) {
        return data[index];
    }

    function getArrayLength() public view returns (uint256) {
        return data.length;
    }
}
```

### 9. 基本的以太坊提款合约

这是一个简单的提款合约，允许合约部署者将捐款提取到他们自己的地址。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleDonation {
    address public owner;
    uint256 public totalDonations;

    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can call this function.");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function donate() public payable {
        totalDonations += msg.value;
    }

    function withdraw() public onlyOwner {
        payable(owner).transfer(address(this).balance);
    }
}
```

### 10. 简易访问控制合约

这个合约允许只有指定的管理员可以执行特定操作。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract AccessControl {
    mapping(address => bool) private admins;
    address public owner;

    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can call this function.");
        _;
    }

    modifier onlyAdmins() {
        require(admins[msg.sender], "Only admins can call this function.");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function addAdmin(address admin) public onlyOwner {
        admins[admin] = true;
    }

    function removeAdmin(address admin) public onlyOwner {
        admins[admin] = false;
    }

    function executeRestrictedAction() public onlyAdmins view returns(string memory) {
        return "Action performed.";
    }
}
```
