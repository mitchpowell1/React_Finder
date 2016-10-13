# React_Finder

A commmand line utility for finding the origin of various react pieces and parts

(currently only finds component definitions)

---

## Usage:

* Syntax:

  ```bash
  reactfind [flags] component name
  ```
  
    OR
  
  ```bash
  reactfind -d root_directory
  ```
* Flags:

  * -h | --help:
     Display the help message
  * -p | --partial-match:
     Allow for partial matching of the react component (fuzzy search)
  * -d | --set-root-directory:
     Configure the root directory of the reactfind search (defaults to working directory)
     
