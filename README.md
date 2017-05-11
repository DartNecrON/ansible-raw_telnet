# ansible-raw_telnet
Hey! As Michael DeHaan said, "Telnet is a obviously a very insecure protocol, completely insecure in fact, and we strongly want to discourage usage. We would likely refuse the pull request, to be honest — it is just asking for a world of hurt should MITM possibilities arise". Nevertheless, if you just have no other choice, you could use this simple playbook workaround.

You will need this on your Ansible host:

sudo apt-get install telnet

or

yum install telnet

You will need pexpect package, which is accessible via pip. Pip is installed along with Ansible, so just go with:

pip install pexpect

Create playbook in .yml format

hosts: <your inventory file group>
gather_facts: false
connection: local
tasks:
name: telnet,login and execute command
ignore_errors: true
expect:
command: telnet "{{ inventory_hostname }}"
responses:
(?i)username: "admin"
(?i)password: "12345"
(?i)#: "{{COMMAND}}\r\nlogout\r\nexit\r\nquit"
echo: yes
register: telnet_output
name: Debug output
debug: var=telnet_output.stdout_lines
    
Edit your responces based on eqipment prompt (replace username with login, etc.)

Edit your password (better store in Ansible Vault, this is not secure!)

Edit your exit string (optional)

Edit your responces/replace with vars (optional)

#Run playbook specifying your command
i.e.
ansible-playbook raw_telnet.yml  -e '{"COMMAND":"show stp"}'
