# Symbol Text Link Format Specification

## Overview

* The current specification is designed to link images to text held within text boxes within the same document.
* It is designed for documents containing separate images and text boxes - for example presentation documents.
* The format originates from creating symbolising software to work with PowerPoint.
* Interoperability with Google Slides, and Keynote has so far been considered.

## Goals

* Use of the format by different providers will enable users to switch symbolising tools and for the new tool to be able to recognise symbols that are already in the document - providing a smooth transition for the user between using their old tool and their new tool.

## Where symbols information should go in a document

Typically the following are available to store additional data to associate with an object/shape in a document:

* Name of the object or shape
* Alternative text

### Shape or object name

#### Symbol meta information

Typically documents include a means for naming objects or shapes, and usually these can be accessed throught the object model of the software - for example PowerPoint.

In PowerPoint the maximum length of the name associated with an object/shape is 256 characters.

When a PowerPoint document is opened in KeyNote (and other software), the name associated with an object/shape is preserved.

**The maximum length of the symbol meta information associated with a shape/object is 256 characters**
**The symbol meta information for a shape/object should be stored in its name field (or equivalent)**

### Alternative text

#### Copyright information

For images, the first part of the text should contain copyright information - more details on how this can be formatted are below.

**Include copyright information - where available - in the first part of the alt text on an image**

#### Symbol meta information

When PowerPoint slides are open with Google Slides, names are not preserved. So, in order to preserve this information, the data within the name field of the object/shape should also be included in the alt text field. This applies to both images and text boxes.

This meta information should be preceded by the following to indicate that it is not part of the normal alt text:

` ```SYMBOLISER-CODE:`

For example:
` ```SYMBOLISER-CODE:List:the-noun-proje...$online,File:117683,MyId:9,SldId:256,TxtBoxId:4,WPos:0,PicIndex:1,DW:39.684,DH:39.684,Txt:hello
` ```SYMBOLISER-CODE:MyId:4,SldId:256,WordCount:1

**Symbol meta information should also be included in the alt text field - preceded by ```SYMBOLISER-CODE:MyId:4,SldId:256,WordCount:1**

## Meta information content

* Meta information is in the format ParameterKey:ParameterValue
* Parameter key-value pairs are separated by commas
* Parameter values cannot contain commas

### Text boxes

|            | Key length | Max chars | Total | Example/description                                                                                          |
|------------|------------|-----------|-------|--------------------------------------------------------------------------------------------------------------|
| MyId:      | 5          | 7         | 12    | Id of the textbox when first symbolised  - to check if this is a copy or original                            |
| SldId:     | 6          | 4         | 12    | Slide ID. Id of the slide where this text was first symbolised.                                              |
| WordCount: | 10         | 4         | 14    | Count of words (i.e. separated by  spaces) when first created.                                               |

### Images (symbols)

|           | Key length | Max chars | Total | Example/description                                                                                       |
|-----------|------------|-----------|-------|-----------------------------------------------------------------------------------------------------------|
| List:     | 5          | 24        | 29    | Name of list truncated - e.g. ARASAAC...                                                                  |
| File:     | 5          | 24        | 29    | File name truncated - cat nap...                                                                          |
| MyId:     | 5          | 7         | 12    | Id of the shape - created when the image is first created - to check if this is a symboliser item or not. |
| SldId:    | 6          | 4         | 10    | Slide ID. Id of the slide where this picture was added. Note shape IDs can duplicate between slides.      |
| TxtBoxId: | 9          | 7         | 16    | Refers to the text box that created it. e.g. 29                                                           |
| WPos:     | 5          | 4         | 9     | The index of a word in a phrase e.g. 12. Something like 50 words is the real max. This gives 9,999.       |
| PicIndex: | 9          | 3         | 12    | The index of the picture from the set of pictures used.                                                   |
| DW:       | 3          | 8         | 11    | Default width (pts)                                                                                       |
| DH:       | 3          | 8         | 11    | Default height (pts)                                                                                      |
| X:        | 3          | 8         | 11    | Horizontal position (pts) when the image                                                                  | was added(pts) |
| Y:        | 3          | 8         | 11    | Vertical position (pts) when the image was added(pts)                                                     |
| Txt:      | 4          | 64        | 68    | The text that matched e.g. "cat"                                                                          |
| WS:       | 3          | 4         | 7     | Character position for start of the phrase - to use in a future align symbols to words option.            |
| Commas:   |            | 11        | 11    | Commas separating the parameters                                                                          |
| TOTAL     | 45         | 16        | 245   | Some leeway under 255.                                                                                    |



