# 🔍 Vulnerability Summary
Generated on: Wed  7 May 09:00:23 CEST 2025

Found 6 vulnerabilities

## System Dependencies

⚠️ openssl (HIGH) → Fixed in: 1.1.1f-2

## Library Dependencies

### From Raw Labs

#### In subproject: core

⚠️ com.fasterxml.jackson.core:jackson-databind (HIGH) → Fixed in: 2.13.4
  • com.raw-labs:core:1.0.0 -> org.apache.spark:spark-core_2.12:3.3.0 -> com.fasterxml.jackson.core:jackson-databind:2.13.3

#### In subproject: api

⚠️ com.fasterxml.jackson.core:jackson-databind (HIGH) → Fixed in: 2.13.4
  • com.raw-labs:api:1.0.0 -> com.fasterxml.jackson.core:jackson-databind:2.13.3

⚠️ org.springframework:spring-web (CRITICAL) → Fixed in: 5.3.21
  • com.raw-labs:api:1.0.0 -> org.springframework:spring-web:5.3.20

#### In subproject: common

⚠️ com.fasterxml.jackson.core:jackson-databind (HIGH) → Fixed in: 2.13.4
  • com.raw-labs:common:1.0.0 -> com.fasterxml.jackson.core:jackson-databind:2.13.3

⚠️ org.apache.commons:commons-text (CRITICAL) → Fixed in: 1.10.0
  • com.raw-labs:common:1.0.0 -> org.apache.commons:commons-text:1.9

### From Third-party

⚠️ org.apache.logging.log4j:log4j-core (CRITICAL) → Fixed in: 2.15.0
  • org.apache.hadoop:hadoop-client:3.3.1 -> org.apache.logging.log4j:log4j-core:2.14.1

⚠️ org.postgresql:postgresql (HIGH) → Fixed in: 42.2.26
  • org.postgresql:postgresql:42.2.25

