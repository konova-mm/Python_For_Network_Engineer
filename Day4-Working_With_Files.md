## Working with files
In real life, in order to make full use of everything covered before this section you need to understand how to work with files.
When working with network equipment (and not only), files can be:
- configurations (simple, non-structured text files)
  - They are discussed in this section
    
- configuration templates
  - usually a special file format.

- files with connection options
  - usually they are structured files in some particular format: YAML, JSON, CSV

- other Python scripts
-----
This section covers simple text files. For example, Cisco configuration file.
There are several aspects to working with files:
- opening/closing
- reading
- writing
-----
### File opening
To start working with a file you have to open it.
