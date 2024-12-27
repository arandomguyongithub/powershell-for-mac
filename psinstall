import os
import time
import subprocess
from colorama import Fore, Style

def install_requirements():
    print("Installing requirements...")
    time.sleep(1)

    try:
        # Install colorama
        os.system("pip3 install colorama")
        from colorama import Fore, Style
    except Exception as e:
        print(Fore.RED + "Error installing colorama: " + str(e))
        return False
    return True

def install_powershell():
    print(Fore.GREEN + Style.BRIGHT + "Installing PowerShell...")
    time.sleep(1)

    # Install PowerShell on macOS using Homebrew, else skip installation
    if os.name == 'posix':  # macOS/Linux
        try:
            os.system("brew install --cask powershell")
            print(Fore.GREEN + Style.BRIGHT + "PowerShell installed.")
        except Exception as e:
            print(Fore.RED + "Error installing PowerShell: " + str(e))
            return False
    else:
        print(Fore.RED + "PowerShell installation is only supported on macOS in this script.")
        return False
    return True

def create_and_run_script():
    print(Style.NORMAL + Fore.WHITE + "Running script...")

    # Create the powershellmain.py script
    script_path = os.path.expanduser('~/powershellmain.py')
    os.system("touch " + script_path)

    # Check if the file is created
    if not os.path.exists(script_path):
        print(Fore.RED + "Failed to create powershellmain.py.")
        return


hostname = subprocess.getoutput("hostname")
# Write powershellmain.py with raw strings to avoid unicodeescape errors
script_content = r'''import subprocess
import os
from colorama import Fore

hostname = subprocess.getoutput("hostname")
command = input(r"PS C:\Users\powershellmain.py> ")  # Raw string for backslashes

def run_powerShell_command(command):
    """Run the command using PowerShell and capture output."""
    try:
        result = subprocess.run(["pwsh", "-Command", command], capture_output=True, text=True)
        print(result.stdout)
    except Exception as e:
        print(f"Error running PowerShell command: {str(e)}")

if command.lower() == "terminal switch":
    confirm1 = input("Are you sure you want to switch to terminal? (Y/N) ")
    if confirm1.lower() == "y":
        print("Control + C to switch.")
    else:
        print("No action taken.")

elif command.lower() == "terminal cmd":
    cmd2 = input(f"{hostname} ~ % ")
    os.system(cmd2)  # This executes the command in the terminal

elif command.lower() == "uninstall":
    confirm2 = input("Are you sure you want to uninstall and remove this script? (Y/N) ")
    if confirm2.lower() == "y":
        os.system("rm ~/powershellmain.py")
        print(Fore.RED + "Uninstalled")
    else:
        print("Uninstall canceled.")

else:
    # Execute any other command via PowerShell
    run_powerShell_command(command)

# Running another Python script (optional or customized)
try:
    os.system(f"python3 {os.path.expanduser('~/Documents/ps.py')}")
except Exception as e:
    print(f"Error running additional script: {str(e)}")
'''

# Write the script content to powershellmain.py
script_path = os.path.expanduser('~/powershellmain.py')
with open(script_path, 'w') as file:
    file.write(script_content)


    # Check if the file exists after writing
    if os.path.exists(script_path):
        print(Fore.GREEN + f"Successfully created {script_path}.")
    else:
        print(Fore.RED + "Failed to create powershellmain.py after writing.")

    # Execute the script if it exists
    try:
        os.system(f"python3 ~/powershellmain.py")
    except Exception as e:
        print(Fore.RED + f"Error running powershellmain.py: {str(e)}")

def main():
    if not install_requirements():
        return
    if not install_powershell():
        return
    create_and_run_script()

if __name__ == "__main__":
    main()
