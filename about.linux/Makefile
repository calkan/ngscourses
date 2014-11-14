.PHONY:all clean show images
BASENAME=linux
DOWNLOADIMAGES=

%.pnm:%.jpg
	jpegtopnm $< > $@
%.ps:%.pnm
	pnmtops $< > $@
%.epsi:%.ps
	ps2epsi $<
%.ps:%.svg
	inkscape --without-gui --export-ps=$@ $<


show: $(BASENAME).pdf 
	evince $< &

all: $(BASENAME).pdf  


linux01.png: linux01.svg Microsoft_Excel_2013_icon.png
	inkscape --without-gui --export-latex --export-png=$@ $< 

DOWNLOADIMAGES+=Microsoft_Excel_2013_icon.png
Microsoft_Excel_2013_icon.png:
	wget http://www.mcgrawmarketing.com/blog/wp-content/uploads/2013/05/Microsoft_Excel_2013_icon-390x250.png -O Microsoft_Excel_2013_icon.png

DOWNLOADIMAGES+=Alphanumeric_keyboard.jpg
Alphanumeric_keyboard.jpg:
	wget "http://upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Alphanumeric_keyboard.jpg/478px-Alphanumeric_keyboard.jpg"

DOWNLOADIMAGES+=LG_L194WT-SF_LCD_monitor.jpg
LG_L194WT-SF_LCD_monitor.jpg:
	wget "http://upload.wikimedia.org/wikipedia/commons/7/7e/LG_L194WT-SF_LCD_monitor.jpg"
	
#images:${DOWNLOADIMAGES}


$(BASENAME).pdf : $(BASENAME).tex images linux01.ps linux02.ps linux03.ps
	latex $<
	latex $<
	dvips $(basename $<).dvi
	ps2pdf $(basename $<).ps

clean: 
	rm -f $(foreach SUF,dvi aux dvi.pdf log nav out ps pdf snm toc vrb, $(BASENAME).$(SUF) ) *~ $(DOWNLOADIMAGES) linux01.ps linux02.ps linux03.ps
