# Sample application for Gtk with Python, Glade, PyGobject, and cx-freeze

<i>Tutorial for Windows</i>

Install Python 3 from https://www.python.org/downloads/windows/

For example, under  C:\PythonXX where XX is the version number

#Gtk binding with PyGobject

Install PyGobject pygi-aio-3.14.0_rev19-setup.exe (aka PyGI)

from http://sourceforge.net/projects/pygobjectwin32/files/

You must install Gtk with the PyGi installer (checkbox Gtk-...).

It will be installed under C:\PythonXX\Lib\site-packages\gnome 

You may now test gtk_simple.py or gtk_builder.py with the python command line

#Create a standalone executable with CX freeze

##install it

from http://cx-freeze.sourceforge.net/

cx-freeze will be installed under your Python path, in the Script subdirectory

## Setup Script GTK

A cx freeze setup script is a python file that list source files and
dependancies for the final stanalone, sort-of like a CMake or Makefile script. 

There is a setup script on the gnome wiki, it does not works as-is for rev19
but it was a good begining for the setup_gtk_simple and setup_gtk_builder scripts

https://wiki.gnome.org/Projects/PyGObject?action=AttachFile&do=view&target=setup.py

To constructe an exe, gtk_simple.exe or gtk_build.exe, do

<pre> 
python setup_gtk_simple.py build
</pre>

or

<pre> 
python setup_gtk_builder.py build
</pre>


# sources

http://cx-freeze.sourceforge.net/

http://cx-freeze.readthedocs.org/en/latest/index.html

https://wiki.gnome.org/Projects/PyGObject

#CX-Freeze Troubleshooting

## dll errors

Make sure all dll are copied from the gnome sudirectory under you Python install
(if you have ruby installed, or an another gtk installation in your path make sure
python in listed before)

## How to know which gtk dll are needed for the standalone exe ?

* Download an install ListDlls from https://technet.microsoft.com/en-us/sysinternals/bb896656.aspx
* launch your gtk python script as you would normaly do (eg 'python gtk_simple.py')
* use ListDlls with: ListDlls python.exe > C:\out.log
* Ignore listed System dll like GDI

## Gdk Cannot create screen error

In the cxfreeze setup script,  Make sure 'gi' is in the packages variable

## Squares instead of text (even plain english/latin characters)

Make sure the PyGi's gnome/etc is listed in the include_files variable