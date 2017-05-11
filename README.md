# ansible-raw_telnet
Hey! As Michael DeHaan said, "Telnet is a obviously a very insecure protocol, completely insecure in fact, and we strongly want to discourage usage. We would likely refuse the pull request, to be honest — it is just asking for a world of hurt should MITM possibilities arise". Nevertheless, if you just have no other choice, you could use this simple playbook workaround.
------------

You will need this on your Ansible host:

``sudo apt-get install telnet``

or

``sudo yum install telnet``

You will need pexpect package, which is accessible via pip. Pip is installed along with Ansible, so just go with:

``sudo pip install pexpect``

Create playbook in .yml format

(See example raw_telnet.yml in repo)
    
Edit your responces based on eqipment prompt (replace username with login, etc.)

Edit your password (better store in Ansible Vault, this is not secure!)

Edit your exit string (optional)

Edit your responces/replace with vars (optional)

Run playbook specifying your command, i.e.

``ansible-playbook raw_telnet.yml  -e '{"COMMAND":"show stp"}'``
