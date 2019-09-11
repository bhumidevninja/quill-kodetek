<h1 align="center">
  Quill-Nexent
</h1>
<p align="center">  
  <a href="https://npmjs.com/package/quill" title="Version">
    <img src="https://img.shields.io/npm/v/quill.svg" alt="Version">
  </a>  
</p>
[Quill](https://quilljs.com/) is a modern rich text editor built for compatibility and extensibility.

We ran into an issue when trying to add the devextreme html editor to the project:
https://js.devexpress.com/Documentation/18_2/ApiReference/UI_Widgets/dxHtmlEditor/

The issue here is that in order for the html editor to work we also need to add Quill to the project. Since we use bower for package management, we tried to add the quill bower package (bower install quill) but it did not work. You can try this yourself and you will notice the errors in the console. However adding the same package through npm resolved the issue but using npm here will create other issues, like having to write custom grunt code for wiring dependencies that are management through npm.

so we can solve the issue with the bower package by creating our own custom bower package for quill and hosting it on github. (bower can install packages from github) We should also modify the package so that when we run grunt serve wiredep will include the correct reference to the quill.js file to the index.html file.

**Notes:** Need to update this package whenever there is new version of quill(https://github.com/quilljs/quill/releases) released.

## How it works
[1] By `npm install` quill package installed in node_modules.
 
[2] we have also copyfiles dependecy in package.json, so it will also installed in node_modules.

[3] while doing npm install, we have postinstall script in package.json, 
    it will copy all the files from node_modules/quill/dist/* and past in root folder. 

## Steps to use

[1] Add dependecy in bower.json
```html
"quill-kodetek": "1.3.7"
or
"quill-kodetek": "https://github.com/bhumidevninja/quill-kodetek/archive/v1.3.7.zip"
or
"quill-kodetek": "https://github.com/bhumidevninja/quill-kodetek/archive/v1.3.7.tar.gz"
```
[2] install bower.json
    
## Steps to update
[1] clone repo. 

[2] check version of quill in package.json, if its not same as letest release of quill change to letest version.

[3] `npm install`

[4] commit and push changes.

[5] generate tag same as quill latest release like: vx.x.x

[6] Go to your consumer project in which you want to use and add following in bower.json
```html
"quill-kodetek": "[pushedtag]"
or
"quill-kodetek": "https://github.com/bhumidevninja/quill-kodetek/archive/[pushedtag].zip"
or
"quill-kodetek": "https://github.com/bhumidevninja/quill-kodetek/archive/[pushedtag].tar.gz"
```
or just change package path if you already have package installed. 

[7] ``bower install``

[8] add 
```html <div style="width: 100%" dx-html-editor="htmlEditorOptions"></div>``` to view file.

[9] add scope variable as `$scope.htmlEditorOptions` in controller 
```html
$scope.htmlEditorOptions = {
        toolbar: {
            items: [
                "undo", "redo", "separator",
                {
                    formatName: "size",
                    formatValues: ["8pt", "10pt", "12pt", "14pt", "18pt", "24pt", "36pt"]
                },
                {
                    formatName: "font",
                    formatValues: ["Arial", "Courier New", "Georgia", "Impact", "Lucida Console", "Tahoma", "Times New Roman", "Verdana"]
                },
                "separator", "bold", "italic", "strike", "underline", "separator",
                "alignLeft", "alignCenter", "alignRight", "alignJustify", "separator",
                {
                    formatName: "header",
                    formatValues: [false, 1, 2, 3, 4, 5]
                }, "separator",
                "orderedList", "bulletList", "separator",
                "color", "background", "separator",
                "link", "image", "separator",
                "clear", "codeBlock", "blockquote"
            ]
        },
        mediaResizing: {
            enabled: true
        }
    };
```

[10] `grunt serve`

if every thing worked fine, you have successfully updated package. 