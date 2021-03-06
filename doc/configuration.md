# OnEarth Configuration

This documentation will go through the steps needed to configure the OnEarth server with imagery.

## Apache and mod_onearth

Dependent RPMs: 
* onearth

Steps:
* [Configure Apache](config_apache.md)
* [Configure Endpoint](config_endpoint.md)

## Image Archive

Dependent RPMs: 
* gibs-gdal
* onearth-mrfgen

Please refer to the following documentation:
[Creating Image Archive](archive.md)


## Imagery Layers

Dependent RPMs: 
* gibs-gdal
* onearth-config

Steps:
* Generate MRF metadata file
* Generate Empty Tile (Optional) 
* Generate Legend Images (Optional) 
* Generate ColorMap 
* Update/Create OnEarth [Layer Configuration](config_layer.md) file 
* Update/Create OnEarth [Support Configuration](config_support.md) files 
* Execute OnEarth Layer Configuration tool
* Restart Apache

The following steps involve the use of the [OnEarth Layer Configuration tool](../src/layer_config/README.md).  These steps should allow one to become familiar with the tool and demonstrate how to quickly configure a layer on the OnEarth server.

### Generate MRF metadata file

The MRF metadata file refers to the .mrf portion of an MRF triplet of files.  For example: [MODIS_Aqua_AerosolTTTTTTT_.mrf](../src/layer_config/test/MODIS_Aqua_AerosolTTTTTTT_.mrf)

Configuration files for the server are generated by reading the MRF metadata files for each of the available layers.  This allows the server to store a binary configuration that can be quickly accessed with minimal performance overhead.

The MRF metadata file may simply be copied from an existing [image archive](archive.md) or generated from scratch using the [mrfgen](../src/mrfgen/README.md) tool.

The following example shows how to generate an MRF file to be used as an archetype for the layer.

1) Run the mrfgen tool to generate an MRF image.  Source imagery may be found [here](..src/mrfgen/test/mrfgen_test_config.xml).  The test configuration may be found [here](../src/mrfgen/test/MYR4ODLOLLDY).
```Shell
mrfgen -c mrfgen_test_config.xml
```

2) Copy the .mrf header file to a "headers" subdirectory with your layer configuration directory.  If there is a timestamp at the end of the filename, replace it with "TTTTTTT".
```Shell
cp MYR4ODLOLLDY2014277_.mrf /etc/onearth/config/headers/MYR4ODLOLLDYTTTTTTT_.mrf
```
 
### Generate Empty Tile (Optional)

### Generate Legend Images (Optional) 

### Generate ColorMap
 
### Update/Create OnEarth Layer Configuration file

### Update/Create OnEarth Support Configuration files

### Execute OnEarth Layer Configuration tool

### Restart Apache

## Log Metrics