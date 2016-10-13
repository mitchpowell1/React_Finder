#!/bin/bash
PARTIALFLAG=false
if [ -f .findreact_root ]; then
    ROOTPATH=$( cat .findreact_root )
else
    ROOTPATH='.'
fi
INPUT=""
while test $# -gt 0; do
    case "$1" in
        -h | --help)
            echo "reactfind syntax: \$ reactfind [flags] [component name]"
            echo "Note: place all flags before component name"
            echo "###############################################"
            echo "# Flags:"
            echo "#"
            echo "#  -h | --help - Display the help message <-- You are here"
            echo "#"
            echo "#  -p | --partial-match - Accept partial matches to your component name"
            echo "#"
            echo "#  -d | --set-root-directory - Set the directory to be searched (defaults to PWD if not configured)"
            echo "#      Note: the root directory will be persistently configured within a file called .findreact_root."
            echo "#         This file will be excluded from git if the working directory is configured as a git repository" 
            echo "###############################################"
            exit 0
            ;;

        -p | --partial-match)
            PARTIALFLAG=true
            shift
            ;;

        -d | --set-root-directory)
            shift
            if [ -d $1 ]; then
                echo $1 > ./.findreact_root
                #if [ -f ".git/info/exclude" && (grep -q ".findreact_root" ".git/info/exclude") ]; then
                #    echo "directory info not saved in .git/info/exclude"
                #fi
            else
                echo "The directory $1 does not exist"
                exit 1
            fi
            exit 0
            ;;
            
        -*)
            echo "$1 is not a valid flag, use -h or --help for a list of valid flags"
            exit 1
            ;;
            
        *)
            INPUT=$1
            if [ "$PARTIALFLAG" = "true" ]; then
                INPUT=".*$INPUT.*"
            fi
            break
            ;;
    esac
done
if [ -n "$INPUT" ]; then
    if [ "$PARTIALFLAG" = "true" ]; then
        echo "Searching $ROOTPATH for definitions of components whose names contain \"$1\""
    else
        echo "Searching $ROOTPATH for a component definition for $INPUT"
    fi
    echo "Root directory can be configured with the -d flag. (Use -h for more info)"
    echo ""
    grep "class $INPUT extends [(React | Component)]" -H -i -r $ROOTPATH | cut -d: -f1 
else
    echo "Please use the following syntax => $./reactfind [options] COMPONENTNAME"
fi
