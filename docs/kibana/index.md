---
layout: default
title: Kibana
nav_order: 11
has_children: true
has_toc: false
---

# Kibana

Kibana is the default visualization tool for data in Elasticsearch. It also serves as a user interface for the Open Distro for Elasticsearch [Security](../security-configuration/) and [Alerting](../alerting/) plugins.


## Run Kibana using Docker

You *can* start Kibana using `docker run` after [creating a Docker network](https://docs.docker.com/engine/reference/commandline/network_create/) and starting Elasticsearch, but the process of connecting Kibana to Elasticsearch is significantly easier with a Docker Compose file.

1. Run `docker pull amazon/opendistro-for-elasticsearch-kibana:1.3.0`.

1. Create a [`docker-compose.yml`](https://docs.docker.com/compose/compose-file/) file appropriate for your environment. A sample file that includes Kibana is available on the Open Distro for Elasticsearch [Docker installation page](../install/docker/#sample-docker-compose-file).

   Just like `elasticsearch.yml`, you can pass a custom `kibana.yml` to the container in the Docker Compose file.
   {: .tip }

1. Run `docker-compose up`.

   Wait for the containers to start. Then see [Get started with Kibana](#get-started-with-kibana).

1. When finished, run `docker-compose down`.


## Run Kibana using the RPM or Debian package

1. If you haven't already, add the `yum` repositories specified in steps 1--2 in [RPM](../install/rpm) or the `apt` repositories in steps 2--3 of [Debian package](../install/deb).
1. `sudo yum install opendistroforelasticsearch-kibana` or `sudo apt install opendistroforelasticsearch-kibana`
1. Modify `/etc/kibana/kibana.yml` to use `elasticsearch.hosts` rather than `elasticsearch.url`.
1. `sudo systemctl start kibana.service`
1. To stop Kibana:

   ```bash
   sudo systemctl stop kibana.service
   ```


### Configuration

To run Kibana when the system starts:

```bash
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable kibana.service
```

You can also modify the values in `/etc/kibana/kibana.yml`.


## Run Kibana using the tarball

1. Download the tarball:

   ```bash
   curl https://d3g5vo6xdbdb9a.cloudfront.net/tarball/opendistroforelasticsearch-kibana/opendistroforelasticsearch-kibana-1.2.0.tar.gz -o opendistroforelasticsearch-kibana-1.2.0.tar.gz
   ```

1. Download the checksum:

   ```bash
   curl https://d3g5vo6xdbdb9a.cloudfront.net/tarball/opendistroforelasticsearch-kibana/opendistroforelasticsearch-kibana-1.2.0.tar.gz.sha512 -o opendistroforelasticsearch-kibana-1.2.0.tar.gz.sha512
   ```

1. Verify the tarball against the checksum:

   ```bash
   shasum -a 512 -c opendistroforelasticsearch-kibana-1.2.0.tar.gz.sha512
   ```

   On CentOS, you might not have `shasum`. Install this package:

   ```bash
   sudo yum install perl-Digest-SHA
   ```

1. Extract the TAR file to a directory and change to that directory:

   ```bash
   tar -zxf opendistroforelasticsearch-kibana-1.2.0.tar.gz
   cd opendistroforelasticsearch-kibana
   ```

1. If desired, modify `config/kibana.yml`.

1. Run Kibana:

   ```bash
   ./bin/kibana
   ```


## Get started with Kibana

1. After starting Kibana, you can access it at port 5601. For example, [http://localhost:5601](http://localhost:5601){:target='\_blank'}
1. Log in with the default username `admin` and password `admin`.
1. Choose **Try our sample data** and add the sample flight data.
1. Choose **Discover** and search for a few flights.
1. Choose **Dashboard**, **[Flights] Global Flight Dashboard**, and wait for the dashboard to load.
