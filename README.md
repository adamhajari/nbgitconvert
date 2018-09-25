# nbgitconvert
a git hook to render jupyter notebooks to html, markdown, pdf, etc. on git commits

## Install
To install, move nbgitconvert to the root of your repo and run:
```sh
$ ./nbgitconvert --setup
```

## Usage
After running the above setup steps, nbgitconvert will convert any *.ipynb files to the specified format, adding the to the `renders/` directory, and commiting any changes.
