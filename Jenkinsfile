#!/usr/bin/env groovy
def mongoImage = docker.image("mongo:2.6.12")
def alpineImage = docker.image("alpine:latest")
mongoImage.pull()
alpineImage.pull()

stage("DB dependency") {
  mongoImage.withRun { mongo ->
    alpineImage.inside("--link=${mongo.id}:mongo") {
      sh "nc -v mongo 27017"
    }
  }
}

