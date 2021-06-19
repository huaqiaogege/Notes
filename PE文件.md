PE文件
1.文件头重要字段作用
可选头大小（224字节），文件属性，机器型号

2.可选头重要成员
PE类型
OEP 程序执行入口位置
数据目录

3.节表

```
typedef struct _IMAGE_SECTION_HEADER {
    BYTE    Name[IMAGE_SIZEOF_SHORT_NAME];　　/*节区的名字*/
    union {
            DWORD   PhysicalAddress;
            DWORD   VirtualSize;　　　　　　　　/*节区的尺寸*/
    } Misc;
    DWORD   VirtualAddress;　　　　　　　　　　/*虚拟地址 节区的RVA地址(偏移)*/
    DWORD   SizeOfRawData;　　　　　　　　　　 /*在文件中对齐的尺寸*/
    DWORD   PointerToRawData;　　　　　　　　 /*在文件中的偏移*/
    DWORD   PointerToRelocations;　　　　　　/*在OBJ文件中使用*/
    DWORD   PointerToLinenumbers;　　　　　　/*行号表位置,调试使用*/
    WORD    NumberOfRelocations;　　　　　　/*在OBJ文件中使用*/
    WORD    NumberOfLinenumbers;　　　　　　/*行号表的数量*/
    DWORD   Characteristics;　　　　　　　　/*节的属性*/
} IMAGE_SECTION_HEADER, *PIMAGE_SECTION_HEADER;
```

重要成员：

1.节的尺寸

2.虚拟地址，RVA（偏移）

3.文件中的大小

4.文件中的偏移

5.节的属性