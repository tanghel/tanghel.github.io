# Using MkDocs

To install the utilities, run the following command as administrator:

```
choco install mkdocs
```

To start the documentation in the browser, navigate in command prompt to the root folder of the documentation and run the command:

```
mkdocs serve
```

When the documentation is ready to deploy, stop the running server in the command prompt using `Ctrl-C`, then run the command: 

```
mkdocs build
```

Now the documentation can be pushed on github!

In GitHub Desktop, commit the changes, then don't forget to also click on Push in the upper right corner