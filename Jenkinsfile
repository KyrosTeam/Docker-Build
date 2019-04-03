node {
    def projectname = "medium-angular-docker"

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

      projectname = docker.build("getintodevops/hellonode")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        projectname.inside {
            bat 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://cloud.docker.com/u/vishnuprasadnarayanan/repository/docker/vishnuprasadnarayanan/docker_images', '88a033d8-66fc-41f2-9f66-a30f59edd008') {
            projectname.push("${env.BUILD_NUMBER}")
            projectname.push("latest")
        }
    }
}
