# Moxygen

Moxygen is a Doxygen XML to Markdown converter for C++ developers who want a minimal beautiful and  documentation solution for their projects.

The code is based on `doxygen2md` with extra options for generating output files, custom templates, and generating multi page documentation.

Moxygen is currently used in conjunction with GitBook to generate the API documentation for LibSourcey, which can be viewed [here](http://sourcey.com/libsourcey/).

## Usage

1. Add `GENERATE_XML=YES` to your `Doxyfile` first.
2. Run `doxygen` to generate the XML documentation.
3. Install `moxygen` like so: `npm install moxygen -g`.
4. Run `moxygen` providing the folder location of the XML documentation as the first argument ie. `{OUTPUT_DIRECTORY}/xml`.  
  ```
  Usage: moxygen [options] <doxygen directory>

  Options:

    -h, --help             output usage information
    -V, --version          output the version number
    -a, --anchors          add anchors to internal links
    -g, --groups           output doxygen groups into separate files
    -o, --output <file>    output file (must contain %s when using groups)
    -l, --language <lang>  programming language
    -t, --templates <dir>  custom templates directory
    -q, --quiet            quiet mode
  ```

## Multi Page Output

Moxygen supports the doxygen [groups](http://www.stack.nl/~dimitri/doxygen/manual/grouping.html#modules) syntax for generating multi page documentation. Every [\defgroup](http://www.stack.nl/~dimitri/doxygen/manual/commands.html#cmddefgroup) in your source code will be parsed and output into a separate markdown file, with internal reference updated accordingly.

Example:

```
moxygen --anchors --groups --output api-%s.md /path/to/doxygen/xml
```

## Example

To get a feel for how Moxygen works you can play with the example which is located in the [example](/example) folder. The example contains:

* Documented C++ example code
* A `Doxyfile` file (for doxygen 1.8.13)
* Pre-generated XML output in [example/xml](/example/xml)
* Pre-generated output Markdown files in [example/doc](/example/doc)

The rebuild the example XML you can run `doxygen` from within the example folder.

Now you can build the example documentation with the following command from within the example folder:

```
moxygen --anchors --groups --output=doc/api-%s.md xml
```
