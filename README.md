# Pimcore Data Director Bundle

formerly known as Pimcore Import Plugin

Feature-rich import and export bundle to connect external systems to Pimcore

* * *

## What does this plugin do?

This plugin imports data from external XML, JSON, CSV, Excel data sources (for example from an ERP system), stores them to an intermediate raw data table, and then creates / updates data objects, assets and documents with this data.

In the Pimcore backend GUI you can define which data is to be extracted from the import source and assign it to the object fields of your Pimcore objects. All Pimcore data types are supported for import. Also the import of assets and documents is possible (including editing metadata, tags etc.).

During the import, data can be modified and adapted to your data model. This plug-in provides extensive functionality and a convenient user interface and is a battle-tested solution for importing structured data into Pimcore objects, assets and documents. It reduces the effort of programming individual interfaces and reduces the time to commissioning your Pimcore project.

![Import workflow](doc/images/dataflow.jpg)

It is also possible to export data of the fields you want - including data from relations, images / thumbnails etc. With the intelligent caching system exports are really fast as export data gets updated in the moment when an object gets saved (in the background, so saving does not take any longer) and not when the export is requested. For exports we already provide lots of ready-to-be-used templates:
* CSV exports
* CSV as zip file including assets
* JSON exports
* JSON as zip file incl. assets
* XML exports
* XML exports as zip file incl. assets

This way you can one the one hand create / edit objects, assets and documents in your Pimcore. On the other hand you can use this bundle to create fully customizable REST API endpoints.

It is also possible to not only generate those export documents but you can also specify what to do with the export document: the bundle already ships with the follwoing ready-to-be-used result action templates:
* upload export document via (S)FTP, AWS S3 and other cloud storage providers
* send export document via email

With the automatic mapping functionalities and the provided templates setting up imports and exports is a matter of minutes - in most cases without any programming necessary. But of course if you want to adjust import or export data, you can by using callback functions.

For an overview how to set up imports and exports, please see our [tutorial videos](https://www.youtube.com/playlist?list=PL4-QRNfdsdKIfzQIP-c9hRruXf0r48fjt).

## How to get the plugin

You can buy this plugin in the [Blackbit Shop](https://shop.blackbit.de/de/pimcore-modul-bb-import).

* * *

## Advantages compared to own import implementation

* Performance:
    * Data is only imported if nothing has changed since the last import
    * If an object has not changed during import, it does not need to be saved
    * Export data gets updated when objects change, so it is already prepared in the moment an export gets requested
* Flexibility:
    * Imports and exports are customizable to data source and your Pimcore data model
    * Supports all Pimcore elements including data objects, object bricks, field collections, assets and documents
    * Supports importing tags and properties
* Minimization of programming effort: Only data modifications from the data source require minimal programming
* Comfort functions: 
    * Automatically extract raw data fields from import resources
    * Automatically map raw data fields to Pimcore class fields
    * Optimize inheritance
    * Replace placeholders (for example to generate texts automatically)
    * Automatic translation (with DeepL API)
    * Error monitoring / notification of imports
    * Revert imports
     
* * *

## Workflow

### Step 1: Import XML, Excel and CSV into Pimcore

This plugin has proven itself in many e-commerce and master data management projects and has been developed according to the needs of our customers.

The aim of the plug-in is to import information from upstream systems into the objects of Pimcore, there appropriately enrich them with further information and publish them via Pimcore itself or via a downstream system such as an online shop.

The import always takes place in two steps: In the first step, an intuitive user interface determines which columns of a CSV file or which attributes of an XML / JSON document should be imported into Pimcore.

A preview shows directly if the raw data fields are set up correctly. The import reads the data into an "intermediate table" so the user can see which data was imported from the upstream system before it is further processed in the next step.

![Import workflow](doc/images/setup-raw-data-fields.png)

### Step 2: Mapping Attributes via Drag-and-Drop

In the second step, the information from the intermediate table is assigned to the attributes of the classes. Thise mappings get individually defined in the Pimcore backend UI via drag-and-drop.

There one or more key attributes get set so that the import process can be repeated and existing objects get updated.

The attribute mapping can also be used to modify the source data. For each field assignment, a callback function can be specified, which, for example, performs date format operations or other calculations on the basis of one or multiple imported or existing attributes of the current object.

![Attribute mapping](doc/images/attribute-mapping.png)

* * *

## Further highlights at a glance

* File-based imports (monitoring of a directory and automatic import on new files), for example for:
  * automatic asset imports into the Pimcore (e.g. from a network drive)
  * automatic mapping of assets to Pimcore objects by file name
* Import multiple files (CSV, XML, JSON, Excel) from a source directory with automatic dataset deduplication
* Import from a URL as a data source
* Import data from Pimcore objects:
  * Migrate data from one field type to another without data loss
  * dynamic mass data manipulation (currently that is not possible in the Pimcore grid (for example, increase prices by 10%))
* Import of documents (filling of the editables)
* Generate response documents
  * generate a response document including all successfully imported items and send that to the source system
  * track import errors
  * call another import which depends on the current one
  * create export documents (JSON / CSV / XML etc.) which other systems can use as import source
  * create response documents for single-page application / PWA frontend requests
* execute imports and exports with the built-in REST API
* Skipping records from the import source, e.g. if data is missing or the quality is insufficient
* easy import of relations
* automatically assign elements to relations via artificial intelligence / machine learning
* Import of object hierarchies / object trees
  * Specification of the parent element possible
  * Option to optimize inheritance (data is entered as high as possible in the object hierarchy)
* Automatic translation of texts via translation providers (via DeepL or AWS API)
* Support of all Pimcore data types including relations with metadata, object bricks, field collections etc.
* optimized performance:
  * If the source data has not changed, the import of the data record can be skipped
  * If data of an object is not changed in the import, it does not need to be saved
* Possibility to revert imports:
  * If an attribute assignment error has crept in and several thousand objects have been filled with incorrect data, the change can be reverted - in this case only the fields mapped in the import are set back, only for the objects changed in the import - a big advantage over a complete backup restore

## Documentation

To learn more about all options and how they can be configured, please [read the full documentation](https://pimcore.blackbit.de/Blackbit/1.pimcore/Handb%C3%BCcher/Ultima-Import-Bundle.pdf).