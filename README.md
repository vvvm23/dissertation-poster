# Slide 1
Fast image generators with a focus on high resolution images. Fast means
useable in interactive applications, higher resolutions are more useful. Due to
nature of project, will be presenting more than demoing about 15-20 minutes

# Slide 2
Project started as an attempt to address the generative modeling trilemma Term
originates from a paper by nvidia. we are focusing on high quality and fast
samples, modest mode coverage.

# Slide 3
Generative models fall into two broad classes. AR needs n iterations to produce
a full sample, iteratively in predefined order NAR needs O(1), constant ranges
from 1 to thousands potentially makes it faster, or slower.

additionally NAR can use full context available, rather than just prevous

# Slide 4
NAR model of interest -> non-adversarial with fast sampling on text, how to
make work on images?

# Slide 5
modelling pixels directly is (often) not scaleable learn a lossy compression
model (identity function through information bottleneck)

# Slide 6
low distortion not synonymous with high perceptual quality vqgan reformulates
compression into rate-perceptual 

Reduces model mode coverage

# Slide 7

# Slide 8
above dashed line is training process below dotted line is sampling process

generate L using VQGAN on image dataset

during sampling, T is unbounded. reasonable min 20, good range 50-100. can be
infinite, not upper bounded like in some prior work.

# Slide 9
hard to illustrate through words alone, video demonstrates sampling process can
see done patch wise, because of VQ component

# Slide 10

# Slide 11
the left most column contains somes 256x256 samples all others are samples from
the dataset, in increasing distance difference between sample and closest
neighbour demonstrates diversity -> indicates mode collapse isnt significant
here

# Slide 12
another good property -> ability to control what is generated tested first on
MNIST as Imagenet is expensive..

MNIST actually more expensive than previous experiments, demonstrates
efficiency of VQ model.

# Slide 13

# Slide 14

# Slide 15
At this point, we have a fast generative model with complexity that doesn't
scale with input size.

Next natural question is to try scaling it.

up until this point, being used pretrained VQGAN from original work at
heidelberg. must train our own vq model

# Slide 16
hard to do full sweep, expensive experiments compressing further was terrible,
compressing less was too big (64x64=4096)

improving VQ model not the topic our our research

# Slide 17
our SUNDAE model is implemented as an attention architecture.

in a text model, every token must attend to every other, natural n^2
complexity. same when applied to VQ indices.

# Slide 18
doesn't actually fix complexity, just decreases n for the majority of layers.

flaw essentially meant resampling only was applied in the last axis of multi
dimensional data, fixing it provided a surprising boost in performance

fix is generally applicable, outside of generative modeling

# Slide 19

# Slide 20
sampling can actually be done faster than this video, which is unheard of with
most previous methods each sample generated in 2 seconds on my GPU, which is by
no means cutting edge.

# Slide 21

# Slide 22
experimenting with some useful applied tasks for generative models. this sample
had a broken eye, correcting it with the model.

# Slide 23
these two are real people, showing multiple samples to demonstrate diversity of
output. unlike AR, don't need to inpaint in predefined order, can do arbitrary
masks like the right one.

fast sampling permits interactive use, useful when integrating with real
software.

also could support outpainting, text-to-image generation, left for future work.

# Slide 24
a somewhat counterintuitive result at first glance..

probably need some kind of 2d plot to verify. left for future work due to time

# Slide 25
what is proportion?
valid, given a sufficient time budget..

also did for temperature but results are less interesting

# Slide 26
hierarchical transformer improvements valid in a wider context

scalability interesting in a language context, viable NAR LLM framework, GPT
but NAR?

more quality can be obtained via more training / parameter searching, better
recall by dropping in a future better VQ model. our method is a good start
towards a model that meets all three key characteristics.

# Slide 27

