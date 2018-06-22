Creating items using the 1Password command-line tool and ansible
=========

Requirements
----------------

Set up the 1pass command-line tool : https://support.1password.com/command-line-getting-started/

Example Playbook
----------------

playbook.yml

```
- name: add items to 1pass
  hosts: localhost
  gather_facts: false
  vars:
    one_pass_data_dir: "/tmp"
    one_pass_signinaddress: "XXXXXXX.1password.com"
    one_pass_emailaddress: "XXXXXX@XXXXXXXX.com"
    one_pass_secretkey: "{{ lookup('file', '~/.1pass_secret') }}"
    one_pass_master_password: "{{ lookup('file', '~/.1pass_master') }}"

    one_pass_vault: "XXXXXXXXXX"

  tasks:
      - include_role:
            name: ansible-role-1pass
        vars:
            one_pass_template: "database"
            one_pass_title: "XXXXXXXXXX"
            database_type: "mysql"
            database_hostname: "XXXXXXXXXXXXX"
            database_port: "3306"
            database_name: "dbname"
            database_username: "dev_user"
            database_password: "XXXXXXXXXXXXXXX"
      - include_role:
            name: ansible-role-1pass
        vars:
            one_pass_template: "login"
            one_pass_title: "Login [test] Dev"
            login_username: "test_login"
            login_password: "XXXXXXXXXXX"
            login_notes_plain: "test_notes"
      - include_role:
            name: ansible-role-1pass
        vars:
            one_pass_template: "secure_note"
            one_pass_title: "Note [test]"
            secure_note_plain: "test_note"
      - include_role:
            name: ansible-role-1pass
        vars:
            one_pass_template: "document"
            one_pass_title: "Document test"
            document_path: "~/testfile"
```

Author Information
------------------
Artem Yushkov

DevOps@Ambisafe
