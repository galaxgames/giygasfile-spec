# Giygasfile Format Specification
Version 0

## Properties and Definitions

### Properties
| Property                      |             |
|-------------------------------|-------------|
| Endianness                    | Unspecified |
| Floating point format         | Unspecified | 

### Sizes
| Expression                    |Byte Size |
|-------------------------------|----------|
| sizeof([unsigned] char)       |        1 |
| sizeof([unsigned] short int)  |        2 |
| sizeof([unsigned] int)        |        4 |

## Structure

### Primary Structure
| Field                              | Size (bytes)  | Format         |
|------------------------------------|---------------|----------------|
| magic numbers / format identifier  |             8 | char[8]        |
| version code                       |             4 | unsigned int   |
| object (repeated)                  |               |                |
| - tag                              |             4 | unsigned int   |
| - data                             |      variable | object         |
| (end of file)                      |               |                |

#### Primary Structure Descriptions
| Name | Description|
|-|-|
| magic numbers | will always represent the ascii string `giygas` (with two spaces at the end). |
| version code | The version of the format encoded. (See top of document) |
| object (repeated) | The data objects composing the file. 

#### Object Structure Descriptions
| Name | Description|
|-|-|
| tag | An integer tag defining what type of object is encoded next. See the tag types below. |
| data | The data for the next object. Size is determined by the type of object encoded, or it's contents. |


### Tag Types
These tags define different types of data that can be encoded within a giygasfile.

| Name                        | Value |
|-----------------------------|-------|
| Vertex Buffer               | 0     |
| Element Buffer              | 1     |
| Vertex Attribute Definition | 2     |

### Vertex Buffer Structure
| Field                              | Size (bytes)  | Format              |
|------------------------------------|---------------|---------------------|
| size                               |             4 | unsigned int        |
| data                               |          size | unsigned char[size] |

#### Vertex Buffer Descriptions
| Name | Description|
|-|-|
| size | The size in bytes of the vetex buffer data. |
| data | Raw vertex buffer data |


### Element Buffer Structure
| Field                              | Size (bytes)     | Format                          |
|------------------------------------|------------------|---------------------------------|
| count                              |                4 | unsigned int                    |
| element size                       |                4 | unsigned int                    |
| data                               | n * element_size | unsigned char[n * element_size] |

#### Element Buffer Descriptions
| Name | Description|
|-|-|
| count | Count of elements described by the element buffer. |
| element size | the byte size of each element contained in the element buffer. |
| data | Raw element buffer data |


### Vertex Attribute Definition Structure
| Field                               | Size (bytes) | Format         |
|-------------------------------------|--------------|----------------|
| layout count                        |            2 | unsigned short |
| vertex buffer layout (repeated)     |              |                |
| - attribute count                 |            2 | unsigned short |
| - attribute definition (repeated) |              |                |
| - - component size              |            1 | unsigned char  |
| - - component count             |            1 | unsigned char  |

#### Vertex Attribute Definition Descriptions
| Name | Description|
|-|-|
| layout count | The count of vertex buffer layout objects encoded |
| vertex buffer layout (repeated) | The vertex buffer layouts |

#### Vertex Buffer Layout Descriptions
| Name | Description|
|-|-|
| attribute count | The count of attribute definition objects encoded |
| attribute definition (repeated) | The definitions of each attribute |

#### Attribute Definition Descriptions
Note: The attribute offset is determined by the component size and count of the previously encoded attribute definitions. This may change in a future version.

| Name | Description|
|-|-|
| component size | The byte size of each vertex component defined by this attribute |
| component count | The count of vertex componenets this vertex attribute contains (e.g. 1 -> single, 2 -> Vector2, 3 -> Vector3, and so on)|

