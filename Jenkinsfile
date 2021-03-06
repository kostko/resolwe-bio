node {

    stage('Checkout') {
        // check out the same revision as this script is loaded from
        checkout scm
        // fetch git LFS files from remote and checkout required working tree files
        sh 'git lfs pull'
    }

    stage('Test') {
        // force a rebuild of Tox environments when testing the 'master' branch
        if (env.BRANCH_NAME == 'master') {
            sh 'rm -rf .tox/'
        }
        // use half of all available CPU cores for Django's test processes
        DJANGO_TEST_PROCESSES = sh (
            script: 'python -c "import multiprocessing as mp; print(mp.cpu_count()/2)"',
            returnStdout: true
        ).trim()
        withEnv(["RESOLWE_POSTGRESQL_USER=postgres",
                 "RESOLWE_POSTGRESQL_PORT=55433",
                 "RESOLWE_ES_PORT=59201",
                 // set database name to a unique value
                 "RESOLWE_POSTGRESQL_NAME=${env.BUILD_TAG}",
                 "RESOLWE_DOCKER_COMMAND=sudo docker",
                 "DJANGO_TEST_PROCESSES=${DJANGO_TEST_PROCESSES}"]) {
            // documentation, linters and packaging environments are run first
            // so that if any of them fails, developer will get the feedback
            // right away (rather than having to wait for all ordinary tests to
            // run)
            sh 'tox -e docs'

            sh 'tox -e linters'

            sh 'tox -e packaging'

            sh 'echo "Environment:" && python2.7 --version'
            sh 'tox -e py27'

            sh 'echo "Environment:" && python3.4 --version'
            sh 'tox -e py34'
        }
    }
}
