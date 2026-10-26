SVV Lab Task: Static Code Verification

Project: Monster Battle Game

1. Code Review

Category	Result	Defect
Initializations	Issue	sum is uninitialized in averageAttack().
Pointers	Issue	Null pointers, dangling pointers, and memory leaks.
Arrays/Buffers	Issue	Monster array overflow and unsafe boss name input.
Loops	Issue	Incorrect loop condition in totalMonsterHealth().
Arithmetic	Issue	Unsigned damage, integer division, and possible division by zero.
Control Flow	Issue	playerRank() does not return a value for every path.
Function Calls	Issue	Functions can dereference missing or deleted monsters.
Classes	Issue	Copying Game duplicates raw pointers and may cause double deletion.

2. Static Code Verification Report

Line	Defect Type	Why It Is a Problem	Proposed Fix
27–29	Array Bounds	More than five monsters can overflow the array.	Check capacity before spawning.
35	Logical Error	Assignment is used instead of comparison.	Replace = with ==.
45–49	Pointer/Arithmetic	Null dereference and unsafe unsigned damage calculations.	Validate the pointer and damage.
55–56	Loop Bounds	The loop accesses beyond the valid array range.	Change <= to <.
60–63	Dangling Reference	A reference to a local string is returned.	Return std::string by value.
68–71	Initialization	Uninitialized sum and division by zero are possible.	Initialize sum and check the count.
76–77	Memory Safety	A deleted monster is accessed and remains in the array.	Check the pointer and remove the monster safely.
82	Arithmetic	Integer division loses the fractional result.	Divide by 100.0.
86–89	Control Flow	Not all execution paths return a rank.	Add a default return.
93–99	Buffer/Memory	Boss input can overflow the buffer; incorrect array deallocation.	Use std::string or delete[] as appropriate.
103–108	Array Bounds	Six monsters are spawned when capacity is five.	Increase capacity or limit spawning.
110	Memory Leak	The bonus monster is never deleted.	Manage its ownership and release it.
112–120	Runtime Safety	Invalid IDs and deletion can cause errors.	Validate IDs and maintain array integrity.
122	Class Design	Shallow copying can cause double deletion.	Implement deep copying or disable copying.
123	Syntax	Return 0; is invalid C++.	Use return 0;.

Conclusion

Static verification identifies logical errors, memory management defects, array bounds problems, unsafe pointers, and control-flow issues. These defects should be corrected and the program tested before execution.