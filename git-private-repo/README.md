## Git private repo
### Building an image
```shell
docker image build -t git:1 .
```

### Running the Docker container
```shell
docker compose up
```

### Create remote repository inside git container
```shell
docker container exec -it git bash
mkdir /home/git/repos/repo-name.git
chown -R git /home/git/repos/repo-name.git
git init --bare /home/git/repos/repo-name.git
Ctrl-d
```

### SSH with git container
#### Generate and copy SSH key
```shell
# Generate SSH key
ssh-keygen -t ed25519 -C "remote-git-access"

# Copy public key from cat output
cat ~/.ssh/id_ed25519.pub

# Put the public key inside authorized_keys
docker container exec -it git bash
echo "ssh-ed25519 ..." > /home/git/.ssh/authorized_keys
Ctrl-d
```

#### Establish connection using SSH
```shell
ssh -p 2222 git@localhost
Ctrl-d
```

#### Cloning repositories
```shell
git clone ssh://git@localhost:2222/home/git/repos/repo-name.git
cd repo-name

# Check remote url
git config --get remote.origin.url
git remote show origin
```
