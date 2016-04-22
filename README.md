`dockerized-rundeck` builds a Docker image and then runs a Docker container containing Rundeck. Rundeck can then be used to invoke Docker commands on the host (this is achieved by exposing the Docker socket). The Docker container is created the first time `dockerized-rundeck` is invoked.

    ./dockerized-rundeck
    # open Rundeck at http://localhost:4440/ (login: admin, password:admin)

Please read [Using Docker-in-Docker for your CI or testing environment? Think twice.](http://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci) for more information.
