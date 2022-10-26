pacman -S wine-staging
pacman -S yabridge yabridgectl
yabridgectl add /PluginsDIR
yabridgectl sync
yabridgectl status
## Step 1 – Dependencies

I used the package list from my post [https://guysherman.com/2015/08/16/building-ardour-on-windows-with-msys2/](https://guysherman.com/2015/08/16/building-ardour-on-windows-with-msys2/) as the basis for this post because MSYS uses pacman, and has similar naming conventions for packages.

So, first step (assuming you’ve got a working Arch Install with Jack set up and working).

> sudo pacman -S glib2 gobject-introspection c-ares \
libidn rtmpdump gnutls libutil-linux gtk-doc \
docbook-xsl intltool libjpeg-turbo jbigkit \
pkg-config ladspa icu boost curl fftw libusb \
libxml2 libogg flac libvorbis libsndfile \
libsamplerate soundtouch pcre cppunit taglib \
gnome-doc-utils gnome-common atk libpng harfbuzz \
cairo fontconfig freetype2 pixman pango jasper \
libtiff gdk-pixbuf2 shared-mime-info gtk2 \
libsigc++ cairomm atkmm pangomm gtkmm liblo \
serd sord sratom lilv aubio portaudio \
jack2 libltc rubberband soundtouch liblrdf cppunit suil

## Step 2 – Get the code

Assuming you have already changed to the directory where you want to clone ardour

> git clone git://git.ardour.org/ardour/ardour.git

Alternatively you could go to their [github mirror](https://github.com/Ardour/ardour) and fork that, and then clone that to your machine. If you want to submit changes doing them via github PRs is by far the easiest way.

## Step 3 – Build

Next change into the ardour directory that was cloned

> cd ardour

My arch system had Python 3 setup as `python` and the version of waf that Ardour uses doesn’t seem to like python 3, so I had to run it with python2:

> python2 waf configure
> python2 waf

If you are missing any depenencies then you should find out during the _waf configure_ step.

#### Step 4 – Run

To run the version you just built

> cd gtk2_ardour
> ./ardev

[Waf](https://github.com/waf-project/waf) also lets you do install/uninstall/clean etc.