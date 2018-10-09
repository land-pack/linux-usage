#SSH login without password

Everytime, when I login my remote server, I have to input those redundancy command. so if I can simple call those with one word will be good.

###Use nickname instead of long command

	ssh frank@192.168.1.203 -p 9001
Yes, we can do it by edite our bash profile. `vim ~/.bash_profile`

	# rest of command ...
	PATH="/Library/Frameworks/Python.framework/Versions/3.6/bin:${PATH}"
	export PATH
	PATH=$PATH:/opt/metasploit-framework/bin
	export PATH=$PATH:/opt/metasploit-framework/bin
	function ssh_dev() {
	     ssh frank@192.168.1.203 -p 9001
	}
	export PATH="/usr/local/opt/openssl/bin:$PATH"
To let the system know you have made some change, do the following command:

	source ~/.bash_profile

And now, you can easily visit your remote server by:

	ssh_dev
But when you try it, you still need to input your password, it's boring too. so ..

### Use public key instead of password

	ssh-keygen

and always hit `Enter`. and then copy your public key to remote server by use:

	ssh-copy-id frank@192.168.1.203 -p 9001

Also, some system require you get a permission to the auth file. so you have to login with your password and do it.

	ssh frank@192.168.1.203 -p 9001 # or ssh_dev
	# input your password
	# and find a file name as `.ssh/authorized_keys`
	chmod 640 .ssh/authorized_keys

### Test it

For now, you can easily login your server with:

	ssh_dev 