# nbconvertsync
A git hook to automatically render jupyter notebooks to html, markdown, pdf, etc. on git commits. Automates keeping rendered versions of notebooks in-sync with their parents.

## Install/Setup
To install, move the `nbgitconvert` file to the root of your repo and run:
```sh
$ ./nbgitconvert --setup
```
This does two things:
 1. creates a `nbgitconvert.ini` file that tells nbgitconvert which output types should be generated
 2. create a git hook such that nbgitconvert runs everytime a \*.ipynb file is committed.

## the config file
`nbgitconvert.ini` contains a line for every supported output type and whether to convert to that output type. `nbgitconvert` will convert all committed \*.ipynb files to all output types specified in the `nbgitconvert.ini` file.

By default, only html is marked for output. Update the config generated during the setup step as needed. Note that in the sample `nbgitconver.ini` file in this repo all formats have been set to "yes". The rendered notebooks in the `jupyter notebooks/rendered/` directory were created from this config.


## Usage
After running the above setup steps, nbgitconvert will convert any committed \*.ipynb files to the output formats specified in `nbgitconvert.ini`, adding them to the `renders/{output_type}` directories, and commiting those new/updated files.

Assume you've already run the setup steps and are using the default values from `nbgitconvert.ini` (only converts to html). Here are two scenarios:
### you create a new jupyter notebook
 1.	you created a new jupyter notebook named `new_notebook.ipynb`
 2. you git add the notebook ```$ git add new_notebook.ipynb```
 3. you commit: ```$ git commit -m "added a new notebook"```
 4. the prehook runs, generating an html version of your file at `rendered/html/new_notebook.html` and git adds that new file before commiting.
 5. Now when you push your changes to the branch, they'll include the rendered html version of your notebook.

### you make a change to an existing notebook
Since this notebook already existed, let's assume the html version of the notebook also already existed.
 1.	you made a change to an existing notebook named `existing_notebook.ipynb`. Now your jupyter notebook is out of sync with the rendered html version of the notebook.
 2. you git add the notebook ```$ git add existing_notebook.ipynb```
 3. you commit: ```$ git commit -m "updated existing notebook"```
 4. the prehook runs, regenerating the html version of your file at `rendered/html/existing_notebook.html` and git adds that updated file before commiting.
 5. Now when you push your changes to the branch, they'll include the changes to your jupyter notebook and the updated rendered html version of your notebook.


## Notes
 1. nbconvert has issues converting notebooks with spaces in their names to pdf. To be safe, avoid putting spaces in your notebooks' names.
