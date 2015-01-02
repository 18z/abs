Appendix H. Important Files
附錄H. 重要的檔案

startup files

These files contain the aliases and environmental variables made available to Bash running as a user shell and to all Bash scripts invoked after system initialization.

/etc/profile
Systemwide defaults, mostly setting the environment (all Bourne-type shells, not just Bash [1])
系統層級上的環境設定

/etc/bashrc
systemwide functions and aliases for Bash
系統層級上(涵蓋每一個使用者)的Bash設定檔

$HOME/.bash_profile
user-specific Bash environmental default settings, found in each user's home directory (the local counterpart to /etc/profile)
針對特定使用者的bash環境設定檔，可在使用者加目錄中找到。

$HOME/.bashrc
user-specific Bash init file, found in each user's home directory (the local counterpart to /etc/bashrc).	Only interactive shells and user scripts read this file. See Appendix M for a sample .bashrc file.

logout file

$HOME/.bash_logout
user-specific instruction file, found in each user's home directory. Upon exit from a login (Bash) shell, the commands in this file execute.

data files

/etc/passwd
A listing of all the user accounts on the system, their identities, their home directories, the groups they belong to, and their default shell. Note that the user passwords are not stored in this file, [2] but in /etc/shadow in encrypted form.

system configuration files

/etc/sysconfig/hwconf
Listing and description of attached hardware devices. This information is in text form and can be extracted and parsed.

bash$ grep -A 5 AUDIO /etc/sysconfig/hwconf	      
class: AUDIO
 bus: PCI
 detached: 0
 driver: snd-intel8x0
 desc: "Intel Corporation 82801CA/CAM AC'97 Audio Controller"
 vendorId: 8086
 

Note	
This file is present on Red Hat and Fedora Core installations, but may be missing from other distros.

Notes

[1]	
This does not apply to csh, tcsh, and other shells not related to or descended from the classic Bourne shell (sh).

[2]	
In older versions of UNIX, passwords were stored in /etc/passwd, and that explains the name of the file.
