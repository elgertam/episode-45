Ansible Demo
============

Stolen shamelessly from sysadmincasts (http://bit.ly/1Pvxvok)

Initial set-up
--------------
    # ssh-keyscan adds the hash of an SSH server to known_hosts
    for i in $(ansible all --list-hosts); do
        ssh-keyscan ${i} >> ~/.ssh/known_hosts
    done

    ansible all -m ping --ask-pass

Do a Simple Thing
-----------------

    # install NTP on each box
    ansible-playbook e45-ntp-install.yml

\#FAIL! Yeah, we need to set up SSH key sharing first

Set Up SSH
----------

    # Now we need to generate our SSH key...
    ssh-keygen -t rsa -b 2048 -f ~/.ssh/id_rsa

    # ...and send it to all of our nodes
    ansible-playbook e45-ssh-addkey.yml --ask-pass

    # Did it work?
    ansible all -m ping

(Re)Do a Simple Thing
---------------------

    # install NTP on each box
    ansible-playbook e45-ntp-install.yml

    # make some change to NTP config
    ansible-playbook e45-ntp-template.yml

    # Who needs NTP, anyway?
    ansible-playbook e45-ntp-remove.yml

Install a Website
-----------------

    # install static website on each web node using roles
    ansible-playbook e46-role-site

Visit http://localhost:10080/haproxy?stats and then refresh the page at http://localhost:10080

UPDATE ALL THE NODES (without downtime)
---------------------------------------

    # rolling update
    ansible-playbook e47-rolling.yml

Keep refreshing the two pages to see the update and lack of downtime.
