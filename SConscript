from building import *
import os

# Import environment variables
Import('env')

# Get the current working directory
cwd = GetCurrentDir()

# Initialize include paths and source files list
path = [os.path.join(cwd, 'Include')]
src = [os.path.join(cwd, 'Source', 'Templates', 'system_stm32h7rsxx.c')]

# Map microcontroller units (MCUs) to their corresponding startup files
mcu_startup_files = {
    'STM32H7R3xx': 'startup_stm32h7r3xx.s',
    'STM32H7R7xx': 'startup_stm32h7r7xx.s',
    'STM32H7S3xx': 'startup_stm32h7s3xx.s',
    'STM32H7S7xx': 'startup_stm32h7s7xx.s',
}

# Check each defined MCU, match the platform and append the appropriate startup file
for mcu, startup_file in mcu_startup_files.items():
    if mcu in env.get('CPPDEFINES', []):
        if rtconfig.PLATFORM in ['gcc', 'llvm-arm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'gcc', startup_file)]
        elif rtconfig.PLATFORM in ['armcc', 'armclang']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'arm', startup_file)]
        elif rtconfig.PLATFORM in ['iccarm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'iar', startup_file)]
        break

# Define the build group
group = DefineGroup('STM32H7RS-CMSIS', src, depend=['PKG_USING_STM32H7RS_CMSIS_DRIVER'], CPPPATH=path)

# Return the build group
Return('group')