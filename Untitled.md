### Slide 1

Moving towards the **Ongoing and Near Future** applications of AI in Neuroscience, I'm going to talk about a recent paper that combines the study of biological neural networks (the brain) with artificial ones. 

In recent years, deep learning has expanded the toolbox for image classification and prediction tasks. One type of architecture in particular, deep Convolutional Neural Networks (or CNNs) has structure somewhat similar to biological networks and has been shown to be very powerful for image processing tasks. They do this by using convolutional filters to break an input image or data stream into chunks. The chunks are then processed to build up representations of the input data at increasing levels of complexity as the data is passed deeper into the network.

By comparing artificial neural nets to biological ones, we can better understand both types of system.

### Slide 2

I'm going to talk about one recent paper published in Nature Machine Intelligence that used this approach of studying biological networks with artificial ones. Specifically, the authors tried to see if they could structure an artificial neural net with guidance from models of the biological visual cortex in monkeys. The neural network which they called PredNet was trained on the KITTI dataset of car dash cam footage by being tasked with predicting the next frame in a video sequence.

The activation patterns of the neuron in the artificial network, were then compared to real neurons in the visual cortex of monkeys to look for similarities.

### Slide 3

The major finding from this work was that this PredNet behaves very similar to biological data when activation patterns are compared to biological networks for the same task of trying to predict the next frame of an optical illusions. 

One of the illusions they showed this similarity for was the illusory contour illusion in which a shape is implied by the other shapes around it but not drawn explicitly. You can see that the graphs to the right which compare biological neuron activation to the activation of the neural network take similar shape when exposed to the same images shown below. Notably, both networks take the same delay to process the illusory contour image.

### Slide 4

Two more illusions were shown to the network

The Flash Lag effect where the network must try to predict the rotation of a line while another flashes randomly in line with the first.

Also the Rotating Snakes illusion which humans perceive as moving when the image is actually static.

Overall, the authors found that the PredNet model behaved very similarly to biological networks when exposed to these illusions.

### Slide 5

The overall conclusions of this paper were that PredNet was able to recapitulate some of the spatial and temporal reasoning learned in biological networks as a result of its structure.

The authors are interested in seeing what other systems can be modeled and recapitulated in this way though they hypothesize that the notable differences in how artificial neural networks and biological networks activate may limit how closely they can agree with one another. They specifically point to the fact that biological networks activate via the repeated firing of neurons referred to as "spiking" while artificial networks simply output scalar values.

Overall, though they are hopeful for the future of this comparison approach to learn more about the ways the human brain and biological neural networks work as well as potential insights they may obtain to design better artificial neural networks.
