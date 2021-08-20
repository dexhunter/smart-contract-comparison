# Comparison between tape & caliper

|                   | caliper                                     | tape             |
|-------------------|---------------------------------------------|------------------|
| developer         | pswg                                        | twgc             |
| language          | nodejs                                      | golang           |
| version           | 4.0.2                                       | 1.0.2            |
| support platforms | Fabric v1.x v2.x, Besu, Etherum, FISCO BCOS | Fabric v1.4 v2.x |
| Metrics           | Success Rate,Read/TX TPS, Read/TX Latency   | TPS              |


## tape
    
    
### advantage

* smaller overhead
* community support

### disadvantage

* lack functionalities
    * success rate
    * read-related metrics
* only support Fabric

## caliper

### advantage

* support more platforms
* custom functions
    * dynamic arguments
    * initialize function

### disadvantage

* large overhead