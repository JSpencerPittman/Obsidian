# Image Recognition and CNN's
A neuron located at in the ith row and jth column is connected to the outputs of the previous layer located in rows $i$ to $i+f_h-1$ and columns $j$ to $j+f_w-1$
> $f_h$ and $f_w$ are the height and width of the vision field

To maintain the same shape as a previous layer 0's are often added as a means of *zero padding*
The shift from one receptive field to the next is called a *stride*

To make a higher level layer smaller we space out the receptive field by saying that
the neuron of ith row and jth column is connected to rows $i*s_h$ to $i*s_h+f_h-1$
and likewise columns $j* s_w$ to $j*s_w+f_w-1$

## Filters
A neuron's weight can be represented as a small image the size of the receptive field. 
A set of weights is called *filters* or *convolutional kernels*.

A layer of neurons using the same filter outputs a *feature map*. 
Often a convolutional layer will have multiple filters and outputs one feature map per filter. 

All neurons in a feature map have the same weights and biases, but neurons in different feature maps have different parameters. 