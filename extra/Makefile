# Build practical

name ?= practical-cnn-reg
ver ?= 2016a

code=\
checkDerivativeNumerically.m \
l1LossBackward.m \
l1LossForward.m \
l2LossBackward.m \
l2LossForward.m \
exercise1.m \
exercise2.m \
exercise3.m \
getBatch.m \
addCustomLossLayer.m \
initializeLargeCNN.m \
initializeSmallCNN.m \
proj.m \
setup.m \
showDeblurringResult.m \
showFeatureChannels.m \
xavier.m \
README.md \
matconvnet

doc=\
doc/images \
doc/instructions.html \
doc/base.css \
doc/prism.css \
doc/prism.js

data=\
data/text_imdb.mat \
data/ray.jpg \
data/crab.jpg

include extra/practical/Makefile

BINPACK_URL=http://www.robots.ox.ac.uk/~karel/project/matconvnet/bin

%-bin: $(TMPDIR)/matconvnet-%-bin.tar.gz
	tar xzvf $< -C ./matconvnet

$(TMPDIR)/matconvnet-%-bin.tar.gz:
	wget $(BINPACK_URL)/$(notdir $@) -O $@

# Preprocessing
.PHONY: preproc bins

papers_url=http://www.robots.ox.ac.uk/~vedaldi/assets/pubs
papers=\
blaschko10simultaneous.pdf \
chatfield11devil.pdf \
chatfield14return.pdf \
cimpoi14describing.pdf \
cimpoi15deep.pdf \
cimpoi16deep.pdf \
fulkerson08localizing.pdf \
fulkerson09class.pdf \
jaderberg14deep.pdf \
jaderberg14speeding.pdf \
jaderberg14synthetic.pdf \
jaderberg15reading.pdf \
jones07inertial.pdf \
juneja13blocks.pdf \
lempitsky11pylon.pdf \
lenc15rcnn.pdf \
lenc15understanding.pdf \
mahendran15understanding.pdf \
parizi15automatic.pdf \
parkhi11truth.pdf \
parkhi12cat.pdf \
parkhi12spotting.pdf \
parkhi14compact.pdf \
parkhi15deep.pdf \
pedersoli11coarse.pdf \
pedersoli14coarse.pdf \
rabinovich07objects.pdf \
simonyan12descriptor.pdf \
simonyan13deep.pdf \
simonyan13fisher.pdf \
simonyan14deep.pdf \
simonyan14learning.pdf \
sreekanth10generalized.pdf \
vedaldi05features.pdf \
vedaldi05kalmansac.pdf \
vedaldi05TRviewpoint.pdf \
vedaldi06local.pdf \
vedaldi06viewpoint.pdf \
vedaldi07boosting.pdf \
vedaldi07complexity.pdf \
vedaldi07moving-orig.pdf \
vedaldi07moving.pdf \
vedaldi07open.pdf \
vedaldi08joint.pdf \
vedaldi08quick.pdf \
vedaldi08relaxed.pdf \
vedaldi09multiple.pdf \
vedaldi09structured.pdf \
vedaldi10efficient.pdf \
vedaldi10knowing.pdf \
vedaldi10vlfeat.pdf \
vedaldi11efficient.pdf \
vedaldi11learning.pdf \
vedaldi12self.pdf \
vedaldi12sparse.pdf \
vedaldi14understanding.pdf \
vedaldi15matconvnet.pdf

papers:=$(addprefix data/text/,$(papers))
papers_crops=$(papers:%.pdf=%.png)

preproc: $(papers) $(papers_crops)

bins: win7-bin maci64-bin glnxa64-bin
	rm -f matlab/mex/*.mex*

ec2bins: ec2-bin
	rm -f matlab/mex/*.mex*

data/text/%.pdf:
	mkdir -p data/text ; \
	wget "$(papers_url)/$(*).pdf" -O "$(@)"

%.png : %.pdf extra/Makefile
	convert \
	-verbose \
	-units PixelsPerInch \
	-density 300 \
	"$(<)"[2] \
	-colorspace 'rgb' \
	-flatten \
	-resize 'x1536' \
	-gravity center -crop 512x512+0+0 \
	"$(@)"

info:
	@echo Images: "$(papers)"
