---
title: Coding Techniques
date: 2021-4-20
categories:
- Programming
tags:
- Coding


---

In this blog, I collect advanced techniques while coding and debugging.  

### backward and optimizer.step

Every time after `loss.backward()` is called, the previous computational graph is released. Thus if you want to use the graph again, just add `loss1.backward(retain_graph = True)` to prevent the graph to be released. And remember to reset `optimizer.zero_grad` , before you call `optimizer.step()`. `loss.backward()` will compute the gradient and `optimizer.step()` will apply the gradient and update the tensor. Since you have two losses, you might need to be more careful about when to reset the grad and update.

### Reference

