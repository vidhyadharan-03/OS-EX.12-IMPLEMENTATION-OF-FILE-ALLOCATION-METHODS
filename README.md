# OS-EX.12-IMPLEMENTATION-OF-FILE-ALLOCATION-METHODS

# FILE MANAGEMENT USING SEQUENTIAL ALLOCATION

## AIM:
To implement file management using sequential list.

## ALGORITHM:

STEP 1: Start the program.

STEP 2: Gather information about the number of files.

STEP 3: Gather the memory requirement of each file.

STEP 4: Allocate the memory to the file in a sequential manner. 

STEP 5: Select any random location from the available location. 

STEP 6: Check if the location that is selected is free or not.

STEP 7: If the location is allocated set the flag = 1.

STEP 8: Print the file number, length, and the block allocated.

STEP 9: Gather information if more files have to be stored.

STEP 10: If yes, then go to STEP 2.

STEP 11: If no, Stop the program

## PROGRAM:
```C
#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
void recurse(int files[])
{
    int flag = 0, startBlock, len, j, k, ch;
    printf("Enter the starting block and the length of the files: ");
    scanf("%d%d", &startBlock, &len);
    for (j=startBlock; j<(startBlock+len); j++)
    {
        if (files[j] == 0)
            flag++;
    }
    if(len == flag)
    {
        for (int k=startBlock; k<(startBlock+len); k++)
        {
            if (files[k] == 0)
            {
                files[k] = 1;
                printf("%d\t%d\n", k, files[k]);
            }
        }
        if (k != (startBlock+len-1))
            printf("The file is allocated to the disk\n");
    }
    else
        printf("The file is not allocated to the disk\n");

    printf("Do you want to enter more files?\n");
    printf("Press 1 for YES, 0 for NO: ");
    scanf("%d", &ch);
    if (ch == 1)
        recurse(files);
    else
        exit(0);
    return;
}

int main()
{
    int files[50];
    for(int i=0;i<50;i++)
    files[i]=0;
    printf("Files Allocated are :\n");

    recurse(files);
    getch();
    return 0;
}
```

## OUTPUT:
![image](https://github.com/Jayabharathi3/OS-EX.12-IMPLEMENTATION-OF-FILE-ALLOCATION-METHODS/assets/120367796/699b1287-7488-4629-af35-a819e3e88303)


## RESULT:
Thus, file management using sequential list is implemented successfully.



# FILE MANAGEMENT USING INDEXED ALLOCATION

## AIM:
To implement file management using Indexed list.

## ALGORITHM:

STEP 1: Start the program.

STEP 2: Get information about the number of files.

STEP 3: Get the memory requirement of each file.

STEP 4: Allocate the memory to the file by selecting random locations. 

STEP 5: Check if the location that is selected is free or not.

STEP 6: If the location is allocated set the flag = 1, and if free set flag = 0.

STEP 7: Print the file number, length, and the block allocated.

STEP 8: Gather information if more files have to be stored.

STEP 9: If yes, then go to STEP 2.

STEP 10: If no, Stop the program.

 
## PROGRAM:
```C
#include <stdio.h>
#include <stdlib.h>

int files[50], indexBlock[50], indBlock, n;
void recurse1();
void recurse2();

void recurse1()
{
    printf("Enter the index block: ");
    scanf("%d", &indBlock);
    if (files[indBlock] != 1)
    {
        printf("Enter the number of blocks and the number of files needed for the index %d on the disk: ", indBlock);
        scanf("%d", &n);
    }
    else
    {
        printf("%d is already allocated\n", indBlock);
        recurse1();
    }
    recurse2();
}

void recurse2()
{
    int ch;
    int flag = 0;
    for (int i=0; i<n; i++)
    {
        scanf("%d", &indexBlock[i]);
        if (files[indexBlock[i]] == 0)
            flag++;
    }
    if (flag == n)
    {
        for (int j=0; j<n; j++)
        {
            files[indexBlock[j]] = 1;
        }
        printf("Allocated\n");
        printf("File Indexed\n");
        for (int k=0; k<n; k++)
        {
            printf("%d ------> %d : %d\n", indBlock, indexBlock[k], files[indexBlock[k]]);
        }
    }
    else
    {
        printf("File in the index is already allocated\n");
        printf("Enter another indexed file\n");
        recurse2();
    }
    printf("Do you want to enter more files?\n");
    printf("Enter 1 for Yes, Enter 0 for No: ");
    scanf("%d", &ch);
    if (ch == 1)
        recurse1();
    else
        exit(0);
    return;
}

int main()
{
    for(int i=0;i<50;i++)
        files[i]=0;

    recurse1();
    return 0;
}
```

## OUTPUT:

![image](https://github.com/Jayabharathi3/OS-EX.12-IMPLEMENTATION-OF-FILE-ALLOCATION-METHODS/assets/120367796/4c67f54c-26d4-4953-ac84-71c59608fe98)


## RESULT:
To implement file management using Indexed list.


# FILE MANAGEMENT USING LINKED ALLOCATION

## AIM:
To implement file management using Linked list.

## ALGORITHM:

STEP 1: Start the program.

STEP 2: Gather information about the number of files.

STEP 3: Allocate random locations to the files.

STEP 4: Check if the location that is selected is free or not.

STEP 5: If the location is free set the flag=0 a location is allocated set the flag = 1.

STEP 6: Print the file number, length, and the block allocated.

STEP 7: Gather information if more files have to be stored.

STEP 8: If yes, then go to STEP 2.

STEP 9: If no, Stop the program.

## PROGRAM:
``` C
#include <stdio.h>

#include <stdlib.h>

void recursivePart(int pages[]){
    int st, len, k, c, j;
    printf("Enter the index of the starting block and its length: ");
    scanf("%d%d", &st, &len);
    k = len;
    if (pages[st] == 0){
        for (j = st; j < (st + k); j++){
            if (pages[j] == 0){
                pages[j] = 1;
                printf("%d------>%d\n", j, pages[j]);
            }
            else {
                printf("The block %d is already allocated \n", j);
                k++;
            }
        }
    }
    else
        printf("The block %d is already allocated \n", st);
    printf("Do you want to enter more files? \n");
    printf("Enter 1 for Yes, Enter 0 for No: ");
    scanf("%d", &c);
    if (c==1)
        recursivePart(pages);
    else
        exit(0);
    return;
}

int main(){
    int pages[50], p, a;

    for (int i = 0; i < 50; i++)
        pages[i] = 0;
    printf("Enter the number of blocks already allocated: ");
    scanf("%d", &p);
    printf("Enter the blocks already allocated: ");
    for (int i = 0; i < p; i++){
        scanf("%d", &a);
        pages[a] = 1;
    }

    recursivePart(pages);
 
    return 0;
}

```

## OUTPUT:
![image](https://github.com/Jayabharathi3/OS-EX.12-IMPLEMENTATION-OF-FILE-ALLOCATION-METHODS/assets/120367796/b09bebf3-c3c1-460e-ac4d-3ec237fda0b3)


## RESULT:
 Thus, file management using Linked list is implemented successfully
