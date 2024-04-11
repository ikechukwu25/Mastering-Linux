# USING AI AND NATURAL LANGUAGE TO ADMINISTER LINUX SYSTEMS

ShellGPT is a command line tool, built in Python, that uses the OpenAI API to leverage ChatGPT capabilities to generate shell commands, code snippets, or scripts. It brings the AI power directly into your terminal. 

ShellGPT is built in Python which comes pre-installed in all Linux distros. 


To set up ShellGPT on your Linux system, follow these steps:

- Ensure Python and Pip are installed, and note their versions. Check Python and Pip versions:
  - To check, run `python3 --version`. You can check python.org to see the latest version of python to compare.
  - `pip3 --version`. 
- `sudo apt install python3-pip`: This command is used to install the Python 3 package manager called Pip on a Debian-based system (such as Ubuntu). This command installs the Pip package manager for Python 3.
- `sudo apt install python3-venv`: To install the Python 3 virtual environment module on Debian-based systems, such as Ubuntu. This step is necessary to create isolated Python environments.
- `Mkdir shellgpt`: A virtual environment should have a directory to keep all it’s files organised. A directory should be created in the user’s home directory
- `cd shellgpt`: Move into the shell directory.
- `python3 -m venv gpt_cli`: To create a virtual environment named "gpt_cli" using Python's built-in venv module. This virtual environment allows you to isolate the dependencies for a specific Python project, providing a clean environment for the project to run in without affecting the global Python environment. This command uses Python's built-in venv module to create a virtual environment named "gpt_cli".
  - `-m venv`: This option specifies that you want to use the venv module to create a virtual environment.
- `source bin/activate`: it’s used to activate a virtual environment in a Unix-like shell, such as Bash or Zsh. This command is typically used after creating a virtual environment using Python's venv module or virtualenv. Remember to move into the gpt_cli directory before running the command.

N/B: When you sign out our close the shell, you’ll have to activate it again from by going through the same process

- `pip3 install shell-gpt`: used to install shell got in the virtual environment. Run this in the virtual environment
- Create an open AI API key by visiting https://platform.openai.com/, click on View keys and generate key. 
- Run `export OPENAI_API_KEY="insert_copied_key"` to export the key.
- Run `env | grep OPENAI_API_KEY` to check that the variable was created and it has the desired value. 
- All new variables are temporarily stored for the current session, to permanently store, you have to add it to an initialisation file such as `.bashrc`. 
- To make it permanent,
  - Open bashrc: `vim ~/.bashrc`
  - Insert the following line : `export OPENAI_API_KEY=skLddLufpdYFcoWqspZILIT3BlbkFJYZgvSMXVApGGeerOiCu3` (export + variable)
 

See usage below: 

- `sgpt "Distance to Mars"`: This command prompts ShellGPT to generate text based on the given prompt "Distance to Mars".
- `sgpt -s “update my system”` or  `sgpt --shell “update my system”` = This command provides the command to run based on the given prompt "update my system".
- `sgpt --execute --shell "update my system" or sgpt -s -e "update my system"`: This command runs the command directly based on the given prompt "update my system".
- `sgpt --code "Bash script that prompts the user for a directory and creates an archive."`: This command generates Bash script code based on the given prompt "Bash script that prompts the user for a directory and creates an archive."
