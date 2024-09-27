---
title: Add SQL Server Change Data Capture as a source to eventstream
description: Learn how to add a SQL Server on virtual machine (VM) database (DB)'s Change Data Capture (CDC) feed as a source to an eventstream.
ms.reviewer: spelluru
ms.author: zhenxilin
author: alexlzx
ms.topic: how-to
ms.date: 09/02/2024
ms.search.form: Source and Destination
---

# Add SQL Server on VM  DB (CDC) source to an eventstream (preview) 

This article shows you how to add a SQL Server on VM DB CDC source to an eventstream. 

The SQL Server on VM DB (CDC) source connector for Fabric event streams allows you to capture a snapshot of the current data in a SQL Server database on VM. The connector then monitors and records any future row-level changes to the data. Once these changes are captured in the event stream, you can process this data in real-time and send it to various destinations for further processing or analysis. 

[!INCLUDE [enhanced-capabilities-preview-note](./includes/enhanced-capabilities-preview-note.md)]

[!INCLUDE [new-sources-regions-unsupported](./includes/new-sources-regions-unsupported.md)]

## Prerequisites

- Access to the Fabric **premium workspace** with **Contributor** or higher permissions.
- A running SQL Server on VM database. 
- Your SQL Server on VM database must be configured to allow public access.  
- Enable CDC in your SQL Server on VM database by running the stored procedure `sys.sp_cdc_enable_db`. For details, see [Enable and disable change data capture](/sql/relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server). 

[!INCLUDE [sources-destinations-note](./includes/sources-destinations-note.md)]


## Enable CDC in your SQL Server on VM database

1. Enable CDC for the database.     
        
   ```sql
   EXEC sys.sp_cdc_enable_db; 
   ```
2. Enable CDC for a table using a gating role option. In this example, `MyTable` is the name of the SQL table. 

    ```sql            
    EXEC sys.sp_cdc_enable_table 
       @source_schema = N'dbo', 
       @source_name   = N'MyTable', 
       @role_name     = NULL 
    GO 
    ```

    After the query executes successfully, you enabled CDC in your SQL Server on VM database. 

   ![A screenshot of showing CDC has enabled.](media/add-source-sql-server-change-data-capture/enable-cdc.png)
   
## Add SQL Server on VM database as a source 

1. In Fabric Real-Time Intelligence, select **Eventstream** to create a new eventstream. Make sure the **Enhanced Capabilities (preview)** option is enabled.

   ![A screenshot of creating a new eventstream.](media/external-sources/new-eventstream.png)

1. On the next screen, select **Add external source**.

   ![A screenshot of selecting Add external source.](media/external-sources/add-external-source.png)

## Configure and connect to SQL Server on VM database

[!INCLUDE [sql-server-on-virtual-machine-cdc-source-connector](./includes/sql-server-on-virtual-machine-cdc-source-connector.md)]

You can see the SQL Server on VM DB CDC source added to your eventstream in **Edit** mode.

:::image type="content" source="media/add-source-sql-server-change-data-capture/edit-mode.png" alt-text="A screenshot of the added SQL Server on VM DB CDC source in Edit mode with the Publish button highlighted." lightbox="media/add-source-sql-server-change-data-capture/edit-mode.png":::

To implement this newly added SQL Server on VM DB CDC source, select **Publish**. After you complete these steps, your SQL Server on VM DB CDC source is available for visualization in the **Live view**.

:::image type="content" source="media/add-source-sql-server-change-data-capture/live-view.png" alt-text="A screenshot of the added SQL Server on VM DB CDC source in Live view mode." lightbox="media/add-source-sql-server-change-data-capture/live-view.png":::


## Related content

Other connectors:

- [Amazon Kinesis Data Streams](add-source-amazon-kinesis-data-streams.md)
- [Azure Cosmos DB](add-source-azure-cosmos-db-change-data-capture.md)
- [Azure Event Hubs](add-source-azure-event-hubs.md)
- [Azure IoT Hub](add-source-azure-iot-hub.md)
- [Azure SQL Database Change Data Capture (CDC)](add-source-azure-sql-database-change-data-capture.md)
- [Confluent Kafka](add-source-confluent-kafka.md)
- [Custom endpoint](add-source-custom-app.md)
- [Google Cloud Pub/Sub](add-source-google-cloud-pub-sub.md) 
- [PostgreSQL Database CDC](add-source-postgresql-database-change-data-capture.md)
- [Sample data](add-source-sample-data.md)
- [Azure Blob Storage events](add-source-azure-blob-storage.md)
- [Fabric workspace event](add-source-fabric-workspace.md)