# About the Project

This scripts are only for local test setups and not for Production!

In some lessons virtual machines are used, as an alternative, Docker containers are a interresting choice - specially for M1 macs which are not supporting e.g. Virtual Box this approach would be an alternative.

## Virtual Machines for following lessons

- Batch Processing-Systeme
- Datenbanksysteme - Konzepte und Modelle

## Getting started

### Batch Processing

Note that for Batch processing you need to build the container by your own locally for this purpose the createDockerContainer.sh is provided.

1. `createDockerContainer.sh`
2. `docker-compose up -d`
3. use the container

Getting files into the container
- using the `docker container cp` command
- using the mounted volume volume_hadoop

Example code snippets for wordcount example:

    /hadoop-3.3.4/bin/hadoop fs -mkdir -p input/wordcount
    /hadoop-3.3.4/bin/hadoop fs -put wordcount-input.txt input/wordcount

    /hadoop-3.3.4/bin/hadoop jar hadoop-simple-examples.jar at.fhv.hadoop.examples.WordCountDriver input/wordcount output/wordcount

### Database Systems

Because this setup consists of different containers, only the docker compose file needs to be started.

- `docker-compose up -d`

