Scenario There is a customer who came to you with a problem to have a custom linux
command for his operations. Your task is to understand the problem and create a linux
command via bash script as per the instructions.
Command name - internsctl
Command version - v0.1.0
Section A
1. I want a manual page of command so that I can see the full documentation of the command.
For example if you execute the command
man ls
as output we get the doc and usage guidelines. Similarly if I execute man internsctl I want
to see the manual of my command.

Output:
sudo cp internsctl.1 /usr/share/man/man1/
sudo mandb

2. Each linux command has an option --help which helps the end user to understand the use
cases via examples. Similarly if I execute internsctl --help it should provide me the
necessary help

Output:

#!/bin/bash

# Define the version
VERSION="v0.1.0"

# Function to display help message
display_help() {
    echo "Usage: internsctl [OPTIONS] DIRECTORY"
    echo "Custom Linux command for operations."
    echo
    echo "Options:"
    echo "  -h, --help          Display this help message."
    echo "  -v, --version       Display the version of internsctl."
    echo "  -a, --action DIR    Perform a custom action on the specified directory."
    echo
    echo "Examples:"
    echo "  internsctl -a /path/to/directory"
    echo "  internsctl --version"
    echo
}

# Function to display version
display_version() {
    echo "internsctl $VERSION"
}

# Parse command line options
while [[ $# -gt 0 ]]; do
    case $1 in
        -h|--help)
            display_help
            exit 0
            ;;
        -v|--version)
            display_version
            exit 0
            ;;
        -a|--action)
            if [ -n "$2" ]; then
                DIRECTORY=$2
                # Add your custom action here
                echo "Performing custom action on directory: $DIRECTORY"
                shift 2
            else
                echo "Error: -a|--action option requires a directory argument."
                exit 1
            fi
            ;;
        *)
            echo "Error: Unknown option '$1'. Use --help for usage information."
            exit 1
            ;;
    esac
done

# Check if the DIRECTORY argument is provided
if [ -z "$DIRECTORY" ]; then
    echo "Error: DIRECTORY argument is required. Use --help for usage information."
    exit 1
fi

3. I want to see version of my command by executing
internsctl –version

Output :
#!/bin/bash

# Define the version
VERSION="v0.1.0"

# Function to display help message
display_help() {
    echo "Usage: internsctl [OPTIONS] DIRECTORY"
    echo "Custom Linux command for operations."
    echo
    echo "Options:"
    echo "  -h, --help          Display this help message."
    echo "  -v, --version       Display the version of internsctl."
    echo "  -a, --action DIR    Perform a custom action on the specified directory."
    echo
    echo "Examples:"
    echo "  internsctl -a /path/to/directory"
    echo "  internsctl --version"
    echo
}

# Function to display version
display_version() {
    echo "internsctl $VERSION"
}

# Parse command line options
while [[ $# -gt 0 ]]; do
    case $1 in
        -h|--help)
            display_help
            exit 0
            ;;
        -v|--version)
            display_version
            exit 0
            ;;
        -a|--action)
            if [ -n "$2" ]; then
                DIRECTORY=$2
                # Add your custom action here
                echo "Performing custom action on directory: $DIRECTORY"
                shift 2
            else
                echo "Error: -a|--action option requires a directory argument."
                exit 1
            fi
            ;;
        *)
            echo "Error: Unknown option '$1'. Use --help for usage information."
            exit 1
            ;;
    esac
done

# Check if the DIRECTORY argument is provided
if [ -z "$DIRECTORY" ]; then
    echo "Error: DIRECTORY argument is required. Use --help for usage information."
    exit 1
fi
Now, when you execute internsctl --version, it will display the version of the internsctl command.







Section B
I want to execute the following command for -
Part1 | Level Easy
I want to get cpu information of my server through the following command:
$ internsctl cpu getinfo
Expected Output -
I want similar output as we get from lscpu command
---
I want to get memory information of my server through the following command:
$ internsctl memory getinfo
Expected Output
I want similar output as we get from free command


OUTPUT :
#!/bin/bash

# Define the version
VERSION="v0.1.0"

# Function to display help message
display_help() {
    echo "Usage: internsctl [OPTIONS] COMMAND"
    echo "Custom Linux command for operations."
    echo
    echo "Options:"
    echo "  -h, --help          Display this help message."
    echo "  -v, --version       Display the version of internsctl."
    echo
    echo "Commands:"
    echo "  cpu getinfo         Get CPU information (similar to lscpu)."
    echo "  memory getinfo      Get memory information (similar to free)."
    echo
    echo "Examples:"
    echo "  internsctl cpu getinfo"
    echo "  internsctl memory getinfo"
    echo "  internsctl --version"
    echo
}

