## Level 0
	
ssh bandit0@bandit.labs.overthewire.org -p 2220

## Level 0 -> Level 1

We use ‘ls’ to list directory contents. It shows a file ‘readme’ in home directory. We use the ‘cat’ command to print the content of ‘readme’. It shows ‘boJ9jbbUNNfktd78OOpsqOltutMc3MY1’

## Level1 -> Level 2

We use ‘boJ9jbbUNNfktd78OOpsqOltutMc3MY1’ from the last level to login into the next ssh session.
‘ssh bandit1@bandit.labs.overthewire.org’
Then, paste the password
We are now logged into the ssh session.
Using ‘ls’ we get a file with the name ‘-’/.
We cannot use ‘cat -’ as it will just print out STDIN.
We can use full path of the file like ‘cat /home/bandit1/-’ which gives us ‘CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9’

## Level 2 -> Level 3

ssh into the next session by using the password found in the previous level
‘ssh bandit2@bandit.labs.overthewire.org’
Using ‘ls’ we get ‘spaces in this filename’.
We need to use \ to escape the space in between the words of the filename.
Or we can use tab autocompletion to do it for us by writing ‘cat spaces’ then pressing tab to autocomplete the filename.
Password:’UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK’

## Level 3 -> Level 4

ssh into next session
Using ‘ls’ we get the ‘inhere’ folder.
‘cd inhere’ and then using ‘ls -a’ we get ‘.hidden’ file.
‘cat .hidden’ we get the password ‘pIwrPrtPN36QITSp3EQaw936yaFoFgAB’

## Level 4 -> Level 5

ssh into next session
Using ‘ls’ we get the ‘inhere’ folder.
Inside ‘inhere’ folder using ‘ls’ we get
‘-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09’.
We can use command ‘file -- *’ list all the file types where ‘--’ is used to signify the end of arguments like ‘-r’, ‘-f’ etc. After ‘--’ we can use positional argument like ‘$’ ‘%’ ‘*’ etc.
We can also use the full path like ‘file /home/bandit4/inhere/*’
We get,

/home/bandit4/inhere/-file00: data
/home/bandit4/inhere/-file01: data
/home/bandit4/inhere/-file02: data
/home/bandit4/inhere/-file03: data
/home/bandit4/inhere/-file04: data
/home/bandit4/inhere/-file05: data
/home/bandit4/inhere/-file06: data
/home/bandit4/inhere/-file07: ASCII text
/home/bandit4/inhere/-file08: data
/home/bandit4/inhere/-file09: data

We see ‘-file07’ is ASCII text, we use ‘cat -- -file07’ or ‘cat /home/bandit04/inhere/-file07’.
We get ‘koReBOKuIDDepwhWk7jZC0RTdopnAYKh’

## Level 5 -> Level 6

There is ‘inhere’ folder in home directory
It contains many ‘maybe’ folders. We use ‘find’ command to search the file with the following properties as given in the challenge

human-readable
1033 bytes in size
not executable

We use ‘man find’ which gives more information about the find command, we find a ‘-size’ argument. 
Finally the command,
‘find . -size 1033c’ where c stands for bytes, we get ‘./maybehere07/.file2’.
Using cat on the file we get the password for the next ssh session ‘DXjZPULLxYr17uwoI01bNLQbtFemEgo7’.

## Level 6 -> Level 7

File Properties:
owned by user bandit7
owned by group bandit6
33 bytes in size
It is similar to the previous level. We use the find command with arguments -size -user -group.

‘find / -size 33c -user bandit7 -group bandit6’
We get ‘/var/lib/dpkg/info/bandit7.password’
Using cat we get the password ‘HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs’

## Level 7 -> Level 8

Password for the next ssh session is next to the word ‘millionth’
We use the cat command on the file ‘data.txt’ and then pipe it to ‘grep millionth’ to search the word millionth. We get the password ‘cvX2JJa4CFALtqS87jk27qwqGhBM9plV’

## Level 8 -> Level 9

It says in the problem that password is the only line of text that occurs once. So we need to use the ‘uniq’ command but it does not work if the lines are not adjacent as it says in the man page, it also says to sort the lines or use ‘sort -u’. I sorted the line first and then piped the uniq command.

‘sort data.txt | uniq -c -’
And we get the password for next session ‘UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR’

## Level 9 -> Level 10

It says that the password is preceded by several ‘=’. When we use cat command on the given file it produces many unprintable characters and some printable characters. We can find the printable characters using strings command and then use grep command to find the password.

‘strings data.txt | grep =’
We get the password ‘truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk’

## Level 10 -> Level 11

We use ‘man base64’ to get more information about the command. It says in the ‘man base64’ command that we can use -d to decode data.
So,
‘base64 -d data.txt’
We get
‘The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR’

