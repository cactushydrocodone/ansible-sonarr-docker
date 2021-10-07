ansible-sonarr-docker
=========
[![Build Status](https://travis-ci.com/MedievalRoadie/ansible-sonarr-docker.svg?branch=main)](https://travis-ci.com/MedievalRoadie/ansible-sonarr-docker)

Starts an instance of [hotio/sonarr](https://hotio.dev/containers/sonarr/)

Requirements
------------

Mainly docker. I've taken to using [this geerlingguy playbook](https://galaxy.ansible.com/geerlingguy/docker/) to orchestrate installation of Docker & Docker Compose.

This is also set up to use my own [traefik playbook](https://github.com/MedievalRoadie/ansible-traefik-docker) to do easy reverse proxying. 

Role Variables
--------------

* ```sonarr_docker_config_dir```: a directory to output the container config to for persistance. Defaults to */opt/docker*
* ```sonarr_proxy_network_name```: the name of the docker network used for proxying to traefik. Defaults to *traefik-proxy*
* ```sonarr_url```: the url to access sonarr through, via traefik. Defaults to *sonarr.tld.com*
* ```sonarr_watchtower_update```: determines if watchtower (if running) should include this container in its runs. Defaults to *true*
* ```sonarr_user_uid```: the user id of the user running sonarr. Defaults to *1000*
* ```sonarr_user_gid```: the user group id to run sonarr. Defaults to *1000*
* ```sonarr_download_dir```: directory where downloads are initially placed
* ```sonarr_media_dir```: media library directory

Dependencies
------------

(none)

Example Playbook
----------------

    - hosts: servers
      roles:
      - role: medievalroadie.docker_sonarr
        vars:
          sonarr_docker_config_dir: /a/different/dir
          sonarr_proxy_network_name: proxy_network
          sonarr_url: sonarr.mydomain.com
          sonarr_watchtower_update: false
          sonarr_user_uid: 1002
          sonarr_user_gid: 1002