# Function to display version
display_version() {
    echo "internsctl $VERSION"
}

# Function to get CPU information
get_cpu_info() {
    lscpu
}

# Function to get memory information
get_memory_info() {
    free
}

# Parse command line options
while [[ $# -gt 0 ]]; do
    case $1 in
        -h|--help)
            display_help
            exit 0
            ;;
        -v|--version)
            display_version
            exit 0
            ;;
        cpu)
            if [ "$2" == "getinfo" ]; then
                get_cpu_info
                exit 0
            else
                echo "Error: Invalid usage of 'cpu' command. Use 'internsctl cpu getinfo'."
                exit 1
            fi
            ;;
        memory)
            if [ "$2" == "getinfo" ]; then
                get_memory_info
                exit 0
            else
                echo "Error: Invalid usage of 'memory' command. Use 'internsctl memory getinfo'."
                exit 1
            fi
            ;;
        *)
            echo "Error: Unknown option or command '$1'. Use --help for usage information."
            exit 1
            ;;
    esac
done

# If no command is provided, display help
echo "Error: No command provided. Use --help for usage information."
exit 1
This script introduces two new commands: cpu getinfo and memory getinfo. When you run internsctl cpu getinfo, it will display CPU information similar to lscpu. Similarly, running internsctl memory getinfo will show memory information similar to free. Adjust the script based on your specific needs and further customize the output format if necessary.


Part2 | Level Intermediate
I want to create a new user on my server through the following command:
$ internsctl user create <username>
Note - above command should create user who can login to linux system and access his home
directory
---
I want to list all the regular users present on my server through the following command:
$ internsctl user list
---
If want to list all the users with sudo permissions on my server through the following command:
$ internsctl user list --sudo-only

OUTPUT
#!/bin/bash

# Define the version
VERSION="v0.1.0"

# Function to display help message
display_help() {
    echo "Usage: internsctl [OPTIONS] COMMAND [ARGS]"
    echo "Custom Linux command for operations."
    echo
    echo "Options:"
    echo "  -h, --help          Display this help message."
    echo "  -v, --version       Display the version of internsctl."
    echo
    echo "Commands:"
    echo "  user create <username>      Create a new user with login access and home directory."
    echo "  user list                   List all regular users."
    echo "  user list --sudo-only       List users with sudo permissions."
    echo
    echo "Examples:"
    echo "  internsctl user create john_doe"
    echo "  internsctl user list"
    echo "  internsctl user list --sudo-only"
    echo "  internsctl --version"
    echo
}

# Function to display version
display_version() {
    echo "internsctl $VERSION"
}

# Function to create a new user
create_user() {
    if [ -n "$1" ]; then
        sudo useradd -m -s /bin/bash "$1"
        echo "User '$1' created successfully."
    else
        echo "Error: Missing username. Use 'internsctl user create <username>'."
        exit 1
    fi
}

# Function to list all regular users
list_users() {
    cut -d: -f1 /etc/passwd
}

# Function to list users with sudo permissions
list_sudo_users() {
    getent group sudo | cut -d: -f4 | tr ',' '\n'
}

# Parse command line options
while [[ $# -gt 0 ]]; do
    case $1 in
        -h|--help)
            display_help
            exit 0
            ;;
        -v|--version)
            display_version
            exit 0
            ;;
        user)
            shift
            case $1 in
                create)
                    shift
                    create_user "$1"
                    exit 0
                    ;;
                list)
                    shift
                    if [ "$1" == "--sudo-only" ]; then
                        list_sudo_users
                    else
                        list_users
                    fi
                    exit 0
                    ;;
                *)
                    echo "Error: Invalid usage of 'user' command. Use 'internsctl user create <username>' or 'internsctl user list [--sudo-only]'."
                    exit 1
                    ;;
            esac
            ;;
        *)
            echo "Error: Unknown option or command '$1'. Use --help for usage information."
            exit 1
            ;;
    esac
done

# If no command is provided, display help
echo "Error: No command provided. Use --help for usage information."
exit 1
This script now supports three commands related to user management:

internsctl user create <username> - Create a new user with login access and a home directory.
internsctl user list - List all regular users.
internsctl user list --sudo-only - List users with sudo permissions.




