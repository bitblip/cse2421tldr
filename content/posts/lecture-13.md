---
title: "Lecture 13"
date: 2021-02-04T02:30:11-05:00
description : "Linked Lists in C"
tags: ["linked lists", "c"]
---

# Lecture 13
**Video** : [Linked Lists In C Part A](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/fW8oloxIVamtCCZCduyFbIbLaAPgTEvpFW1ZXypcqBfx-qfcbNsyCdKFvLoTg5fu.1mFswHf-TeWllLmS__;!!KGKeukY!mAjGQn3EYr8gE72x-9l3ueITEty04yQDuNPaxZERZivRx1_MbcF2Bea6sl2TWIZ1$)
**Video** : [Linked Lists In C Part B](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/WyhpWZIaMqvdXwV5yAuEFc7KEsp6qaAClGvhKAttglKC49sg1sWxV0Sc0aof2pa5.2hLmg7hUGC_I5GJs__;!!KGKeukY!ifE1E_pLTsdEVryrpNX6WCWz0NtauHucY71p6z0FFwUk2Y6eDH-Dop7XJ_2wJSWk$)

**Slides** : [Linked Lists](https://osu.instructure.com/courses/95904/files/folder/Class%20slides?preview=29178134)

# Linked List Nodes
List of objects that have pointers to the next node in the list. More efficient than arrays when inserting and deleting items from the list.

``` c
struct Data {
  ...
}

typedef struct Node {
  struct Data data;
  struct Node *next;
}Node; 
```

> Note that despite the `typedef` Node declaration as `Node`, the identifier is not available until after the struct has been parsed by the compiler. Thus `Node *next` is not possible, therefore the longer from `struct Node *next;` appears.

Begin the list with a **head** pointer.
``` c
Node *listHead = NULL;
```

When passing listHead, consider if it should be passed by reference or by value. If the function needs to alter the pointer, such as inserting a new node at the start of the list, then it will be necessary to modify the pointer to point to the new lead node.

## New Node
``` c
Node *pNewNode;
pNewNode = malloc(sizeof(Node));
```

ALways check allocation for `NULL`.
``` c
if(pNewNode != NULL) {
  /* Populate data */
}
```

``` c
listHead = &pNewNode;
```

## Insert into a sorted list
 Use a temporary variable, such as `Node *traversePtr;` to store each *next reference. **Traverse** the list, looking for the correct location to insert and updating `*traversePtr` as you go.

 Normally we begin this process by assigning `traversePtr` from `listHead`.

 ``` c
 Node *traversePtr = listHead;
 ```

 ### The list is empty
 ``` c
 *listHeadPtr = newNodePtr;
 newNodePtr->next = NULL;
 ```

 ### Insert a leading node
 Point the current head to the new node then assign the new node to head.

 ``` c
 newNodePtr->next = *listHeadPtr;
 *listHeadPtr = newNodePtr;
 ```

 ### Insert an ordered node
 Traverse the next nodes, looking for the next node that does not satisfy the sorting equality.
 ``` c
 Node *traversePtr = listHead;
 while(*traversePtr->next != null && *traversePtr->next->data.ID < *newNotePtr->data.ID) {
   traversePtr = *traversePtr->next;
 }

 /* Whatever is next at traversePtr->next, is were the new node goes */
 newNodePtr->next = *traversePtr->next;
 *traversePtr->next = &newNodePtr;
 ```

 ## Delete a node

 ### Deleting a node
 Traverse the nodes, looking for the node. Skip the node and deallocate the node.

``` c
Node *traversePtr = *listHeadPtr;
while(traversePtr->next != null && *traversePtr->next->data.ID != id) {
  traversePtr = *traversePtr->next;
}

/* traversePtr->next is the node that needs removed, or null because the node did not exist */
Node *removePtr = *traversePtr->next;
*traversePtr->next = *removePtr->next;
free(*removePtr);
```