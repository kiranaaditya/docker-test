# jenkins_docker_test_repo
 Testing docker image builds with Jenkins pipeline with Jenkins runner and vscode.


Important notes:



Jenkins restart policy:
* Jenkins restart policy has been changed on containers. It will send a message to the host system to start the container once it stops.
* With docker its easy to control the restart policy by using --restart=Always
* But since podman runs without a daemon, we need to create a systemctl file and then implement the restart policy.
* https://www.redhat.com/sysadmin/podman-features-3#:~:text=If%20the%20containerized%20webserver%20fails,the%20%2D%2Drestart%2Dpolicy%20flag.
* https://docs.podman.io/en/latest/markdown/podman-generate-systemd.1.html
        1028  podman generate systemd --new jenkins-blueocean > ~/.config/systemd/user/jenkins-blueocean.service
        1029  systemctl --user daemon-reload
        1030  systemctl --user start jenkins-blueocean
        1043  systemctl --user enable jenkins-blueocean
        1044  systemctl --user status jenkins-blueocean

* Always use the --user flag whenever we are interacting with the user genrated services.



About starting jenkins without a CSRF protection:
https://unix.stackexchange.com/questions/444177/how-to-disable-the-csrf-protection-in-jenkins-by-default

Podman docs:

* Remote podman executable - https://docs.podman.io/en/latest/markdown/podman-remote.1.html
* Issues with remote podman socket - https://github.com/containers/podman/issues/12493
* Issues with remote podman socket - https://github.com/containers/podman/issues/4234
* Podman networking - https://www.tutorialworks.com/podman-host-networking/
