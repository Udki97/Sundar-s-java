def call(body) {

  def config = [:]
  body.resolveStrategy = Closure.DELEGATE_FIRST
  body.delegate = config
  body()

  node('any') {
    try {
      def mvnHome = tool "${config.maven_tool ?: 'Maven 3.3.9'}"
      env.JAVA_HOME = tool "${config.java_tool ?: 'JAVA_8'}"
      def projectDirectory = "${config.project_directory ?: '.'}"

      if (config.cron_string) {
        properties([pipelineTriggers([cron("${config.cron_string}")])])
      } else {
        properties([pipelineTriggers([])])
      }

      stage('Source Checkout') {
        echo 'Source Checkout started...'
        checkout scm
      }

      stage('Build') {
        echo 'Build started...'
      }
    }
  }
