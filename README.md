# java-gc-demo-supplement
This is the repo with scripts and setup for comparing performance of various Java 23 GC Types 

### gcapp directory:
- runme = This is the script to run the spring boot application with different GC Types:
  The script is interractive, will ask choice to run with G1GC/ZGC/Shenandoah.
  > Note:
  > 1) Please change JAVA_HOME to the correct JDK-23 path
  > 2) The java argument -XX:ActiveProcessorCount=2 is added to limit CPU use to 2 cores, this way we can identify bottlenecks easily.
    
  

- testme = This script runs 30 iterations of sending curl POST request to the gcdemo app, with the following steps
LOOP:
  1) POST /api/memory/load/500
  2) Sleep
  3) POST /api/memory/load/800
  4) Sleep
     
> Note: The script runs for ~12min, you can change the number of iterations or the sleep to have different load pattern.

### docker-compose.yml:
This docker-compose file will 
- Setup Grafana+Prometheus
- Setup Prometheus datasource in Grafana
- Setup Prometheus scraping setting to scrape http://localhost:8080/actuator/prometheus endpoint for the gcdemo app.
> **Note: The Grafana login user/pass: admin/password**

### Tests performed:
1) OpenJDK (build 23.0.1+11-39)
   - G1GX - 2 tests (12 min duration each)
   - ZGC - 2 tests (12 min duration each)
   - Shenandoah - application did not start with OpenJDK.

2) Amazon Corretto (build 23.0.1+8-FR)
   - G1GX - 2 tests (12min duration each)
   - ZGC - 2 tests (12 min duration each)
   - Shenandoah - 2 tests (12 min duration each)


### Screenshots:
This directory contains images of Grafana dashboard for each test. 

> Note: I have copied the data folder for Grafana in this repo, so the Dashboard should already be there.
> 
> Prometheus GC Demo-1734719334875.json -> This is the exported Grafana dashboard json.

### results-comparison.xlsx
This Excel sheet contains the comparison between the Java 23 GC Types based on the metrics observed on the Grafana Dashboard.