Part3 | Advanced Level
By executing below command I want to get some information about a file
$ internsctl file getinfo <file-name>
Expected Output [make sure to have the output in following format only]
xenonstack@xsd-034:~$ internsctl file getinfo hello.txt
File: hellot.txt
Access: -rw-r--r--
Size(B): 5448
Owner: xenonstack
Modify: 2020-10-07 20:34:44.616123431 +0530
In case I want only specific information then I must have a provision to use options
$ internsctl file getinfo [options] <file-name>
--size, -s to print size
--permissions, -p print file permissions
--owner, o print file owner
--last-modified, m
Expected Output with options
If I want to obtain the size of the specified file only, I should be able to use the following
command:
xenonstack@xsd-034:~$ internsctl file getinfo --size hello.txt
5448
If I want to obtain the permissions of the specified file only, I should be able to use the following
command:
xenonstack@xsd-034:~$ internsctl file getinfo --permissions hello.txt
-rw-r--r--
If I want to obtain the owner of the specified file only, I should be able to use the following
command:
xenonstack@xsd-034:~$ internsctl file getinfo --owner hello.txt
xenonstack
If I want to obtain the last modified time of the specified file only, I should be able to use the
following command:
xenonstack@xsd-034:~$ internsctl file getinfo --last-modified hello.txt
2020-10-07 20:34:44.616123431 +0530
OUTPUT:
#!/bin/bash

# Define the version
VERSION="v0.1.0"

# Function to display help message
display_help() {
    echo "Usage: internsctl [OPTIONS] COMMAND [ARGS]"
    echo "Custom Linux command for operations."
    echo
    echo "Options:"
    echo "  -h, --help          Display this help message."
    echo "  -v, --version       Display the version of internsctl."
    echo
    echo "Commands:"
    echo "  file getinfo <file-name>                    Get information about a file."
    echo "    Options:"
    echo "      --size, -s            Print file size."
    echo "      --permissions, -p     Print file permissions."
    echo "      --owner, -o           Print file owner."
    echo "      --last-modified, -m   Print last modified time."
    echo
    echo "Examples:"
    echo "  internsctl file getinfo hello.txt"
    echo "  internsctl file getinfo --size hello.txt"
    echo "  internsctl file getinfo --permissions hello.txt"
    echo "  internsctl file getinfo --owner hello.txt"
    echo "  internsctl file getinfo --last-modified hello.txt"
    echo "  internsctl --version"
    echo
}

# Function to display version
display_version() {
    echo "internsctl $VERSION"
}

# Function to get information about a file
get_file_info() {
    FILENAME=$1

    # Check if the file exists
    if [ ! -e "$FILENAME" ]; then
        echo "Error: File '$FILENAME' does not exist."
        exit 1
    fi

    # Default output
    OUTPUT="File: $FILENAME"

    # Check options
    while [[ $# -gt 0 ]]; do
        case $1 in
            --size|-s)
                OUTPUT+="\nSize(B): $(stat -c %s "$FILENAME")"
                ;;
            --permissions|-p)
                OUTPUT+="\nAccess: $(stat -c %A "$FILENAME")"
                ;;
            --owner|-o)
                OUTPUT+="\nOwner: $(stat -c %U "$FILENAME")"
                ;;
            --last-modified|-m)
                OUTPUT+="\nModify: $(stat -c %y "$FILENAME")"
                ;;
            *)
                # Unknown option
                echo "Error: Unknown option '$1'. Use --help for usage information."
                exit 1
                ;;
        esac
        shift
    done

    echo -e "$OUTPUT"
}

# Parse command line options
while [[ $# -gt 0 ]]; do
    case $1 in
        -h|--help)
            display_help
            exit 0
            ;;
        -v|--version)
            display_version
            exit 0
            ;;
        file)
            shift
            case $1 in
                getinfo)
                    shift
                    get_file_info "$1" "${@:2}"
                    exit 0
                    ;;
                *)
                    echo "Error: Invalid usage of 'file' command. Use 'internsctl file getinfo <file-name> [options]'."
                    exit 1
                    ;;
            esac
            ;;
        *)
            echo "Error: Unknown option or command '$1'. Use --help for usage information."
            exit 1
            ;;
    esac
done

# If no command is provided, display help
echo "Error: No command provided. Use --help for usage information."
exit 1
This script now supports the file getinfo command with various options (--size, --permissions, --owner, --last-modified)
