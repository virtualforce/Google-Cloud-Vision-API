# Google-Cloud-Vision-API
Google Cloud Vision API enables developers to understand the content of an image by encapsulating powerful machine learning models in an easy to use REST API. It quickly classifies images into thousands of categories (e.g., "sailboat", "lion", "Eiffel Tower"), detects individual objects and faces within images, and finds and reads printed words contained within images.

## Getting Started
The Visoin API has very broader scope but here we will discuss only two features and its API Implementation:

1. Text Detection (OCR)   
2. Label Detection

Lets move to API Implementation first because both of a same kind & have identical implementation.

### API Implementation?

#### Endpoint
The Vision API consists of a single endpoint (https://vision.googleapis.com/v1/images) that supports one HTTP request method (annotate):
POST https://vision.googleapis.com/v1/images:annotate

#### Body
The body of your POST request contains a JSON object of type AnnotateImageRequest, such as:

```
{
  "image": {
    object(Image)
  },
  "features": [
    {
      object(Feature)
    }
  ],
  "imageContext": {
    object(ImageContext)
  },
}
```
#### Input Image
 
![](https://github.com/farhanh/raw-images/blob/master/abbey_road.png "Sample")

## 1. Text Detection (OCR)
The Vision API can detect and extract text from images. For example, a photograph might contain a street sign or traffic sign. 
The JSON includes the entire extracted string, as well as individual words, and their bounding boxes. 
Here we are discussing only one feature that support OCR:

- TEXT_DETECTION   

### Sample Request
Image can be sent as a base64-encoded string, a Google Cloud Storage file location, or as a publicly-accessible URL, ImageContext is optional & used very rarely based on your request parameters, So we are skipping it. 
You can try this request in Google Vision API [console](https://developers.google.com/apis-explorer/?hl=en_GB#p/vision/v1/):

```
{
  "requests": [
    {
      "image": {
        "content": "/9j/7QBEUGhvdG9zaG9...base64-encoded-image-content...fXNWzvDEeYxxxzj/Coa6Bax//Z"
      },
      "features": [
        {
          "type": "TEXT_DETECTION"
        }
      ]
    }
  ]
}
```

### Sample Response
```
{
  "responses": [
    {
      "textAnnotations": [
        {
          "locale": "en",
          "description": "ABBEY\nROAD NW8\nCITY OF WESTMINSTER\n",
          "boundingPoly": {
            "vertices": [
              {
                "x": 45,
                "y": 43
              },
              {
                "x": 269,
                "y": 43
              },
              {
                "x": 269,
                "y": 178
              },
              {
                "x": 45,
                "y": 178
              }
            ]
          }
        },
        {
          "description": "ABBEY",
          "boundingPoly": {
            "vertices": [
              {
                "x": 45,
                "y": 50
              },
              {
                "x": 181,
                "y": 43
              },
              {
                "x": 183,
                "y": 80
              },
              {
                "x": 47,
                "y": 87
              }
            ]
          }
        },
        {
          "description": "ROAD",
          "boundingPoly": {
            "vertices": [
              {
                "x": 48,
                "y": 96
              },
              {
                "x": 155,
                "y": 96
              },
              {
                "x": 155,
                "y": 132
              },
              {
                "x": 48,
                "y": 132
              }
            ]
          }
        },
        {
          "description": "NW8",
          "boundingPoly": {
            "vertices": [
              {
                "x": 182,
                "y": 95
              },
              {
                "x": 269,
                "y": 95
              },
              {
                "x": 269,
                "y": 130
              },
              {
                "x": 182,
                "y": 130
              }
            ]
          }
        },
        {
          "description": "CITY",
          "boundingPoly": {
            "vertices": [
              {
                "x": 51,
                "y": 162
              },
              {
                "x": 85,
                "y": 161
              },
              {
                "x": 85,
                "y": 177
              },
              {
                "x": 51,
                "y": 178
              }
            ]
          }
        },
        {
          "description": "OF",
          "boundingPoly": {
            "vertices": [
              {
                "x": 95,
                "y": 162
              },
              {
                "x": 111,
                "y": 162
              },
              {
                "x": 111,
                "y": 176
              },
              {
                "x": 95,
                "y": 176
              }
            ]
          }
        },
        {
          "description": "WESTMINSTER",
          "boundingPoly": {
            "vertices": [
              {
                "x": 124,
                "y": 162
              },
              {
                "x": 249,
                "y": 160
              },
              {
                "x": 249,
                "y": 174
              },
              {
                "x": 124,
                "y": 176
              }
            ]
          }
        }
      ]
    }
  ]
}
```

## 2. Label Detection
The Vision API can detect and extract information about entities within an image, across a broad group of categories. 
Labels can identify objects, locations, activities, animal species, products, and more.
we need to specify LABEL_DETECTION as the value of features.type, same as above, done for TEXT_DETECTION:

- LABEL_DETECTION 

API implementation would be the same as described above, so moving to next step

### Sample Request

```
{
  "requests": [
    {
      "image": {
        "source": {
          "imageUri": "https://cloud.google.com/vision/docs/images/ferris-wheel.jpg"
        }
      },
      "features": [
        {
          "type": "LABEL_DETECTION"
        }
      ]
    }
  ]
}
```

### Sample Response
```
{
  "responses": [
    {
      "labelAnnotations": [
        {
          "mid": "/m/017rgb",
          "description": "ferris wheel",
          "score": 0.84832066
        },
        {
          "mid": "/m/010jjr",
          "description": "amusement park",
          "score": 0.8101249
        },
        {
          "mid": "/m/01d74z",
          "description": "night",
          "score": 0.8036025
        },
        {
          "mid": "/m/05b0n7k",
          "description": "outdoor recreation",
          "score": 0.68825835
        },
        {
          "mid": "/m/02jf28",
          "description": "fair",
          "score": 0.6566326
        }
      ]
    }
  ]
}
```



