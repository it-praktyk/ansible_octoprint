Role Name
=========

semuadmin.octoprint

Ansible role to deploy Octoprint and mjpg_stremer on Raspberry Pi running stock Raspbian
lite or full. Should also work on other Debian distributions though webcam support may
depend on the specific hardware.

By default:
- octoprint service will be available on: http://host_ip:5000.
- mjpg_streamer service will be available on: http://host_ip:8080/?action=stream.

The user will be prompted to go through the Setup Wizard on accessing the service for the
first time, but a pre-configured config.yaml template is included with standard configuration
items already set up. These can be amended via the Octoprint admin console.

Based on instructions here:
https://community.octoprint.org/t/setting-up-octoprint-on-a-raspberry-pi-running-raspbian/2337

Requirements
------------

Raspberry Pi model 3 or 4 with SSH enabled. If installing on a 'headless' Raspberry Pi
server, add an empty file named 'ssh' to the boot directory of the SD card to 
enable remote SSH access.

Role Variables
--------------

- `install_octoprint`: true
- `install_webcam`: true
        
- `host_ip`: ip_of_host
- `octoprint_user`: pi
- `install_dir`: "/home/{{ octoprint_user }}"
- `octoprint_port`: 5000

- `webcam_user`: mjpg_streamer
- `webcam_dir`: "{{ install_dir}}/mjpg-streamer/mjpg-streamer-experimental"
- `webcam_port`: 8080
- `webcam_resolution`: "1280x720"
- `webcam_fps`: "10"
- `webcam_type` : "usb" (options are 'usb' or 'raspi')

Dependencies
------------

- Python >=2.7.9<3

Example Playbook
----------------

Install Octoprint with raspberry pi camera support:

```yaml

    - name: Provision octoprint on raspbian
      hosts: ip_address_of_rpi
      become: true
      become_user: pi
      
      vars:
        install_octoprint: true
        install_webcam: true
        host_ip: 192.168.0.18
        webcam_type: raspi

      roles:
      - semuadmin.octoprint
```

License
-------

BSD

Author Information
------------------

semuadmin@noreply.user.github.com
