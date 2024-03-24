# 数组
---
数组(Array)是一种线性的结构, 将相同类型的元素存储在连续的内存空间中
元素在数组中的位置称为该元素的索引(index)
## 1. 初始化数组
---
- 无初始值。在未指定初始值的情况下, 大部分将数组元素初始化为0。使用构造函数`new Array()`
- 给定初始值。使用数组字面量 `[]` 方式创建
```javascript
// 无初始值
var arr = new Array(5).fill(0);
// 给定初始值
var nums = [1, 2, 3, 4, 5];
```

## 2. 访问元素
---
索引从0开始, 索引本质是内存地址的偏移量
首个元素地址偏移量是0
元素内存地址 = 数组内存地址 + 元素长度 × 元素索引
```javascript
var arr = [1, 2, 3, 4, 5];
// 元素索引:0, 1, 2, 3, 4
// 元素内存地址 = 首元素地址 + 地址偏移量
// 假设首元素地址: 000, 数组3处的内存地址
// 000 + 4 × 3 = 012
```
1. 访问数组元素: `arr[index]`
2. 使用 `array.at(index)` 属性访问, 允许传入负数从末尾开始获取
	- 当 `index >= 0` 时, 与 `arr[index]` 相同
	- 当 `index < 0` 时, 从数组末尾开始倒序获取数据
```javascript
// 随机访问元素
function randomAccess(nums) {
    // 在区间[0, nums.length)随机抽取一个数字
    const random_index = Math.floor(Math.random() * nums.length);
    // 获取并返回随机元素
    const random_num = nums[random_index];
    return random_num;
}
```
## 3. 插入元素
---
1. `array.push(item)`：在数组末尾添加一个元素
2. `array.unshift(item)`: 在数组首位添加一个元素
3. `array.splice(index, 0, item)`: 在指定索引位置处添加
```javascript
// 在索引index处插入元素
function insert(nums, num, index) {
    // 将索引index以及之后的所有元素向后位移一位
    for (let i = nums.length - 1; i > index; i--) {
        nums[i] = nums[i - 1];
    }
    // 将num赋给index处的元素
    nums[index] = num;
}
```
## 4. 删除元素
---
1. `array.pop()`: 删除数组末尾的元素
2. `array.shift()`: 删除数组首位元素
3. `array.splice(index, deleteCount)`: 删除指定索引位置处的元素
```javascript
// 删除索引index处的元素
function remove(nums, index) {
    // 把索引index之后的元素向前移动一位
    for (let i = index; i < nums.length - 1; i++) {
        nums[i] = nums[i + 1];
    }
}
```
4. `delete array[index]`: 物理删除, 该元素仍存在, 值变为 `empty`
5. `length`: 数组截断, 将长度设置为所需长度
```javascript
let arr = [1, 2, 3, 4, 5];
arr.length = 3;
console.log(arr);// [1, 2, 3]
```

