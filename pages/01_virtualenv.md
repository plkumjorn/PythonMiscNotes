# Basic virtual environments (with Version control & Jupyter notebooks)
Virtual environment is used to maintain python libraries for a particular project without affecting system-wide libraries. It also promotes reproducible research as other researchers can create the same environment to run your codes successfully (e.g., after cloning your repository from github).

## Installations
1. Install virtualenv via pip.
        
        pip install virtualenv
          
2. Test your installation.
	
		virtualenv --version

## Basic Usage
1. Inside the project folder, create a virtual environment for the project

		virtualenv venv
	where `venv` is the name of the environment you create. 

	You can also use the Python interpreter of your choice. For example, to use python 2.7,

		virtualenv -p /usr/bin/python2.7 venv

2. To begin using the virtual environment,

		source venv/Scripts/activate

	You can notice the environment name appearing before the terminal prompt.

		(venv) xxxxx $ 

3. To check that you are in the virtual environment,
		
		which python
		> xxxxx/venv/bin/python 
		# Python in the venv is used 

4. To install a package, we can use a normal pip command.

		pip install numpy

5. To list all the libraries installed in the current virtual environment (with their versions),
	
		pip freeze

	We can also divert the output to a requirement file for future use.

		pip freeze > requirements.txt

6. When we want to deactivate the environment, just type

		deactivate

## Working with version control systems 

1. We should exclude the virtual environment folder (`venv`) from source control by adding it to the ignore list. For example, adding the following line to your `.gitignore` file.

		venv/

2. For other developers who clone your folder and want to set up the virtual environment, just create a new environment and install all the required libraries.

		virtualenv venv		
		source venv/Scripts/activate
		pip install -r requirements.txt

## Jupyter notebooks under the virtual environment

1. From inside the environment, install ipykernel using pip.

		pip install ipykernel

2. Install a new kernel.

		ipython kernel install --user --name=venv

	where `venv` is the name of the environment we created.

3. Start Jupyter notebook.

		jupyter notebook

4. To create a new notebook under this environment, select New > venv.

## Notes

- You may want to use [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/index.html) to work with virtual environments more conveniently, but in my opinion, it is not needed as the original commands are already easy to use. 

## References

I would like to thank the authors of these helpful resorces which I used as references.

- [Pipenv & Virtual Environments](https://docs.python-guide.org/dev/virtualenvs/) by Kenneth Reitz & Tanya Schlusser
- [Jupyter Notebook in a virtual environment (virtualenv)](https://medium.com/@eleroy/jupyter-notebook-in-a-virtual-environment-virtualenv-8f3c3448247) by Emmanuel
- [Using jupyter notebooks with a virtual environment](https://anbasile.github.io/programming/2017/06/25/jupyter-venv/) by Angelo Basile