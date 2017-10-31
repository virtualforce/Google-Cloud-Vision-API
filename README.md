# Google-Cloud-Vision-API
Google Cloud Vision API enables developers to understand the content of an image by encapsulating powerful machine learning models in an easy to use REST API. It quickly classifies images into thousands of categories (e.g., "sailboat", "lion", "Eiffel Tower"), detects individual objects, faces within images, finds/reads printed words and contained within images.

## Getting Started
The Visoin API has very broader scope but we will discuss only two features and its API Implementation here:

1. Text Detection (OCR)   
2. Label Detection

Lets move to API Implementation Schema first to know about its usage

### API Implementation Schema

#### Endpoint
The Vision API consists of a single endpoint (https://vision.googleapis.com/v1/images) that supports one HTTP request method (annotate):
POST https://vision.googleapis.com/v1/images:annotate

#### Authentication
If your client application does not use OAuth 2.0, then it must include an API key when it calls an API that's enabled within a Google Cloud Platform project. The application passes this key into all API requests as a key=API_key parameter,             
such as:
```
POST https://vision.googleapis.com/v1/images:annotate?key=YOUR_API_KEY
```
we are just testing these API in Google Vision API [console](https://developers.google.com/apis-explorer/?hl=en_GB#p/vision/v1/) therefore we can work without authentication.

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

#### Console
You can try requests mentioned below in Google Vision API [console](https://developers.google.com/apis-explorer/?hl=en_GB#p/vision/v1/)

## 1. Text Detection (OCR)
The Vision API can detect and extract text from images. For example, a photograph might contain a street sign or traffic sign. 
The JSON includes the entire extracted string, as well as individual words, and their bounding boxes.         
Here we are discussing only one feature that support OCR:

- TEXT_DETECTION   

#### Input Image
 
![](https://github.com/farhanh/raw-images/blob/master/abbey_road.png "Sample")

### Sample Request
Image can be sent as a base64-encoded string, a Google Cloud Storage file location, or as a publicly-accessible URL, ImageContext is optional & used very rarely based on your request parameters, so we are skipping it. 

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
              ...
            ]
          }
        },
        {
          "description": "ROAD",
          "boundingPoly": {
            "vertices": [
             ...
            ]
          }
        },
        {
          "description": "NW8",
          "boundingPoly": {
            "vertices": [
             ...
            ]
          }
        },
        {
          "description": "CITY",
          "boundingPoly": {
            "vertices": [
             ...
            ]
          }
        },
        {
          "description": "OF",
          "boundingPoly": {
            "vertices": [
             ...
            ]
          }
        },
        {
          "description": "WESTMINSTER",
          "boundingPoly": {
            "vertices": [
             ...
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

#### Input Image
 
![](https://github.com/farhanh/raw-images/blob/master/ferris-wheel.jpg "Sample")

### Sample Request

```
{
  "requests": [
    {
      "image": {
        "source": {
          "imageUri": "https://github.com/farhanh/raw-images/blob/master/ferris-wheel.jpg"
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