## 5. 数组遍历
---
- 通过索引遍历
- 直接获取数组中的每个元素
```javascript
// 遍历
function traverse(nums) {
    let count = 0;
    // 通过索引遍历数组
    for (let i = 0; i < nums.length; i++) {
        count += nums[i];
    }
    // 直接遍历数组元素
    for (const num of nums) {
        count += num;
    }
}
```
## 6. 查找元素
---
先遍历数组, 判断每轮元素值是否匹配, 匹配返回对应索引
数组是线性数据结构, 所以也叫"线性查找"
```javascript
function find(nums, target) {
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] === target) return i;
    }
    return -1;
}
```
## 7. 数组扩容
---
在大多数语言中, 数组的长度是不可变的
JavaScript 中的数组是动态数组, 可以直接扩展
1. `array[index] = 0`: 在未知索引处赋值为0, 初始化从而扩充数组
2. `array.length`: 修改数组长度扩充数组
数组扩容, 重新建立一个更大的数组, 再将原数组依次复制到新数组
```javascript
// 在js中, 数组是可变的, 这里假设array是不可变的数组
function extend(nums, enlarge) {
    // 初始化一个扩容的数组
    const res = new Array(nums.length + enlarge).fill(0);
    // 将原数组的元素复制到新数组
    for (let i = 0; i < nums.length; i++) {
        res[i] = nums[i];
    }
    // 返回扩展后的数组
    return res;
}
```
## 数组特点
---
存储在连续的空间内, 元素类型相同。 提升操作效率
- 空间效率: 为数据分配了连续的内存块, 无需额外的开销
- 支持随机访问: 允许在 O(1) 时间复杂度内访问
- 缓存局部性: 访问元素后, 会加载周围的数据, 借助高速缓存提升后续的执行速度
局限:
1. 插入和删除的效率低: 在元素较多时, 插入和删除需要移动大量的元素
2. 长度不可变: 初始化后, 长度就固定了, 扩容是将所有的元素复制到新的数组中, 开销很大
3. 空间浪费: 如果分配空间大小超过实际所需, 多余空间就被浪费了
## 数组应用
---
1. 随机抽样: 可以使用数组存储样本, 生成随机序列, 实现索引的随机抽样
2. 排序和搜索: 排序算法。如: 快速排序, 归并排序, 二分查找等
3. 查找表: 需要查找元素或对应关系时, 如: 字符和ASCII码的映射, 可以将ASCII码作为索引
4. 机器学习: 神经网络中使用了向量, 矩阵, 张量之间的线性代数运算, 可以以数组的形式构建
5. 数据结构的实现: 栈, 队列, 哈希表, 堆, 图等基于数组实现
> 数组排序: 
> 	`sort()`: 不传参数, 会按Unicode码排序, 对于数字来说, 是逐字排序
> 		传入回调函数 `a - b`: 升序; `b - a`: 降序
```javascript
arr.sort((a, b) => a - b);

// 相当于
arr.sort(function (a, b) { return a - b; });
```
> 反转数组:
> 1. 将旧数组遍历, 逆序传入新的数组中
> 2. 交换法: 不使用新的数组的情况; 使用中间变量
> 3. `reverse()`: 这种方法直接影响原数组
```javascript
let newArr = [];
for (let i = arr.length - 1; i >= 0; i--) {
    newArr[newArr.length] = arr[i];
}

// 交换法
for (let i = 0; i < arr.length / 2; i++) {
	let temp;
	temp = arr[i];
	arr[i] = arr[arr.length - 1 - i];
	arr[arr.length - 1 - i] = temp;
}

// reverse()
arr.reverse();
```
# 链表
---
内存空间是公共的, 在复杂的环境中, 空闲的内存空间会散布在内存各处
当数组特别大时, 内存无法提供如此大的连续空间
链表(Linked List)是一种线性数据结构, 每个元素都是一个节点对象, 每个节点通过"引用"相连"
即每个元素存储自身值和下一个节点的内存地址(指针), 使得每个节点分布在内存各处, 内存空间是分散的, 无需连续
- 第一个节点称"首节点"或"头节点", 最后一个节点称"尾节点"
- 尾节点: 指向 `null`
- 链表节点: `ListNode`, 包含值和下一个指针(引用)
在相同数据量下, 链表比数组占用更多的空间
```javascript
// 链表节点
class ListNode {
    constructor(val, next) {
        this.val = (val === undefined ? 0 : val);
        this.next = (next === undefined ? null : next)
    }
}

// 链表类
class LinkedList {
    constructor(head = null) {
        this.head = head;
    }
    // 添加链表头节点
    addAtHead(val) {
        const newNode = new ListNode(val);
        newNode.next = this.head;
        this.head = newNode;
    }
    // 添加链表尾节点
    addAtTail(val) {
        const newNode = new ListNode(val);
        if (!this.head) {
            this.head = newNode;
        } else {
            let current = this.head;
            while (current.next !== null) {
                current = current.next;
            }
            current.next = newNode;
        }
        this.length++;
    }

    // 打印链表
    toString() {
        let currentNode = this.head;
        let result = '';
        // 遍历所有的节点，拼接为字符串，直到节点为 null
        while (currentNode) {
            result += currentNode.val + '';
            currentNode = currentNode.next;
        }
        return result;
    }
}
```
## 1. 初始化
---
初始化分为两步, 第一步初始化各个节点对象, 第二步初始化各节点之间的引用关系
从头节点出发, 依次通过指向 `next` 访问所有对象
```javascript
// 1. 初始化链表: 1 -> 3 -> 2 -> 5 -> 4
const linkedList = new LinkedList();
const n0 = new ListNode(1);
const n1 = new ListNode(3);
const n2 = new ListNode(2);
const n3 = new ListNode(5);
const n4 = new ListNode(4);
// 2. 构建节点之间的引用
n0.next = n1;
n1.next = n2;
n2.next = n3;
n3.next = n4;
// 3. 设置头节点
linkedList.head = n0;

// 调用addAtTail(val)方法添加节点, 和上面相同
const linkedList = new LinkedList(); 
linkedList.addAtTail(1); 
linkedList.addAtTail(3); 
linkedList.addAtTail(2); 
linkedList.addAtTail(5); 
linkedList.addAtTail(4);

// 4. 打印链表
console.log(linkedList.toString());
```
链表是由多个独立节点对象组成的, 通常将头节点视作链表的代称, 如上可记作: 链表 `n0`
## 2. 插入节点
---
在链表中插入节点, 只需修改两个节点之间的引用(指针)即可, 时间复杂度是O(1)
数组中, 插入元素的时间复杂度是O(n)
```javascript
insert(position, val) {
    // 1. 创建新节点
    const newNode = new ListNode(val);
    // 2. 对position进行越界判断
    if (position < 0 || position > this.length) {
        return null;
    }
    if (position === 0) {
        // 如果position为0, 那就说明是第一个节点
        newNode.next = this.head;
        this.head = newNode;
    } else {
        // 0 < position <= this.length
        let currentNode = this.head;
        let previousNode = null;
        let index = 0;
        while (index < position) {
            previousNode = currentNode;
            currentNode = currentNode.next;
            index++;
        }
        newNode.next = currentNode;
        previousNode.next = newNode;
    }
    this.length++;
    return newNode;
}
```
调用时需要更新链表的`length`属性, 因为`insert()`方法会检测`position`是否超出`length`
```javascript
// 1 -> 3 -> 2 -> 5 -> 4
const linkedList = new LinkedList(); 
linkedList.addAtTail(1); 
linkedList.addAtTail(3); 
linkedList.addAtTail(2); 
linkedList.addAtTail(5); 
linkedList.addAtTail(4);

// 调用insert()方法
linkedList.insert(1, 6);
console.log(linkedList.toString());// 1 6 3 2 5 4
```
## 3. 删除节点
---
只需改变一个节点的指针即可
删除节点后, 被删除节点仍指向下一节点, 但经过遍历已经无法访问该节点, 该节点仍存在, 不属于当前链表了
```javascript
remove(position) {
	// 1. 越界判断
	if (position < 0 || position > this.length) {
        return null;
    }
    // 2. 删除
    let currentNode = this.head;
    if (position === 0) {
	    // 1>. position为0时
	    this.head = this.head.next;
    } else {
	    let previousNode = null;
        let index = 0;
        while (index < position) {
            previousNode = currentNode;
            currentNode = currentNode.next;
            index++;
        }
	    previousNode.next = currentNode.next;
    }
    this.length--;
    return currentNode;
}
```
## 4. 访问节点
---
在链表中访问节点的效率较低。 
在数组中是在O(1)下访问数组的任意元素, 链表每次都需从头节点出发, 逐个遍历, 直到找到目标节点。
访问链表的第`i`个节点需要循环`i - 1`轮, 时间复杂度为O(n)
```javascript
getData (position) {
	// 1. 越界判断
	if (position < 0 || position > this.length) {
        return null;
    }
    // 2. 获取指定position节点的值
    let currentNode = this.head;
    for(let i = 0; i < position; i++) {
	    currentNode = currentNode.next;
    }
    return currentNode;    
}
```
## 5. 查找索引
---
查找目标节点在链表中的`index`, 如果没有, 返回`-1`
```javascript
indexOf(target) {
	let currentNode = this.head;
	let index = 0;
	while(currentNode) {
		if(currentNode.val === target) {
			return index;
		}
		currentNode = currentNode.next;
		index++;
	}
	return -1;
}
```
## 数组和链表
---
数组与链表的效率对比

