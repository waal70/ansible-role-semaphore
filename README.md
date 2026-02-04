waal70.semaphore
=========

Docker Compose project for Semaphore UI <https://semaphoreui.com/> Open Source edition
Started out with the excellent <https://github.com/CorentinTh/it-tools>
Contains the following (altered) settings:

ANSIBLE_HOST_KEY_CHECKING: "False"
SEMAPHORE_SCHEDULE_TIMEZONE: "Etc/Amsterdam"

Because my main repository uses a secrets repository, the volume mappings reflect a folder where this repo is based

Additional tasks
----------------

* This role will (pre-)create the directories used for the volume mapping, and set their owner to 1001, as the container seems to default to using 1001 as the user. This is in order to prevent permission errors.
* The role will perform a git clone of the private repository to the relevant path, so that you may refer to this from within Semaphore
* The role 


Getting it up and running
-------------------------

I have not figured out a way to have the inventory dynamic (yet), so retrieve a list of your hosts as they currently are by issuing a ```ansible-inventory --list --yaml``` to get a static version of the inventory. The downside of this is of course that you will have to update it on changes.
In that file, add the ```ansible_ssh_private_key_file: /home/semaphore/ansible/[path to key]```. If you use certificate backed SSH-keys, you should generate a semaphore pair that has a long(er) validity.
Also, set the ```private_repo``` variable to not contain any Jinja2 templates, as that seems not to work.

Enter your vault passphrase in the project definition inside semaphore.

Volume mappings
---------------

* path-to-secrets-repo:/home/semaphore/ansible:ro

Dependencies
------------

waal70.portainer

License
-------

[GPLv3](https://www.gnu.org/licenses/gpl-3.0.html#license-text)

Author Information
------------------

Unless otherwise noted, this entire repository is (c) 2026 by André (waal70). [See github profile](https://github.com/waal70)

Please contact me if you need a commercial license for any of these files
