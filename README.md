# windows-kernel-debugging
How to create a setup for windows kernel debugging using WinDbg and VMware Workstation.

## Requirements
1. Installed debugging tools for windows, you can found it [here](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/)
2. Clean Windows 10 machine (in VMware workstation)

## Configure the symbols server
Microsoft publishes symbols to every windows version, using symbols we can see functions names and global vars and more. The public symbols are extremely important to the debugging session.

Create local directory (c:\symbols) for symbols caching.

Add to your host machine system environment variables the symbol server path:

Open cmd as Administrator in your host machine and run: `set _NT_SYMBOL_PATH=srv*c:\symbols*https://msdl.microsoft.com/download/symbols`

## Setup
1. Check that you have a ping between the host and the guest (if you don't have a ping try to configure the network adapter from the workstation to bridged)
2. Open cmd as Administrator in your guest machine
3. Run: bcdedit /debug on
4. Run: bcdedit /dbgsettings net hostip:{hostIP} port:{port}
5. Save the output key in your host machine
6. Restart the computer
7. Open windbg, File->Kernel Debug->NET, enter the port that you choose and the output key
8. Break into the debugger using CTRL+Break
9. Run in windbg: .reload /f (in order to load the kernel symbols)
10. Ensure that all the symbols are loaded using: lm
 
Now you got a kernel debugging session.

DONE!!!