|      | 数组      | 链表      |
| :--- | :------ | :------ |
| 存储方式 | 连续存储空间  | 分散存储空间  |
| 容量扩展 | 长度不可变   | 可灵活拓展   |
| 内存效率 | 元素占用内存少 | 元素占用内存多 |
| 访问元素 | O(1)    | O(n)    |
| 添加元素 | O(n)    | O(1)    |
| 删除元素 | O(n)    | O(1)    |

## 链表类型
---
- 单向链表: 每个节点包含值和指向下一节点的指针两项内容。首届点称为"头节点", 最后一个节点称为"尾节点", 尾节点指向`null`
- 环形链表: 将单向链表的尾节点指向头节点(首尾相连), 在环形链表中, 任意节点都可以视作"头节点"
- 双向链表: 双向链表同时包含了两个方向的指针, 同时指向前驱节点(上一个节点)和后继节点(下一个节点)的指针; 双向链表相较于单向链表更灵活, 可以朝两个方向遍历, 会占用更多的内存空间
```javascript
// 环形链表
// 方法一
// 1. 初始化链表: 1 -> 3 -> 2 -> 5 -> 4
const linkedList = new LinkedList();
const n0 = new ListNode(1);
const n1 = new ListNode(3);
const n2 = new ListNode(2);
const n3 = new ListNode(5);
const n4 = new ListNode(4);
// 2. 构建节点之间的引用
n0.next = n1;
n1.next = n2;
n2.next = n3;
n3.next = n4;
// 3. 设置头节点
linkedList.head = n0;
// 4. 首尾相连
n4.next = n0;
// 5. 遍历
traversal() {
	let currentNode = this.head;
	do {
		console.log(currentNode);
	    currentNode = currentNode.next;
	} while (currentNode !== this.head);
}


// 方法二: 重写addAtTail()方法
addAtTail(val) {
	const newNode = new ListNode(val);
	if (!this.head) {
		this.head = newNode;
		newNode.next = this.head;// 将新节点的next指向自身, 形成环
	} else {
		let currentNode = this.head;
		while (currentNode.next !== this.head) {
			currentNode = currentNode.next;
		}
		currentNode.next = newNode;// 将最后一个节点的指针指向新节点
		newNode.next = this.head;// 将新节点的指针指向头节点, 形成环
	}
	this.length++;// 正确增加链的长度
}
```