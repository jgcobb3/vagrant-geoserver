# ansible-tomcat

An Ansible role for installing Tomcat 7 on Ubuntu via apt.

## Dependencies

- Installs Apache 2 using role dependency azavea.apache2 


## Example Playbook

    - hosts: servers
      roles:
         - { role: stumptownlabs.tomcat }

## License

Apache2
