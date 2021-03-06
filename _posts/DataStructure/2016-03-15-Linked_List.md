---
layout: post
title: Singly Linked List
subtitle: What is the singly Linked List ? 
category: Data Structure
tags: [list]
permalink: /2016/03/15/Linked_List/
---

윤성우의 열혈자료구조를 참조했습니다.

아래 그림은 간단한 LinkedList 기능을 보여주는 그림이다.

LinkedList에서 기본적으로 참조 변수를 head, cur, tail를 가지고 있으면 LinkedList를 구현할 수 있다.  

head와 tail은 연결을 추가 및 유지하기 위한것

cur은 참조 및 조회를 위한것 

// 초기화

  ![](/img/Image/DataStructure/2016-03-15-Linked_List/Linked_List_Node_Pointer.png)

// 삽입 1

  ![](/img/Image/DataStructure/2016-03-15-Linked_List/Linked_List_Insert1.png)

// 삽입 2

  ![](/img/Image/DataStructure/2016-03-15-Linked_List/Linked_List_Insert2.png)

// 조회

  ![](/img/Image/DataStructure/2016-03-15-Linked_List/Linked_List_Search.png)

// 삭제

  ![](/img/Image/DataStructure/2016-03-15-Linked_List/Linked_List_Remove.png)

1-1. Linked 개념

  ![](/img/Image/DataStructure/Linked.png)
  
1-2. 정렬기능이 추가된 Linked List ADT

    - ADT니깐 1. 삽입 2. 삭제 3. 검색을 기본 기능으로 추가적인 기능도 설계하자
    - 추가적인 기능 (정렬하면서 삽입 + 원소의갯수 + 초기화)
    - 데이터 중복 허용

  1-2-1. void ListInit(List * plist)
  
        - 초기화할 리스트의 주소 값을 인자로 전달한다. 
        - 리스트 생성 후 제일 먼저 호출되어야 하는 함수이다. 
        
  1-2-2. void LInsert(List * plist, LData data)
  
        - 리스트에 데이터를 저장한다. 매개변수 data에 전달된 값을 저장한다. 
  
  1-2-3. int LFirst (List * plist, LData * pdata)
  
        - 첫번째 데이터가 pdata가 가리키는 메모리에 저장된다. 
        - 데이터의 참조를 위한 초기화가 진행된다. 
        - 참조 성공 시 TRUE(1), 실패시 FALSE(0) 반환
        
  1-2-4. LNext(List * plist, LData * pdata)
  
        - 참조된 데이터의 다음 데이터가 pdata가 가리키는 메모리에 저장된다.
        - 순차적인 참조를 위해서 반복호출이 가능하다. 
        - 참조를 새로 시작하려면 먼저 LFirst 함수를 호출해야 한다. 
        - 참조 성공 시 TRUE(1), 실패 시 FALSE (2) 리턴
        
  1-2-5. LData LRemove(List * plist)
  
        -  LFirst 또는 LNext 함수의 마지막 반환 데이터를 삭제한다. 
        -  삭제된 데이터는 반환한다. 
        -  마지막 반환 데이터는 삭제하므로 연이은 반복 호출을 허용하지 않도록 설계한다. 
  
  1-2-6. int LCount(List *plist)
        
        - 리스트에 저장되어 있는 데이터의 수를 반환한다. 
        
  1-2-7. void SetSortRule(List * plist, int (*comp)(LData d1 LData d2))
  
        - 리스트에 정렬의 기준이 되는 함수를 등록한다. 
        * SetSortRule 함수는 정렬의 기준을 설정하기 위해 정의 된 함수!
        
1-3. 노드 추가의 위치 설정 

    - 새 노드를 머리에 추가하는 경우 : 포인터 tail 불필요, 저장 순서는 반대로 유지
    - 새 노드를 꼬리에 추가하는 경우 : 포인터 tail 필요, 저장 순서 유지
    * 하지만 우리는 tail 생략을 위해 머리에 추가하는 방식으로 할 것이다. 
    
1-4. SetSortRule

  ![](/img/Image/DataStructure/2016-03-15-Linked_List/Set_Sort_Rule.png)
  
1-5. 본격적이 코드 구현 
  
  1-5-1. 더미노드를 추가하여 구현 -> 삽입시 불필요한 연산을 줄여준다. 
  
  ![](/img/Image/DataStructure/2016-03-15-Linked_List/dummynode.png)
  
  1-5-2. source code
  
```c
#define TRUE 1
#define FALSE 0
  
typedef int LData;
typedef struct _node        /// 리스트의 노드
{
    LData data;
    struct _node * next;
} Node;
  
typedef struct _linkedList      // Linked List 설정
{
    Node * head;
    Node * cur;
    Node * before;
    int numOfData;
    int (*comp)(LData d1, LData d2);
} LinkedList;
  
typedef LinkedList List;
  
// 구조체 정의를 보고 초기화를 설정한다. 
void ListInit(List * plist)
{
    plist -> head = (Node *)malloc(sizeof(Node));  // 더미노드 생성
    plist -> head -> next = NULL;
    plist -> comp = NULL;
    plist -> numOfData = 0;
}
```
  
  ![](/img/Image/DataStructure/2016-03-15-Linked_List/DummynodeInit.png)  
    
