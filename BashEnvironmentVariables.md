Where Bash Looks for Permanent Environment Variables
====================================================

 Shell Type |      Interactive      |    Non-Interactive
------------|-----------------------|---------------------
Login       | <ol><li>`/etc/profile`</li><li>`~/.bash_profile`</li><li>`~/.bash_login`</li><li>`~/.profile`</li></ol>     | <ol><li>`/etc/profile`</li><li>`~/.bash_profile`</li><li>`~/.bash_login`</li><li>`~/.profile`</li></ol>
Non-Login   | <ol><li>`/etc/bash.bashrc`</li><li>`~/.bashrc`</li></ol> | `$BASH_ENV`


**Note: Although .bashrc is not necessarily executed on login, it is common for .profile or .bash_profile to include a line prompting
.bashrc to be loaded. Accordingly, an environment variable can be set in .bashrc and .bash_profile can execute .bashrc so the variable
only needs to be set in one place.**
