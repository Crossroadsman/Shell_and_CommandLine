Backticks
=========

Anything typed between backticks is evaluated by the shell and the result of that evaluation is inserted into the command.

For example:

```
sudo chown -R `whoami` /usr/local
```

Bash will evaluate whoami and replace the backticked text with the result of that evaluation, so if the user was 'rosie'
then the command that Bash would end up executing would be:

```
sudo chown -R rosie /usr/local
```
