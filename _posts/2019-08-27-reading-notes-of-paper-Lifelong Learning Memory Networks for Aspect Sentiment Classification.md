---
title: Reading notes of paper "Lifelong Learning Memory Networks for Aspect Sentiment Classification"
date: 2019-08-27
categories:
- Paper Digest
tags:
- Sentiment Analysis
- Natural Language Processing
- 
---

This paper 《Lifelong Learning Memory Networks for Aspect Sentiment Classification》 is published on 2018 IEEE International Conference on Big Data (Big Data) by Shuai Wang from UIC.

There are two main contributions of this paper. First, the authors use memory networks from big unlabeled data to solve the data scarcity problem. Second, they develop a novel model named lifelong learning memory network (L2MN) that can leverage the learned knowledge to new domains.

- #### **Bubble Sort** (best: O(N); worst: O(N^2))

Sorts a list by 'bubbling' the largest element to the end of list. 

I find bubble sort most intuitive for me. If given the task to write a sorting algorithm without any prior knowledge of it, I would probably come up with bubble sort.

```python
def bubbleSort(L):
  for i in range(len(L)):
    for j in range(len(L) - 1):
      if L[j] > L[j+1]:
        temp = L[j]
        L[j] = L[j+1]
        L[j+1] = temp
  return L
  
# a better bubble, stops computing when there's no more to swap
def betterBubble(L):
  swapped = True
  while swapped:
    swapped = False
    for i in range(len(L) + 1):
      if L[i] > L[i-1]:
        temp = L[i]
        L[i] = L[i+1]
        L[i+1] = temp
        swapped = True
  return L
```





- #### **Selection Sort** (best/worst: O(N^2))

Sorts a list by comparing every element to sorted minimal value.

```python
def selSort(L):
  for i in range(len(L) - 1):
    minIndex = i
    minValue = L[i]
    j = i + 1
    while j < len(L):
      if L[j] < minValue:
        minIndex = j
        minValue = L[j]
      j += 1
    temp = L[i]
    L[i] = L[minIndex]
    L[minIndex] = temp
  return L
```





- #### **Insertion Sort** (best: O(N); worst: O(N^2))

Sorts a list by spliting it into 2 parts, the first element being the 'prefix', the rest being the 'suffix'. Then compares and insert properly the first element of the suffix list to the prefix, until the suffix becomes empty.

```python
def insertSort(L):
  for i in range(1, len(L)):
    val = L[i]
    index = i
    while index > 0 and L[index-1] > val:
      L[index] = L[index-1]
      index -= 1
    L[index] = val
  return L
```





- #### **Merge Sort** (O(N lgN))

Sorts by beaking the problem down into minimal sub-problems, them combines the solutions to sub-problems.

```python
def merge(left, right):
  """
  Given 2 lists, merge them into one list with elements sorted.
  """
  result = []
  i, j = 0, 0
  while i < len(left) and j < len(right):
    if left[i] <= right[j]:
      result.append(left[i])
      i += 1
    else:
      result.append(right[j])
      j += 1
  while i < len(left):
    result.append(left[i])
    i += 1
  while j < len(right):
    result.append(right[j])
    j += 1
  return result

def mergeSort(L):
  if len(L) < 2:
    return L[:]
  else:
    middle = len(L) // 2
    left = mergeSort(L[:middle])
    right = mergeSort(L[middle:])
    return merge(left, right)

```





#### *Reference:*

[Wikipedia article on Sorting Algorithms](https://en.wikipedia.org/wiki/Sorting_algorithm)

MIT600 (2008) lecture 9-10 on Sorting Algorithms

[BetterExplained: Sorting Algorithms](https://betterexplained.com/articles/sorting-algorithms/) 