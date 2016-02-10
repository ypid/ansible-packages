Getting started
===============

.. contents::
   :local:


Export mode
-----------

Here's an example playbook you can use to export package lists for Debian jessie:

.. code:: yaml

   ---
   - name: Export package lists for Debian jessie
     hosts: localhost
     gather_facts: False
     vars:
       ansible_pkg_mgr: 'apt'
       ansible_virtualization_role: 'host'
       packages__mode: 'export'
       packages__export_directory: '{{ inventory_dir | realpath }}/../../apt_package_lists'
       packages__contrib_enabled: True
       packages__non_free_enabled: True
       packages__export_classes:
         - 'core'
         - 'base'
         - 'live_system'
         - 'desktop_explorer'
         - 'desktop_normal'
         - 'desktop_school'
       packages__export_distributions:
         - ansible_distribution: 'Debian'
           ansible_distribution_release: 'jessie'

     roles:
       - role: ypid.packages
         tags: [ 'role::packages' ]
