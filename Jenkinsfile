pipeline {
    agent any

    stages {
        stage('Building Custom Network') {
            steps {
                bat 'echo "Creating custom bridge network..." && docker network create --driver bridge elg'
            }
        }
        stage('Creating ElasticSearch Container') {
            steps {
                bat 'echo "Creating ElasticSearch..." && docker run -d --name elasticsearch -p 9200:9200 --network elg --restart always plaulkar/elasticsearch_logstash_grafana:elasticsearch'
            }
        }
        stage('Creating LogStash Container') {
            steps {
                bat 'echo "Creating LogStash..." && docker run -d --name logstash --network elg --restart always plaulkar/elasticsearch_logstash_grafana:logstash'
            }
        }
        stage('Creating Grafana Container') {
            steps {
                bat 'echo "Creating Grafana..." && docker run -d --name grafana --network elg --restart always plaulkar/elasticsearch_logstash_grafana:grafana'
            }
        }
    }
}
