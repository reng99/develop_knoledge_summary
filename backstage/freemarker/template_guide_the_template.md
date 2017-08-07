## the template

### 1. overall structure

Templates are in fact programs you write in language called `FLT`(for FreeMarker Template Language). This is a quite simple programming language designed for writing templates and nothing else.

comment format:`<#-- and -->`


### 2. directive

There are two kind of FTL tags:

- Start-tag:<#directivename parameters>

- End-tag:</#directicename>

This is similar to HTML or XML syntax, except that the tag name starts with `#`.If the directive doesn't have nested content(content between the start-tag and the end-tag), you must use the start-tag with no end-tag. For  example you write `<#if something>...</#if>`,but just `<#include somthing>` as FreeMarker knows that the `include` directive can't have nested content.


### 3. expression

refer to [http://freemarker.org/docs/dgui_template_exp.html](http://freemarker.org/docs/dgui_template_exp.html)


### 4. interpolation



