To build and start the container run:

docker build -f Dockerfile . -t rpmrepo
docker run -p 8000:8000 -v ~/<path-to-out/RPMS>:/rpms -it rpmrepo --name rpmrepo_container


To add the repo to a target system, add the rpm repo host's ip to below and run it:

echo -e "[test-repo]
name=Local test repo
baseurl=http://<BUILD MACHINE IP HERE>:8000
enabled=1" | sudo tee -a /etc/yum.repos.d/test.repo; sudo chmod 644 /etc/yum.repos.d/test.repo

dnf clean all

dnf repolist
