# 01 SBoM Creation 

# Overview

Command line script **01_cyclonedx-cli_csv_to_cdx.cmd** illustrates how to create an SBoM in format CycloneDX from a CSV file using Open Source tool cyclonedx-cli.

# Points of Interest

Although the command line script is pretty trivial, it might be confusing to you what it actually does.

If you are familiar with the SBoM concept, SBoM contents and SBoM formats, feel free to skip this documentation. For all other readers who are not yet familiar with SBoMs: continue reading.

## Input CSV file 

The file .\input\mini_toolchain_components.csv is a simple file with comma-separated values.

If you inspect the first line of this file, then you will find the following attributes there:

- Supplier
- Name
- Version
- LicenseExpressions
- LicenseNames
- Copyright
- Cpe 
- Purl
- Description

So what is the motivation behind this file?

Consider you want to document all components in your software project. There are many different ways how you could do that. File **mini_toolchain_components.csv** shows  you a simple and pragmatic approach how to do that.

The approach is simple and pragmatic because it focusses on the most important component information.

With the attributes above, you cover the most important attributes for both SBoM standards: SPDX and CycloneDX.

Most of the attributes are self-explaining - let's have a closer look at the attributes that might be new to you.

### LicenseExpressions and LicenseNames
There are many Open Source licenses out there in the Open Source universe. For the most well known licenses, there are license identifiers like "Apache-2.0" that are useful for clearly identifying a license with a short name. Check the (SPDX license list)[https://spdx.org/licenses/] column "Identifier" for all well known licenses and their license identifier. For your SBoM you should add the licenses identifier of a component in column "LicenseExpression". 

If the license of a component cannot be found in the SPDX license list, then leave the "LicenseExpression" empty, and add the license name to the "LicenseNames" column.

### Copyright
Some Open Source components come with a copyright file. For those components, add the copyrigth to the "Copyright" column of your SBoM.

### CPE
[CPEs](https://en.wikipedia.org/wiki/Common_Platform_Enumeration) are identifiers for components which are used to document vulnerabilities. Not all components have a registered CPE. Whenever you integrate a component into your project, you should check whether the component has a registered CPE. CPE research can be done through (NIST CPE search)[https://nvd.nist.gov/products/cpe/search]

### PURL
[PURLs](https://en.wikipedia.org/wiki/Persistent_uniform_resource_locator) are concise way to clearly indicate the origin of a component. Whenever you download a component, you should use a PURL to document where you retrieved the component.
File mini_toolchain_components.csv gives you some examples for PURLs for components from GitHub.


## cyclonedx-cli Command Line

The command line in "01_cyclonedx-cli_csv_to_cdx.cmd" is not very spectacular: it only specifies the "convert" command, as well as the input/output file, and the input/ouput format.

The cyclonedx-cli tool is capable of converting between numerous formats - we are using csv to CycloneDX json conversion in this example.

Please note that you could not simply add additional column names to the .csv file, because cyclonedx-cli supports only the column names given in the [example file](https://github.com/CycloneDX/cyclonedx-cli/blob/main/example.csv).

## Conversion result 

The conversion result in file .\output\mini_toolchain_sbom.cdx.json is a SBoM file in CycloneDX json format. 

Note that all the attributes from the .csv file properly end up in the CycloneDX attributes.

With this first simple step you have created an SBoM for your project. Now you have an SBoM in a standardized format that can be processed by numerous other tools!




