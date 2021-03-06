---
title: RabbitMQ Transport
summary: An overview of the RabbitMQ transport
reviewed: 2018-05-18
component: Rabbit
related:
 - samples/rabbitmq/simple
 - samples/rabbitmq/native-integration
redirects:
 - nservicebus/rabbitmq/configuration-api
 - nservicebus/rabbitmq
tags:
 - Transport
---

Provides support for sending messages over [RabbitMQ](https://www.rabbitmq.com/) using the [RabbitMQ .NET Client](https://www.nuget.org/packages/RabbitMQ.Client/).

WARNING: The transport is not compatible with RabbitMQ broker version 3.3.X and below.

## Transport at a glance

|Feature                    |   |  
|:---                       |---
|Transactions |None, ReceiveOnly
|Pub/Sub                    |Native
|Timeouts                   |Native
|Large message bodies       |Broker can handle arbitrary message size within available resources, very large messages via DataBus
|Scale-out             |Competing consumer
|Scripted Deployment        |Not supported
|Installers                 |Mandatory

## Configuring the endpoint

To use RabbitMQ as the underlying transport:

snippet: rabbitmq-config-basic

The RabbitMQ transport requires a connection string to connect to the broker. See [connection settings](/transports/rabbitmq/connection-settings.md) for options on how to provide the connection string.


### Routing topology

partial: topology

## Advantages and disadvantages


### Advantages

 * Provides [native reliability](https://www.rabbitmq.com/reliability.html) and [high-availability](https://www.rabbitmq.com/ha.html) features.
 * Offers a native publish-subscribe mechanism; therefore it doesn't require NServiceBus persistence for storing event subscriptions.
 * Wide range of [supported clients](https://www.rabbitmq.com/devtools.html) allows for integrating the system with applications written in other languages using native RabbitMQ features.
 * Supports the [competing consumers](https://www.enterpriseintegrationpatterns.com/patterns/messaging/CompetingConsumers.html) pattern out of the box. Messages are received by instances in a round-robin fashion without additional configuration.


### Disadvantages

 * Doesn't handle [network partitions](https://www.rabbitmq.com/partitions.html) well; partitioning across a WAN requires using dedicated features.
 * Requires careful consideration for duplicate messages, e.g. using the [outbox](/nservicebus/outbox/) feature or making all endpoints idempotent.
 * Many organizations don't have the same level of expertise with RabbitMQ, as with other technologies, such as SQL Server, so it may require additional training.
 * Might require covering additional costs of [commercial RabbitMQ license and support](https://www.rabbitmq.com/services.html).