```c
// 더미 노드를 이용한 삽이 
void LInsert(List * plist, LData data)
{
    // 더미 노드 때문에 두 가지 경우로 나누어서 삽입을 생각 안해도 된다. 
    if(plist -> comp == NULL)       // 정렬기준이 없다면
      FInsert(plist, data);         // 머리에 노드 계속 추가
    else                            // 정렬기준이 있다면
      SInsert(plist, data);         // 정렬기준에 근거하여 노드 추가 
}
  
void FInsert(List * plist, LData data)
{
    Node * newNode = (Node *)malloc(sizeof(Node)); // 새노드 생성
    newNode -> data = data;                       //  새노드에 데이터 저장
      
    newNode -> next = plist -> head -> next;      // 새노드가 다른노드 가리킨다. 
    plist -> head -> next = newNode;              // 더미 노드가 새노드를 가리킨다. 
      
    (plist -> numOfData)++;                       // 리스트의 노드 수 증가
}
```
 
  ![](/img/Image/DataStructure/2016-03-15-Linked_List/DummyLinkedListFInsert.png) 
  
```c
void SInsert(List * plist, LData data)
{
    // 1 단계
    Node * newNode = (Node *)malloc(sizeof(Node));
    Node * pred = plist -> head;
    newNode -> data = data;
      
    // 2 단계 
    // comp 0을 반환한다는 것은 첫번째인자가 정렬순서 상 head에 가깝다는 것을 의미한다. 
    // 새 노드가 들어갈 위치를 찾기 위한 반복문
    while(pred -> next != NULL  && plist -> comp(data, pred -> next -> data) != 0)
    {
        pred = pred -> next;
    }
      
    // 3단계
    newNode -> next = pred -> next;
    pred -> next = newNode;
    (plist -> numOfData)++;
      
}
  
// SetSortRule함수를 통해서 List의 comp값 설정
void SetSortRule(List * plist, int (*comp)(LData d1, LData d2))
{ 
    plist -> comp = comp;
}
```
  
  위의 상황을 그림으로 이해하자.
  
  먼저 주어진 상황에서  SInsert(&plist, 5); 실행, 상황은 아래와 같다. 
  
  ![](/img/Image/DataStructure/2016-03-15-Linked_List/DummyLinkedListLInsert1.png)
  
  // 1 단계
  
  ![](/img/Image/DataStructure/2016-03-15-Linked_List/DummyLinkedListLInsert2.png)  
  
  // 2단계
  
  // pred -> next != NULL  마지막 노드를 가리키는지 묻기 위한 연산
  
  // pred -> comp(data, pred->next->data != 0)
  
  // data, pred->next -> data의 우선 순위 비교
  
  // comp return 0이면  data가 head에 가까워야 하고 
  
  // comp return 1이면 pred->next->data가 head에 가까워야 한다. 
  
  ![](/img/Image/DataStructure/2016-03-15-Linked_List/DummyLinkedListLInsert3.png) 
  
  // 3 단계
  
  ![](/img/Image/DataStructure/2016-03-15-Linked_List/DummyLinkedListLInsert4.png) 
  
```c
// comp에 대입할 함수 
int WhoisPreceed(int d1, int d2)
{
    if(d1 < d2)
        return 0;    /// d1이 정렬순서상 앞
    else
        return 1;    /// d2가 정렬순서상 앞
}

// 더미 노드 연결리스트 참조1
int LFirst(List * plist, LData * pdata)
{
    if(plist -> head -> next == NULL)         /// 더미노드가 NULL을 가리키면 아무것도 없는 것
        return FALSE;                         /// 반환할 데이터가 없다. 
        
    plist -> before  = plist -> head;         /// before는 더미 노드를 가리킨다. 
    plist -> cur = plist -> head -> next;     /// cur은 첫번째 노드를 가리킨다. 
      
    *pdata = plist -> cur -> data;            /// 첫번째 노드의 데이터 반환
    return TRUE;                              /// 데이터 참조 성공
}
```
  
  // 더미노드 기반 LinkedList 참조 1
  
  ![](/img/Image/DataStructure/2016-03-15-Linked_List/DummyNodeLinkedListReference1.png)
  
```c
// 더미 연결리스트 참조 2
int LNext(List * plist, LData * pdata)
{
    if(plist -> cur -> next == NULL)          //더미 노드가 NULL이라면
          return FALSE;                       // 참조할 데이터 없다. 
      
    plist -> before = plist -> cur;           // cur이 가리키던 노드를 before이 가리키고
    plist -> cur = plist -> cur -> next;      // cur은 그 다음 노드를 가리킨다. 
      
    *pdata = plist -> cur -> data;            // cur이 가리키느 노드의 데이터 전달
    return TRUE;                              // 참조 성공
}
```
  
  // 더미노드 기반 LinkedList 참조 2
  
  ![](/img/Image/DataStructure/2016-03-15-Linked_List/DummyNodeLinkedListReference2.png)
  
  // 더미노드 기반 LinkedList 삭제 1
  
  ![](/img/Image/DataStructure/2016-03-15-Linked_List/DummyNodeLinkedListDelete1.png)
  
  // 더미노드 기반 LinkedList 삭제 2
  
  ![](/img/Image/DataStructure/2016-03-15-Linked_List/DummyNodeLinkedListDelete2.png)
    
