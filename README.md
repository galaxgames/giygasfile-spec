# giygasfile-spec

Inside this repository is the specification for the giygasfile file format. Giygasfile is a file format for assets used in modern video games and graphical applications. 

## Objectives
The giygasfile format is designed to be simple, and the process of loading a giygasfile's data should be efficient and performant.

## Properties
To acheive the above objectives, the giygasfile format inherits the following properties.

* giygasfiles are best used as post-process artifacts
giygasfiles are designed to be easy and cheap to load. This makes them un-ideal for use as content source files. It is best to use a higher level format to store your content, and then use a processor to build those source files as giygasfiles for application use.

* giygasfiles are **not** portable
To ensure giygasfiles have minimal load-time requirements, giygasfiles are not portable across platforms. For each platform the application supports, a different set of giygasfile assets should be used. This process can be facilitated by a post-process build tool. 
