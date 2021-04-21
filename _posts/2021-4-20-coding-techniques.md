---
title: Coding Techniques
date: 2021-4-20
categories:
- Programming
tags:
- Coding


---

In this blog, I collect advanced techniques while coding and debugging.  

### Pytorch backward and optimizer.step

Every time after `loss.backward()` is called, the previous computational graph is released. Thus if you want to use the graph again, just add `loss1.backward(retain_graph = True)` to prevent the graph to be released. And remember to reset `optimizer.zero_grad` , before you call `optimizer.step()`. `loss.backward()` will compute the gradient and `optimizer.step()` will apply the gradient and update the tensor. Since you have two losses, you might need to be more careful about when to reset the grad and update.

### Pytorch save and load model

1. Save the whole module.

   ```python
   torch.save(net, path)
   ```

2. Save module parameters.

   ```python
   state_dict = net.state_dict()
   torch.save(state_dict , path)
   ```

### Pytorch checkpoint

1. Save checkpoint.

   ```python
   checkpoint = {
           "net": model.state_dict(),
           'optimizer':optimizer.state_dict(),
           "epoch": epoch
       }
   if not os.path.isdir("./checkpoint"):
       os.mkdir("./checkpoint")
       torch.save(checkpoint, './checkpoint/ckpt_best_%s.pth' %(str(epoch)))
   ```

   

2. Resume from checkpoint.

   ```python
   if RESUME:
       path_checkpoint = "./checkpoint/ckpt_best_1.pth"  # checkpoint path
       checkpoint = torch.load(path_checkpoint)  # load checkpoint
   
       model.load_state_dict(checkpoint['net'])  # load module  parameters
   
       optimizer.load_state_dict(checkpoint['optimizer'])  # load optimizer
       start_epoch = checkpoint['epoch']  # load epoch
   ```

### Pytorch initialize random seed

```python
import torch
import random
import numpy as np

def set_random_seed(seed = 10,deterministic=False,benchmark=False):
    random.seed(seed)
    np.random(seed)
    torch.manual_seed(seed)
    torch.cuda.manual_seed_all(seed)
    if deterministic:
        torch.backends.cudnn.deterministic = True  # deterministic is used to fixed internal randomness
    if benchmark:
        torch.backends.cudnn.benchmark = True  # benchmark is used to make the input sizes consistent 
    
```

​	

### Reference

