KNoT Documentation
==================

### How to build:
- Make sure that pip3 is installed in your machine.

	If you're using a Debian based OS, run the following command to install pip3:
	```bash
	$ sudo apt-get install python3-pip
	```

- Install Sphinx and Read The Docs theme:
	```bash
	$ pip3 install Sphinx
	$ pip3 install recommonmark
	$ pip3 install sphinx_rtd_theme
	```

- Build KNoT Doc:
	```bash
	$ make html 
	```
	> Result will be in the _build/html directory
