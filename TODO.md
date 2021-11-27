# Rasa X Setup for Arch

1. curl -sSL -o install.sh https://storage.googleapis.com/rasa-x-releases/0.23.3/install.sh 
2. Change this in the `install.sh` file 
    - `apt get install python3`
    + `sudo pacman -S python3`
    - `ansible-galaxy install angstwad.docker_ubuntu`
    + `ansible-galaxy install geerlingguy.docker`
3. sudo bash ./install.sh
4. Leads to error 
5. Modify the downloaded file `rasa_x_playbook.yml` 
```
    -   roles:
    -     - role: angstwad.docker_ubuntu
    -       when: ansible_testing is not defined
```
6. Modify the install Script 
    - `wget -qO rasa_x_playbook.yml https://storage.googleapis.com/rasa-x-releases/0.23.3/rasa_x_playbook.yml`
7. Agree to Terms of Service 
8. `$ docker-compose up -d`
9. `$ sudo python rasa_x_commands.py create --update admin me <PASSWORD>` 
10. Visit <IP>/login
    - Enter the <PASSWORD> 
11. Git integration 
    - Activate Experimental features (Account -> Experimental)
    - Create git repo for assistant 
    - Create RSA keys:
        - `$ ssh-keygen -t rsa -b 4096 -f git-deploy-key`
        - Creates a public and private key 
    - Add public key to git repo (Settings -> Deploy keys). Give write access 
    - Create `repository.json` 
```
{
    "repository_url": "<SSH url from Git>",
    "ssh_key": "<Private key>",
    "target_branch": "<Branch>"
}
```
12. `$ curl --request POST --url "http://<HOST>/api/projects/default/git_repositories?api_token=<API_TOKEN>" --header 'content-type: application/json' --data-binary @repository.json`
