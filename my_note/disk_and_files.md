**The byte offset bits are always 0 for word accesses**

page: the basic unit of data for disk, the smallest unit of transfer from disk to memory 

I/O: equivalent to 1 page read to disk or 1 page write to disk

heap file: no particular ordering of pages or records on pages; quick to insert, slow to search
1. linked list implementaion 
2. page direcotry implementation 

sorted file: page are sorted and records are also sorted(search logn, insert logn + n)

![[Screen Shot 2022-04-26 at 11.53.34 AM.png]]

#DBMS_R/G

# chapter9(storing data: disk and files )
## Question
1. different kinds of memory in a computer system?
2. how does the physical characteristics of disks and tapes affect the design of database system?
3. RAID storage systems? what is the advanatge?
4. how does DBMS access and modify data on disks? (how does DBMS keep track of space on disks?) why is *pages* important as a unit of storage and transfer
5. how does DBMS create and main files of records? how is record arranged on pages? how are pages arranged in files?

## 9.1: the memory hierarchy

![[Screen Shot 2022-04-26 at 12.25.31 PM.png]]

primary memory including **cache memory and main memory** is 100 times more expensive than the cost of disk space and tapes. therefore, we can only store data on tapes and disks. **we need DBMS to retrieve data from lower levels of the memory hierarchy into main memory as needed for processing**.

32_bit_addressing: a single byte's address is 32_bit_addressing, which means it can store up to 2^32 bytes, but the number of data object that needs to be stored may exceed 2^32. Thus, we need disk and tapes.

byte addressable: a single character can be read from or written to any memory byte, while disks do it in chunks.

32 bit vs 64 bit: 32-bit system can access 2^32 different memory addresses, each address corresponds to one byte of data(byte addressable), so the total data ram can hold is 2^32 byte = 4GB. 

**novalatility:** we need to store file even when computer is off.

**tape**: tape is sequential device and therefore hard to locate the required information.

### 9.1.1 Magnetic Disks
**disk:** While **direct acces**s to any desired location in main memory takes approximately the same time, **determining the time to access a location** on disk is more complicated.

### 9.1.2 performance implications of disk structure
1. data must be stored in memory for DBMS to operate on it 
2. the unit for data transfer between disk and main memory is a block, operation on block is called I/O operation.
3. the time for moving data from or to disk is essential: the records that are used frequently together should be stored together. 

## 9.2  redundant arrays of independent disks
**disk striping**: distribute data over several disks
**redundancy:** Instead of having a single copy of the data, redundant information is maintained.
**RAID**: redundant array of independent disks

## 9.3 disk space management 
disk space manager: 
1. provide command to read or write a page(same as disk block)
2. allocate pages to hold data frequently accessed together
3. allow software to think of data as a collection of pages
4. keep track of free blocks
5. useing OS file to manage disk space

