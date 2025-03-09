# ELK Stack Docker Setup

This repository provides a Docker-based deployment of the ELK (Elasticsearch, Logstash, and Kibana) stack, allowing users to quickly set up a centralized logging system.

## Features
- **Fully Automated Deployment**: Run a single command to set up ELK.
- **Preconfigured Logstash Pipeline**: Includes a sample configuration for ingesting logs.
- **User-Friendly**: Easily customizable for different logging needs.
- **Lightweight & Scalable**: Uses Docker Compose to manage services efficiently.

## Prerequisites
Ensure you have the following installed:
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Installation

Clone the repository:
```sh
git clone https://github.com/UmarShaikh79/docker-elk-stack.git
cd elk-docker-setup
```

Start the ELK stack:
```sh
docker-compose up -d
```

Verify services:
- **Elasticsearch**: [http://localhost:9200](http://localhost:9200)
- **Kibana**: [http://localhost:5601](http://localhost:5601)

## Configuration
### Logstash
Modify `logstash.conf` to adjust the log ingestion pipeline:
```plaintext
input {
  beats {
    port => 5044
  }
}

filter {
  grok {
    match => { "message" => "%{COMBINEDAPACHELOG}" }
  }
}

output {
  elasticsearch {
    hosts => ["http://elasticsearch:9200"]
    index => "logs-%{+YYYY.MM.dd}"
    user => "elastic"
    password => "changeme"
  }
  stdout { codec => rubydebug }
}
```

## Stopping the ELK Stack
To stop the containers, run:
```sh
docker-compose down
```

## Contributing
Contributions are welcome! Feel free to submit issues or pull requests.

### Contributors
- **Muhammad Umar** - [GitHub Profile](https://github.com/UmarShaikh79)

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

