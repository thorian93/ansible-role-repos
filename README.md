# Ansible Role: Repos

This role configures package repositories on RHEL/CentOS, Debian/Ubuntu, Fedora and openSUSE servers.

[![Ansible Role: Repos](https://img.shields.io/ansible/role/56361?style=flat-square)](https://galaxy.ansible.com/thorian93/repos)
[![Ansible Role: Repos](https://img.shields.io/ansible/quality/56361?style=flat-square)](https://galaxy.ansible.com/thorian93/repos)
[![Ansible Role: Repos](https://img.shields.io/ansible/role/d/56361?style=flat-square)](https://galaxy.ansible.com/thorian93/repos)

## Here be Dragons!

Please review the variables in `vars/` carefully and consider changing the `*_host` variables to point to a mirror near your systems!
Leaving them per default will use the official and central mirrors of the distributors. As this puts load on that servers it is recommended to avoid using them directly. Thanks for your consideration.

## Requirements

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: foobar
      roles:
        - role: thorian93.repos
          become: yes

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    repos_transport_protocol: http

Configure globally if repositories should be contacted via `http` or `https`.

    repos_ubuntu_enable_backports: 'false'

Enable Ubuntu 'Backports' repository. Default: `false`.

    repos_apt_cacher_url: []

Configure a APT-Cacher instance to use for updates.

    repos_custom_repository_urls: [] # Can contain host and port
      # - deb https://superrepo.example/foo/ {{ ansible_lsb.codename }} bar
      # - deb http://apt.cacher.example:3142/ftp.debian.org/debian/ {{ ansible_lsb.codename }} main

If you do not whish to use the predefined templates (see `templates/`) you can build your very own repository list using this variable. **Keep in mind that this variable does not distinguish between operating systems, so you need to make sure the right system gets the right configuration!**

    repos_additional_repository_urls: []
      # - name: "Supersoft"
      #   comment: "Super important software"
      #   url: deb https://supersoft.example/packages/apt stable main

If you want to add repositories additional to the base repositories you can do that by using this variable. Each item gets its own repository file.

## Dependencies

None.

## OS Compatibility
This role ensures that it is not used against unsupported or untested operating systems by checking, if the right distribution name and major version number are present in a dedicated variable named like `<role-name>_stable_os`. You can find the variable in the role's default variable file at `defaults/main.yml`:

    role_stable_os:
      - Debian 10
      - Ubuntu 18
      - CentOS 7
      - Fedora 30

If the combination of distribution and major version number do not match the target system, the role will fail. To allow the role to work add the distribution name and major version name to that variable and you are good to go. But please test the new combination first!

Kudos to [HarryHarcourt](https://github.com/HarryHarcourt) for this idea!

## Example Playbook

    ---
    - name: "Run role."
      hosts: all
      become: yes
      roles:
        - ansible-role-repos

## Contributing

Please feel free to open issues if you find any bugs, problems or if you see room for improvement. Also feel free to contact me anytime if you want to ask or discuss something.

## Disclaimer

This role is provided AS IS and I can and will not guarantee that the role works as intended, nor can I be accountable for any damage or misconfiguration done by this role. Study the role thoroughly before using it.

## License

MIT

## Author Information

This role was created in 2021 by [Thorian93](http://thorian93.de/).
