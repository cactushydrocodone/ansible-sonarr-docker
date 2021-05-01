ansible-sonarr-docker
=========
[![Build Status](https://travis-ci.com/MedievalRoadie/ansible-nzbget-docker.svg?branch=main)](https://travis-ci.com/MedievalRoadie/ansible-nzbget-docker)

Starts an instance of [hotio/sonarr](https://hotio.dev/containers/sonarr/)

Requirements
------------

Mainly docker. I've taken to using [this geerlingguy playbook](https://galaxy.ansible.com/geerlingguy/docker/) to orchestrate installation of Docker & Docker Compose.

This is also set up to use my own [traefik playbook](https://github.com/MedievalRoadie/ansible-traefik-docker) to do easy reverse proxying. 

Role Variables
--------------

* ```docker_config_dir```: a directory to output the container config to for persistance. Defaults to */opt/docker*
* ```proxy_network_name```: the name of the docker network used for proxying to traefik. Defaults to *traefik-proxy*
* ```sonarr_url```: the url to access nzbget through, via traefik. Defaults to *sonarr.tld.com*
* ```watchtower_update```: determines if watchtower (if running) should include this container in its runs. Defaults to *true*
* ```user_uid```: the user id of the user running sonarr. Defaults to *1000*
* ```user_gid```: the user group id to run sonarr. Defaults to *1000*

Dependencies
------------

(none)

Example Playbook
----------------

    - hosts: servers
      roles:
      - role: medievalroadie.docker_sonarr
        vars:
          docker_config_dir: /a/different/dir
          proxy_network_name: proxy_network
          nzbget_url: sonarr.mydomain.com
          watchtower_update: false
          user_uid: 1002
          user_gid: 1002
