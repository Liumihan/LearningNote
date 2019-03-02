# 2019年01月28日14:58:15:

Pytorch 中遇到的内存泄露的问题:

在训练的循环中:

​        running_loss = (float(running_loss * i) + float(loss)) / float(i + 1)

在这里，total_loss你的循环训练中积累了历史，因为它loss是一个具有autograd历史的可微变量。你可以通过编写total_loss += float(loss)来解决这个问题。